<script>

import {add,parse,format,isFirstDayOfMonth,sub,lastDayOfMonth,differenceInMonths,differenceInYears} from "date-fns";

let minPension = 13500;
let maxPension = 120600;
let maxFamilyPension = 80400;
let inputReact = ""
let dcrgMax = 20000000;
let DA = 8.5


let CF = {
	'17':19.28,'18':19.2,'19':19.11,'20':19.01,'21':18.91,'22':18.81,'23':18.7,'24':18.59,'25':18.47,'26':18.34,'27':18.21,'28':18.07,'29':17.93,'30':17.78,'31':17.62,'32':17.46,'33':17.29,'34':17.11,'35':16.92,'36':16.72,'37':16.52,'38':16.31,'39':16.09,'40':15.87,'41':15.64,'42':15.4,'43':15.15,'44':14.9,'45':14.64,'46':14.37,'47':14.1,'48':13.82,'49':13.54,'50':13.25,'51':12.95,'52':12.66,'53':12.35,'54':12.05,'55':11.73,'56':11.42,'57':11.1,'58':10.78,'59':10.46,'60':10.13,'61':9.81,'62':9.48
}



let formValues = {
	"dateOfBirth" : "dd/mm/yyyy",
	"dateOfJoin" : "dd/mm/yyyy",
    "dateOfRetire" : "dd/mm/yyyy",
	"halfYrs" : 0,
	"totalYrs" : 0,
    "lastPay" : 0,
    "pendingEL" : 0,
    "DCRG" : 0,
	"pension":0,
	"enhancedFamilyPension":0,
	"familyPension":0,
	"commutation":0,
	"typePension": "Superannuation",
	"encashEL" : 0,
	
	
}

function parseDate(a){
	return parse(a, "dd/MM/yyyy", new Date())
}

function fixRetirementDate(a){
	if (isFirstDayOfMonth(a)) {
		return sub(a, {days:1})
	}

	return lastDayOfMonth(a)
}

function setReadOnly(){
	if(formValues.typePension == "Superannuation"){
		inputReact = "readonly"
	}else{
		inputReact = ""
	}

	
}

function calculatePension() {
    
	const dob = parseDate(formValues.dateOfBirth)
	const doj = parseDate(formValues.dateOfJoin)
	let dor ;
	if(formValues.typePension == "Superannuation"){
		dor = fixRetirementDate(add(dob,{years:60}));
		formValues.dateOfRetire = format(dor, "dd/MM/yyyy");
	}else {
		dor = parseDate(formValues.dateOfRetire);
	}

	
	let months = differenceInMonths(dor,doj) ;
	formValues.totalYrs = Math.trunc(months / 12) ;
	let halfYrs = Math.trunc(months / 6) ;
	formValues.halfYrs = halfYrs > 60 ? 60 : halfYrs ;



	let pension = Math.round((formValues.lastPay / 2)*(formValues.halfYrs/60))
	if (pension > maxPension){
		formValues.pension = maxPension ;
	}else if(pension < minPension){
		formValues.pension = minPension ;
	}else{
		formValues.pension = pension ;
	}

	let enhancedFamilyPension =  Math.round(formValues.lastPay * 0.50) ;
	let normalFamilyPension = Math.round(formValues.lastPay * 0.30) ;
	let twiceNormalFP = normalFamilyPension * 2 ;


	if (formValues.typePension == "Death") {
		formValues.enhancedFamilyPension = enhancedFamilyPension <= twiceNormalFP ? enhancedFamilyPension : twiceNormalFP ;
		if(formValues.enhancedFamilyPension >= maxFamilyPension){
			formValues.enhancedFamilyPension = maxFamilyPension
		} else if (formValues.enhancedFamilyPension <= maxFamilyPension){
			formValues.enhancedFamilyPension = minPension
		}
		
		formValues.familyPension = normalFamilyPension ;
		if(formValues.familyPension >= maxFamilyPension){
			
			formValues.familyPension = maxFamilyPension ;
		} else if(formValues.familyPension <= minPension){
			formValues.familyPension = minPension ;
			
		}
	} else{
		
		formValues.familyPension = normalFamilyPension ;
		if(formValues.familyPension >= maxFamilyPension){

			formValues.familyPension = maxFamilyPension ;
		} else if(formValues.familyPension <= minPension){
			formValues.familyPension = minPension ;

		}

		
	}

	let dcrg = Math.round((formValues.lastPay/4)*halfYrs)

	if(formValues.typePension == "Death"){

		switch (true) {
			case formValues.totalYrs < 1:
				formValues.DCRG = formValues.lastPay * 2
				break;
			case formValues.totalYrs >= 1 && formValues.totalYrs <= 5:
				formValues.DCRG = formValues.lastPay * 6 > dcrgMax ? dcrgMax : formValues.lastPay * 6 ;
	
				break;
			case formValues.totalYrs >= 5 && formValues.totalYrs <= 20:
				formValues.DCRG = formValues.lastPay * 12 > dcrgMax ? dcrgMax : formValues.lastPay * 12 ;
	
				break;
			case formValues.totalYrs > 20:
				formValues.DCRG = (formValues.lastPay/2)*formValues.halfYrs > dcrgMax ? dcrgMax : (formValues.lastPay/2)*formValues.halfYrs ;
	
				break;
		
			
		}
	} else{
		formValues.DCRG = dcrg > dcrgMax ? dcrgMax : dcrg ;
	}

	

	let age = (differenceInYears(dor,dob) + 1).toString() ;


	formValues.commutation = Math.round(0.4 * formValues.pension * 12 * CF[age]) ;

	formValues.encashEL = Math.round(((formValues.lastPay + (formValues.lastPay * (DA / 100)))/30)*formValues.pendingEL) ;


	
	







	

	


	
}


	
</script>

<svelte:head>
	<title>Karnataka Pension and Family Pension Calculator - For Government of Karnataka Employees</title>
	<meta name="description" content="Easily calculate your pension and family pension entitlements as per Government of Karnataka rules. Get accurate estimates and understand your pension benefits online.">

    
</svelte:head>





<main>
	<div class="row row-card">
		<div class="col-md-4">
			<div class="card h-100">
				<div class="card-header">
					<h3 class="card-title">Pension Calculator/ನಿವೃತ್ತಿ ಪಿಂಚಣಿ ಲೆಕ್ಕ </h3>
				</div>
				<div class="card-body">
					<div class="mb-3">
						<div class="form-label">Type of Pension</div>
						<div>
						  <label class="form-check form-check-inline">
							<input class="form-check-input" bind:group={formValues.typePension} type="radio" value="Superannuation" name="radios-inline" >
							<span class="form-check-label">Superannuation</span>
						  </label>
						  <label class="form-check form-check-inline">
							<input class="form-check-input" bind:group={formValues.typePension} type="radio" value="Death" name="radios-inline">
							<span class="form-check-label">Death</span>
						  </label>
						  <label class="form-check form-check-inline">
							<input class="form-check-input" bind:group={formValues.typePension} type="radio" value="Voluntary" name="radios-inline" >
							<span class="form-check-label">Voluntary</span>
						  </label>
						</div>
					  </div>
					
					
					<div class="mb-3">
                        <label class="form-label" for="">Date of Birth/ ಜನ್ಮ ದಿನಾಂಕ</label>
                         <div class="input-icon mb-2">
                            <input type="text" name="input-mask" bind:value={formValues.dateOfBirth} id="datepicker" class="form-control" data-mask="00/00/0000" data-mask-visible="true" placeholder="00/00/0000" autocomplete="off">
                          <span class="input-icon-addon"><!-- Download SVG icon from http://tabler-icons.io/i/calendar -->
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="icon"><path stroke="none" d="M0 0h24v24H0z" fill="none"></path><path d="M4 7a2 2 0 0 1 2 -2h12a2 2 0 0 1 2 2v12a2 2 0 0 1 -2 2h-12a2 2 0 0 1 -2 -2v-12z"></path><path d="M16 3v4"></path><path d="M8 3v4"></path><path d="M4 11h16"></path><path d="M11 15h1"></path><path d="M12 15v3"></path></svg>
                          </span>
                        </div>
                        
                    </div>
					<div class="mb-3">
                        <label class="form-label" for="">Date of Joining/ ಸೇವೆಗೆ ಸೇರಿದ ದಿನಾಂಕ</label>
                         <div class="input-icon mb-2">
                            <input type="text" name="input-mask" bind:value={formValues.dateOfJoin} id="datepicker" class="form-control" data-mask="00/00/0000" data-mask-visible="true" placeholder="00/00/0000" autocomplete="off">
                          <span class="input-icon-addon"><!-- Download SVG icon from http://tabler-icons.io/i/calendar -->
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="icon"><path stroke="none" d="M0 0h24v24H0z" fill="none"></path><path d="M4 7a2 2 0 0 1 2 -2h12a2 2 0 0 1 2 2v12a2 2 0 0 1 -2 2h-12a2 2 0 0 1 -2 -2v-12z"></path><path d="M16 3v4"></path><path d="M8 3v4"></path><path d="M4 11h16"></path><path d="M11 15h1"></path><path d="M12 15v3"></path></svg>
                          </span>
                        </div>
                        
                    </div>
                    <div class="mb-3">
                        <label class="form-label" for="">Date of Retirement/ ನಿವೃತ್ತಿ ದಿನಾಂಕ</label>
                         <div class="input-icon mb-2">
							{#if formValues.typePension == "Superannuation"}
								<input class="form-control " readonly  placeholder="Select a date"  id="datepicker-icon" bind:value={formValues.dateOfRetire} >
							{:else}
								<input class="form-control "   placeholder="Select a date"  id="datepicker-icon" bind:value={formValues.dateOfRetire} >
							{/if}
                          
                          <span class="input-icon-addon"><!-- Download SVG icon from http://tabler-icons.io/i/calendar -->
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="icon"><path stroke="none" d="M0 0h24v24H0z" fill="none"></path><path d="M4 7a2 2 0 0 1 2 -2h12a2 2 0 0 1 2 2v12a2 2 0 0 1 -2 2h-12a2 2 0 0 1 -2 -2v-12z"></path><path d="M16 3v4"></path><path d="M8 3v4"></path><path d="M4 11h16"></path><path d="M11 15h1"></path><path d="M12 15v3"></path></svg>
                          </span>
                        </div>
                        
                    </div>
					<div class="mb-3">
						<label class="form-label required" for="">Last Pay 7th Pay</label>
						<div>
							<input
								type="number"
								class="form-control"
								bind:value={formValues.lastPay}
								placeholder="Curren Basic Pay"
							/>
							<small class="form-hint">ನಿಮ್ಮ ನಿವೃತ್ತಿಗೆ 7ನೇ ಮೂಲ ವೇತನವನ್ನು ನಮೂದಿಸಿ. </small>
						</div>
					</div>
                    <div class="mb-3">
						<label class="form-label required" for="">No of Earned Leave/ ಒಟ್ಟು ಗಳಿಕೆ ರಜೆ</label>
						<div>
							<input
								type="number"
								class="form-control"
								bind:value={formValues.pendingEL}
								placeholder="Curren Basic Pay"
							/>
							<small class="form-hint">ನಿಮ್ಮ ನಿವೃತ್ತಿ ಸಮಯದಲ್ಲಿ ಒಟ್ಟು ಉಳಿದಿರುವ ಗಳಿಕೆ ರಜೆ. </small>
						</div>
					</div>
					
					
				</div>
				<div class="card-footer text-end">
					<button type="submit" class="btn btn-danger">Clear</button>
					<button type="submit" class="btn btn-primary" on:click={calculatePension}>Submit</button>
				</div>
			</div>
		</div>
		<div class="col-md-8">
			<div class="card" id="result-print">
				<div class="card-header">
					<h3 class="card-title">Pensionary Benefit Details / ನಿವೃತ್ತಿ ಸೌಲಭ್ಯಗಳು </h3>
				</div>
				<div class="card-body" id="printJS-form">
					<div class="row">
						<div class="col">

							<p>Date of Birth</p>
							<p>{formValues.dateOfBirth}</p>
						</div>
						<div class="col">
							<p>Date of Joining</p>
							<p>{formValues.dateOfJoin}</p>
						</div>
						<div class="col">
							<p>Date of Retirement</p>
							<p>{formValues.dateOfRetire}</p>
						</div>
					</div>
					<div class="row">
						<div class="col">
							<p>Last Basic Pay</p>
							<p>₹ {formValues.lastPay}</p>
						</div>
						<div class="col">
							<p>Total Service in Yrs</p>
							<p>{formValues.totalYrs}</p>
						</div>
						<div class="col">
							<p>Total Service in Half Yrs</p>
							<p>{formValues.halfYrs}</p>
						</div>
						
					</div>
					<div class="hr-text">
						<span>Details of Pensionary Benefits </span>
					</div>
					<div class="row">
						<div class="col">
							<p>Type Pension</p>
							<p>{formValues.typePension}</p>
						</div>
						<div class="col">
							{#if formValues.typePension == "Death"}
								<p>Enhanced Family Pension</p>
								<p>₹ {formValues.pension}</p>
							{:else}
								<p>Basic Pension</p>
								<p>₹ {formValues.pension}</p>
							{/if}
							
						</div>
						
						<div class="col">
							<p>Family Pension</p>
							<p>₹ {formValues.familyPension}</p>
						</div>
						
					</div>
					<div class="row">
						<div class="col">
							<p>Death Cum Retirement Gratuity</p>
							<p>₹ {formValues.DCRG}</p>
						</div>
						<div class="col">
							<p>Earned Leave Encahment Value</p>
							<p>₹ {formValues.encashEL}</p>
						</div>
						<div class="col">
							<p>Commutation of Pension</p>
							{#if formValues.typePension == "Death"}
								<p>Not Applicable / ಅನ್ವಯಿಸುವುದಿಲ್ಲ </p>
							{:else}
								<p>₹ {formValues.commutation}</p>
							{/if}
							
						</div>
						
					</div>
					
            
            </div>
           
          
          
            
			
					
				
				<div class="card-footer text-end">
					<button  class="btn btn-facebook w-20" >
						<!-- Download SVG icon from http://tabler-icons.io/i/brand-facebook -->
						<svg
							xmlns="http://www.w3.org/2000/svg"
							width="24"
							height="24"
							viewBox="0 0 24 24"
							fill="none"
							stroke="currentColor"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
							class="icon icon-tabler icons-tabler-outline icon-tabler-printer"
							><path stroke="none" d="M0 0h24v24H0z" fill="none" /><path
								d="M17 17h2a2 2 0 0 0 2 -2v-4a2 2 0 0 0 -2 -2h-14a2 2 0 0 0 -2 2v4a2 2 0 0 0 2 2h2"
							/><path d="M17 9v-4a2 2 0 0 0 -2 -2h-6a2 2 0 0 0 -2 2v4" /><path
								d="M7 13m0 2a2 2 0 0 1 2 -2h6a2 2 0 0 1 2 2v4a2 2 0 0 1 -2 2h-6a2 2 0 0 1 -2 -2z"
							/></svg
						>
						Print
          </button>
				</div>
			</div>
		</div>
	</div>
</main>
