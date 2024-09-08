<script>


	let da = 31;
	let fixationRate = 27.5;
	let newDA = 8.5;
	let oldDAJan = 42.5;

	let oldHraRates = {
		A: 24,
		B: 16,
		C: 8
	};

	let hraRates = {
		A: 20,
		B: 15,
		C: 7.5
	};

	let formValues = {
		oldPay: 0,
		presentPay: 0,
		newPay: 0,
		newPayAug: 0,
		payScale: 'Select',
		seventhpayScale: '',
		sixthpayScale: '',
		hraGroup: 'C',
		group: 'A',
		daPay: 0,
		hraPay: 0,
		mediAll: 0,
		gross: 0,
		sxithgross: 0,
		sixthDA: 0,
		sixthPayConvert: 0,
		incrementJanJul2023:0,
		incrementJanJul2024:0,
	};

	let sixthPay2022 = {
		basicPay: 0,
		da: 0,
		hra: 0,
		medAll: 0,
		IR: 0,
		gross: 0
	};

	let sevenPay2022 = {
		basicPay: 0,
		da: 0,
		hra: 0,
		medAll: 0,

		gross: 0
	};

	let sixthPay2024 = {
		basicPay: 0,
		da: 0,
		hra: 0,
		medAll: 0,
		IR: 0,
		gross: 0
	};

	let sevenPay2024 = {
		basicPay: 0,
		da: 0,
		hra: 0,
		medAll: 0,

		gross: 0
	};

	let scaleExtract = [
		27000, 27650, 28300, 28950, 29600, 30325, 31050, 31775, 32500, 33300, 34100, 34900, 35700,
		36600, 37500, 38400, 39300, 40300, 41300, 42300, 43300, 44425, 45550, 46675, 47800, 49050,
		50300, 51550, 52800, 54175, 55550, 56925, 58300, 59800, 61300, 62800, 64300, 65950, 67600,
		69250, 70900, 72550, 74200, 76100, 78000, 79900, 81800, 83700, 85600, 87900, 90200, 92500,
		94800, 97100, 99400, 102100, 104800, 107500, 110200, 112900, 115600, 118700, 121800, 124900,
		128000, 131100, 134200, 137700, 141200, 144700, 148200, 151700, 155200, 159200, 163200, 167200,
		171200, 175200, 179200, 183700, 188200, 192700, 197200, 201700, 206200, 211200, 216200, 221200,
		226200, 231200, 236200, 241200
	];
	let scaleExtractSixthPay = [
		17000, 17400, 17800, 18200, 18600, 19050, 19500, 19950, 20400, 20900, 21400, 21900, 22400,
		22950, 23500, 24050, 24600, 25200, 25800, 26400, 27000, 27650, 28300, 28950, 29600, 30350,
		31100, 31850, 32600, 33450, 34300, 35150, 36000, 36950, 37900, 38850, 39800, 40900, 42000,
		43100, 44200, 45300, 46400, 47650, 48900, 50150, 51400, 52650, 53900, 55350, 56800, 58250,
		59700, 61150, 62600, 64250, 65900, 67550, 69200, 70850, 72500, 74400, 76300, 78200, 80100,
		82000, 83900, 86100, 88300, 90500, 92700, 94900, 97100, 99600, 102100, 104600, 107100, 109600,
		112100, 114900, 117700, 120500, 123300, 126100, 128900, 132000, 135100, 138200, 141300, 144400,
		147500, 150600
	];
	let payScaleData = [
		{
			id: 1,
			sixthPay: '17000-400-18600-450-20400-500-22400-550-24600-600-27000-650-28950',
			seventhPay: '27000-650-29600-725-32500-800-35700-900-39300-1000-43300-1125-46675',
			max: 46675,
			min: 27000
		},
		{
			id: 2,
			sixthPay: '18600-450-20400-500-22400-550-24600-600-27000-650-29600-750-32600',
			seventhPay: '29600-725-32500-800-35700-900-39300-1000-43300-1125-47800-1250-52800',
			max: 52800,
			min: 29600
		},
		{
			id: 3,
			sixthPay:
				'19950-450-20400-500-22400-550-24600-600-27000-650-29600-750-32600-850-36000-950-37900',
			seventhPay:
				'31755-725-32500-800-35700-900-39300-1000-43300-1125-47800-1250-52800-1375-58300-1500-61300',
			max: 61300,
			min: 31755
		},
		{
			id: 4,
			sixthPay:
				'21400-500-22400-550-24600-600-27000-650-29600-750-32600-850-36000-950-39800-1100-42000',
			seventhPay:
				'34100-800-35700-900-39300-1000-43300-1125-47800-1250-52800-1375-58300-1500-64300-1650-67600',
			max: 67600,
			min: 34100
		},
		{
			id: 5,
			sixthPay:
				'23500-550-24600-600-27000-650-29600-750-32600-850-36000-950-39800-1100-46400-1250-47650',
			seventhPay:
				'37500-900-39300-1000-43300-1125-47800-1250-52800-1375-58300-1500-64300-1650-74200-1900-76100',
			max: 76100,
			min: 37500
		},
		{
			id: 6,
			sixthPay: '25800-600-27000-650-29600-750-32600-850-36000-950-39800-1100-46400-1250-51400',
			seventhPay:
				'41300-1000-43300-1125-47800-1250-52800-1375-58300-1500-64300-1650-74200-1900-81800',
			max: 81800,
			min: 41300
		},
		{
			id: 7,
			sixthPay: '27650-650-29600-750-32600-850-36000-950-39800-1100-46400-1250-52650',
			seventhPay: '44425-1125-47800-1250-52800-1375-58300-1500-64300-1650-74200-1900-83700',
			max: 83700,
			min: 44425
		},
		{
			id: 8,
			sixthPay: '30350-750-32600-850-36000-950-39800-1100-46400-1250-53900-1450-58250',
			seventhPay: '49050-1250-52800-1375-58300-1500-64300-1650-74200-1900-85600-2300-92500',
			max: 92500,
			min: 49050
		},
		{
			id: 9,
			sixthPay: '33450-850-36000-950-39800-1100-46400-1250-53900-1450-62600',
			seventhPay: '54175-1375-58300-1500-64300-1650-74200-1900-85600-2300-99400',
			max: 99400,
			min: 54175
		},
		{
			id: 10,
			sixthPay: '36000-950-39800-1100-46400-1250-53900-1450-62600-1650-67550',
			seventhPay: '58300-1500-64300-1650-74200-1900-85600-2300-99400-2700-107500',
			max: 107500,
			min: 58300
		},
		{
			id: 11,
			sixthPay: '37900-950-39800-1100-46400-1250-53900-1450-62600-1650-70850',
			seventhPay: '61300-1500-64300-1650-74200-1900-85600-2300-99400-2700-112900',
			max: 112900,
			min: 61300
		},
		{
			id: 12,
			sixthPay: '40900-1100-46400-1250-53900-1450-62600-1650-72500-1900-78200',
			seventhPay: '65950-1650-74200-1900-85600-2300-99400-2700-115600-3100-124900',
			max: 124900,
			min: 65950
		},
		{
			id: 13,
			sixthPay: '43100-1100-46400-1250-53900-1450-62600-1650-72500-1900-83900',
			seventhPay: '69250-1650-74200-1900-85600-2300-99400-2700-115600-3100-134200',
			max: 134200,
			min: 69250
		},
		{
			id: 14,
			sixthPay: '45300-1100-46400-1250-53900-1450-62600-1650-72500-1900-83900-2200-88300',
			seventhPay: '72550-1650-74200-1900-85600-2300-99400-2700-115600-3100-134200-3500-141200',
			max: 141200,
			min: 72550
		},
		{
			id: 15,
			sixthPay: '48900-1250-53900-1450-62600-1650-72500-1900-83900-2200-97100-2500-99600',
			seventhPay: '78000-1900-85600-2300-99400-2700-115600-3100-134200-3500-148200',
			max: 148200,
			min: 78000
		},
		{
			id: 16,
			sixthPay: '52650-1250-53900-1450-62600-1650-72500-1900-83900-2200-97100',
			seventhPay: '83700-1900-85600-2300-99400-2700-115600-3100-134200-3500-155200',
			max: 155200,
			min: 83700
		},
		{
			id: 17,
			sixthPay: '56800-1450-62600-1650-72500-1900-83900-2200-97100-2500-99600',
			seventhPay: '90200-2300-99400-2700-115600-3100-134200-3500-155200-4000-159200',
			max: 159200,
			min: 90200
		},
		{
			id: 18,
			sixthPay: '61150-1450-62600-1650-72500-1900-83900-2200-97100-2500-102100',
			seventhPay: '97100-2300-99400-2700-115600-3100-134200-3500-155200-4000-163200',
			max: 163200,
			min: 97100
		},
		{
			id: 19,
			sixthPay: '67550-1650-72500-1900-83900-2200-97100-2500-104600',
			seventhPay: '107500-2700-115600-3100-134200-3500-155200-4000-167200',
			max: 167200,
			min: 107500
		},
		{
			id: 20,
			sixthPay: '70850-1650-72500-1900-83900-2200-97100-2500-104600',
			seventhPay: '112900-2700-115600-3100-134200-3500-155200-4000-171200',
			max: 171200,
			min: 112900
		},
		{
			id: 21,
			sixthPay: '74400-1900-83900-2200-97100-2500-109600',
			seventhPay: '118700-3100-134200-3500-155200-4000-175200',
			max: 175200,
			min: 118700
		},
		{
			id: 22,
			sixthPay: '82000-1900-83900-2200-97100-2500-112100-2800-117700',
			seventhPay: '131100-3100-134200-3500-155200-4000-179200-4500-188200',
			max: 188200,
			min: 131100
		},
		{
			id: 23,
			sixthPay: '90500-2200-97100-2500-112100-2800-123300',
			seventhPay: '144700-3500-155200-4000-179200-4500-197200',
			max: 197200,
			min: 144700
		},
		{
			id: 24,
			sixthPay: '97100-2500-112100-2800-128900-3100-141300',
			seventhPay: '155200-4000-179200-4500-206200-5000-226200',
			max: 226200,
			min: 155200
		},
		{
			id: 25,
			sixthPay: '104600-2500-112100-2800-128900-3100-150600',
			seventhPay: '167200-4000-179200-4500-206200-5000-241200',
			max: 241200,
			min: 167200
		}
	];

	function calculateSalary() {
		let oldPayIndex = scaleExtractSixthPay.indexOf(formValues.presentPay);
		formValues.oldPay = scaleExtractSixthPay[oldPayIndex - 2];
		let newPayCalculated =
			formValues.oldPay +
			Math.round((formValues.oldPay * da) / 100) +
			Math.round((formValues.oldPay * fixationRate) / 100);

		if (formValues.group == 'C' || formValues.group == 'D') {
			formValues.mediAll = 500;
		} else {
			formValues.mediAll = 0;
		}

		scaleExtract.some(function (ele, index) {
			if (newPayCalculated >= payScaleData[Number(formValues.payScale) - 1].max) {
				formValues.newPay = payScaleData[Number(formValues.payScale) - 1].max;
				formValues.newPayAug = scaleExtract[scaleExtract.indexOf(formValues.newPay) + 2];
				console.log(1);
				return true;
			} else if (newPayCalculated <= payScaleData[Number(formValues.payScale) - 1].min) {
				formValues.newPay = payScaleData[Number(formValues.payScale) - 1].min;
				formValues.newPayAug = scaleExtract[scaleExtract.indexOf(formValues.newPay) + 2];
				console.log(2);
				return true;
			} else if (ele > newPayCalculated) {
				if (ele > payScaleData[Number(formValues.payScale) - 1].max) {
					formValues.newPay = payScaleData[Number(formValues.payScale) - 1].max;
					formValues.newPayAug = formValues.newPay;
					formValues.newPayAug = scaleExtract[index + 2];
					console.log(3);
				} else if (ele < payScaleData[Number(formValues.payScale) - 1].min) {
					formValues.newPay = payScaleData[Number(formValues.payScale) - 1].min;
					formValues.newPayAug = formValues.newPay;
					formValues.newPayAug = scaleExtract[index + 2];
					console.log(4);
				} else {
					formValues.newPay = ele;
					formValues.newPayAug = scaleExtract[index + 2];
					console.log(5);
				}
				return true;
			}
		});




		formValues.seventhpayScale = payScaleData[Number(formValues.payScale) - 1].seventhPay;
		formValues.sixthpayScale = payScaleData[Number(formValues.payScale) - 1].sixthPay;
		let tempHRA = formValues.hraGroup;
		formValues.daPay = Math.round((formValues.newPayAug * newDA) / 100);
		formValues.hraPay = Math.round((formValues.newPayAug * hraRates[tempHRA]) / 100);
		formValues.gross =
			formValues.newPayAug + formValues.daPay + formValues.hraPay + formValues.mediAll;
		let mediAll = formValues.group == 'C' || formValues.group == 'D' ? 200 : 0;
		formValues.sxithgross =
			formValues.presentPay +
			Math.round((formValues.presentPay * oldDAJan) / 100) +
			Math.round((formValues.presentPay * oldHraRates[tempHRA]) / 100) +
			mediAll +
			Math.round((formValues.presentPay * 17) / 100);

		formValues.incrementJanJul2023 = scaleExtract[scaleExtract.indexOf(formValues.newPay)+1] ;
		formValues.incrementJanJul2024 = scaleExtract[scaleExtract.indexOf(formValues.newPay)+2] ;



		sixthPay2024.basicPay = formValues.presentPay;
		sixthPay2022.basicPay = formValues.oldPay;
		sixthPay2024.da = Math.round((sixthPay2024.basicPay * oldDAJan) / 100);
		sixthPay2022.da = Math.round((sixthPay2022.basicPay * da) / 100);
		sixthPay2024.hra = Math.round((sixthPay2024.basicPay * oldHraRates[tempHRA]) / 100);
		sixthPay2022.hra = Math.round((sixthPay2022.basicPay * oldHraRates[tempHRA]) / 100);
		sixthPay2024.medAll = formValues.group == 'C' || formValues.group == 'D' ? 200 : 0;
		sixthPay2022.medAll = formValues.group == 'C' || formValues.group == 'D' ? 200 : 0;
		sixthPay2024.IR = Math.round((sixthPay2024.basicPay * 17) / 100);
		sixthPay2022.IR = Math.round((sixthPay2022.basicPay * 17) / 100);
		sixthPay2024.gross =
			sixthPay2024.basicPay +
			sixthPay2024.da +
			sixthPay2024.hra +
			sixthPay2024.medAll +
			sixthPay2024.IR;
		sixthPay2022.gross =
			sixthPay2022.basicPay +
			sixthPay2022.da +
			sixthPay2022.hra +
			sixthPay2022.medAll +
			sixthPay2022.IR;

		sevenPay2024.basicPay = formValues.newPayAug;
		sevenPay2022.basicPay = formValues.newPay;
		sevenPay2024.da = Math.round((sevenPay2024.basicPay * newDA) / 100);
		sevenPay2022.da = Math.round((sevenPay2022.basicPay * 0) / 100);
		sevenPay2024.hra = Math.round((sevenPay2024.basicPay * hraRates[tempHRA]) / 100);
		sevenPay2022.hra = Math.round((sevenPay2022.basicPay * hraRates[tempHRA]) / 100);
		sevenPay2024.medAll = formValues.group == 'C' || formValues.group == 'D' ? 500 : 0;
		sevenPay2022.medAll = formValues.group == 'C' || formValues.group == 'D' ? 500 : 0;
		sevenPay2024.gross =
			sevenPay2024.basicPay + sevenPay2024.da + sevenPay2024.hra + sevenPay2024.medAll;
		sevenPay2022.gross =
			sevenPay2022.basicPay + sevenPay2022.da + sevenPay2022.hra + sevenPay2022.medAll;
	}

	

</script>

<svelte:head>
	<title>Karnataka 7th Pay Commission Salary Calculator - For Government of Karnataka Employees</title>
	<meta name="description" content="Quickly calculate your salary as per the 7th Pay Commission rules for Karnataka government employees. Get accurate estimates of basic pay, allowances, and deductions. Easy-to-use salary calculator for Karnataka state government staff.">

</svelte:head>

<main>
	<div class="row row-card">
		<div class="col-md-4">
			<div class="card h-100 rounded-0 border-primary">
				<div class="card-header rounded-0 bg-blue text-white">
					<h3 class="card-title">SIXTH Pay Details/6ನೇ ವೇತನ ಮಾಹಿತಿ</h3>
				</div>
				<div class="card-body">
					<div class="mb-3">
						<label class="form-label required" for="">Current Pay Scale/ಪ್ರಸ್ತುತ ವೇತನ ಶ್ರೇಣಿ</label>
						<div>
							<select class="form-select" bind:value={formValues.payScale}>
								<option value="Select">Select Pay Current Scale</option>
								{#each payScaleData as data}
									<option value={data.id}>sixth Pay / {data['sixthPay']}</option>
								{/each}
							</select>
							<small class="form-hint"
								>ನಿಮ್ಮ ವೇತನ ಶ್ರೇಣಿಯನ್ನು <a href="https://hrmsess.karnataka.gov.in">
									hrmsess.karnataka.gov.in
								</a> ಪಡೆಯಿರಿ.
							</small>
						</div>
					</div>
					<div class="mb-3">
						<label class="form-label required" for="">Present Basic Pay/ಈಗಿನ ಮೂಲ ವೇತನ</label>
						<div>
							<input
								type="number"
								class="form-control"
								bind:value={formValues.presentPay}
								placeholder="Curren Basic Pay"
							/>
							<small class="form-hint">01.07.2024 ಕ್ಕೆ  ಮೂಲ ವೇತನವನ್ನು ನಮೂದಿಸಿ. </small>
						</div>
					</div>
					<div class="row">
						<div class="col-6">
							<div class="mb-3">
								<label class="form-label" for="">Employee Group/ನೌಕರನ ವರ್ಗ</label>
								<div>
									<select class="form-select" bind:value={formValues.group}>
										<option value="A">A</option>
										<option value="B">B</option>
										<option value="C">C</option>
										<option value="D">D</option>
									</select>
									<small class="form-hint"> ನಿಮ್ಮ ಪದನಾಮವು ಯಾವ ವರ್ಗಕ್ಕೆ ಸೇರುತ್ತದೆ. </small>
								</div>
							</div>
						</div>
						<div class="col-6">
							<div class="mb-3">
								<label class="form-label" for="">HRA City Grade/ಮನೆ ಬಾಡಿಗೆ ಭತ್ಯೆ ವರ್ಗ</label>
								<div>
									<select class="form-select" bind:value={formValues.hraGroup}>
										<option>A</option>
										<option>B</option>
										<option>C</option>
									</select>
									<small class="form-hint">
										ನೀವು ವೇತನ ಪಡೆಯುವ ಕಚೇರಿಯು ಯಾವ ವರ್ಗಕ್ಕೆ ಸೇರುತ್ತದೆ ಎಂದು ಆಯ್ಕೆ ಮಾಡಿ.
									</small>
								</div>
							</div>
						</div>
					</div>
					<div class="mb-3">
						<small class="form-hint text-justify">** ಈ ವೆಬ್‌ಸೈಟ್ ನಲ್ಲಿ 7 ನೇ ವೇತನಕ್ಕಾಗಿ ಅಂದಾಜು ವೇತನವನ್ನು ಲೆಕ್ಕಹಾಕಬಹುದು. ಇದು ಮಾನ್ಯ ಸರಕಾರದ ಅಧಿಕೃತ ವೆಬ್‌ ಸೈಟ್‌ ಆಗಿರುವುದಿಲ್ಲ. </small>
						<small class="form-hint text-justify">** ಈ ವೆಬ್‌ಸೈಟ್ ನಲ್ಲಿ ತುಟ್ಟಿ ಭತ್ಯೆಯಾನ್ನು Jul-2022 - 0% , Jan-2023 - 2.88%, Jul-2023 - 2.88%, Jan-2024 - 2.88% ಒಟ್ಟು ತುಟ್ಟಿ ಭತ್ಯೆ - 8.75% ಎಂದು ಅಂದಾಜು ಪರಿಗಣಿಸಲಾಗಿದೆ. ಮಾನ್ಯ ಘನ ಸರಕಾರದ ಯಾವುದೇ ಅಧಿಕೃತ ಆದೇಶವಿರುವುದಿಲ್ಲ. </small>
						
					</div>
				</div>
				<div class="card-footer text-end border-primary">
					<button type="submit" class="btn btn-danger">Clear</button>
					<button type="submit" class="btn btn-primary" on:click={calculateSalary}>Submit</button>
				</div>
			</div>
		</div>
		<div class="col-md-8">
			<div class="card rounded-0 border-primary" id="result-print">
				<div class="card-header rounded-0 bg-blue   text-white">
					<h3 class="card-title">Seventh Pay Details/7ನೇ ವೇತನ ಆಯೋಗದ ವರದಿಯಂತೆ</h3>
				</div>
				<div class="card-body" id="printJS-form">
					<div class="table-responsive">
						<table class="table table-vcenter table-bordered table-wrap">
							<thead>
								<tr>
									<th class="text-wrap">Current Pay Scale/ಈಗೀನ ವೇತನ ಶ್ರೇಣಿ</th>
									<th class="text-wrap">New Pay Scale/ಪರಿಷ್ಕ್ರತ ವೇತನ ಶ್ರೇಣಿ</th>
								</tr>
							</thead>
							<tbody>
								<tr>
									<td>{formValues.sixthpayScale}</td>
									<td>
										{formValues.seventhpayScale}
									</td>
								</tr>
							</tbody>
						</table>
					</div>
					<div class="hr-text">
						<span>Increment on 2023 & 2024 / ಕಾಲಿಕ ವೇತನ ಬಡ್ತಿ 2023 & 2024 </span>
					</div>
					<div class="table-responsive">
						<table
							  class="table table-vcenter table-bordered table-wrap">
						  <thead>
							<tr>
							  <th class="text-wrap">7th Pay As on 01.07.2022 / 7ನೇ ವೇತನ 01.07.2022 </th>
							  <th class="text-wrap">ಕಾಲಿಕ ವೇತನ ಬಡ್ತಿ Jan/Jul 2023 </th>
							  <th class="text-wrap">ಕಾಲಿಕ ವೇತನ ಬಡ್ತಿ Jan/Jul 2024 </th>
							  
							</tr>
						  </thead>
						  <tbody>
							<tr>
							  <td>{formValues.newPay}</td>
							  <td>{formValues.incrementJanJul2023}</td>
							  <td>{formValues.incrementJanJul2024}</td>
							</tr>
						  </tbody>
						</table>
					  </div>
					<!-- <div class="table-responsive">
              <table
                    class="table table-vcenter table-bordered table-wrap">
                <thead>
                  <tr>
                    <th>6th Pay As On 01-07-2022 / ವೇತನ 01-07-2022 </th>
                    <th>New Pay /ಪರಿಷ್ಕ್ರತ ವೇತನ As on 01-07-2022 </th>
                    <th>New Pay /ಪರಿಷ್ಕ್ರತ ವೇತನ As on 01-08-2024 </th>
                    
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <td>{formValues.oldPay}</td>
                    <td>{formValues.newPay}</td>
                    <td>{formValues.newPayAug}</td>
                    
                  
                  
                  </tr>
                </tbody>
              </table>
            </div>
            <div class="hr-text">
              <span>Allowance Details / ಭತ್ಯೆಗಳ ಮಾಹಿತಿ</span>
            </div>
            <div class="table-responsive">
              <table
                    class="table table-vcenter table-bordered table-wrap">
                <thead>
                  <tr>
                    
                    <th>DA/ತುಟ್ಟಿ ಭತ್ಯೆ </th>
                    <th>HRA / ಮನೆ ಬಾಡಿಗೆ ಭತ್ಯೆ </th>
                    <th>Medical Allowance/ ವೈದ್ಯಕೀಯ ಭತ್ಯೆ </th>
                    <th>Gross Salary/ ಒಟ್ಟು ವೇತನ </th>
                    
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <td>{formValues.daPay}</td>
                    <td>{formValues.hraPay}</td>
                    <td>{formValues.mediAll}</td>
                    <td>{formValues.gross}</td>
                    
                  
                  
                  </tr>
                </tbody>
              </table>
            </div>
            <div class="hr-text">
              <span>Comparision of Pay / ಹೊಸ ಮತ್ತು ಹಳೆಯ ವೇತನ ವ್ಯತ್ಯಾಸ</span>
            </div>
            <div class="table-responsive">
              <table
                    class="table table-vcenter table-bordered table-wrap">
                <thead>
                  <tr>
                    <th>6th Pay Gross / ಒಟ್ಟು ವೇತನ </th>
                    <th>7th Pay Gross / ಒಟ್ಟು ವೇತನ </th>
                    <th>Diffence Amount / ವ್ಯತ್ಯಾಸ ಮೊತ್ತ </th>
                    
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <td>{formValues.sxithgross}</td>
                    <td>{formValues.gross}</td>
                    <td>{formValues.gross - formValues.sxithgross}</td>
                    
                  
                  
                  </tr>
                </tbody>
              </table>
            </div> -->
			<div class="hr-text">
				<span>Comparision of New Pay and Old Pay / ಹಳೆಯ ಮತ್ತು ಹೊಸ ವೇತನ</span>
			</div>
					<div class="col-12">
						<div class="table-responsive">
							<table class="table table-vcenter table-bordered table-wrap">
								<thead>
									<tr>
										<th>ವೇತನ ಆಯೋಗದ ಹೆಸರು</th>
										<th class="text-wrap">6ನೇ ವೇತನ ಆಯೋಗ /6th Pay Commission 01.07.2022</th>
										<th class="text-wrap">7ನೇ ವೇತನ ಆಯೋಗ /7th Pay Commission 01.07.2022</th>
										<th class="text-wrap">6ನೇ ವೇತನ ಆಯೋಗ /6th Pay Commission 01.07.2024</th>
										<th class="text-wrap">7ನೇ ವೇತನ ಆಯೋಗ /7th Pay Commission 01.08.2024</th>
										<th class="text-wrap">ವ್ಯತ್ಯಾಸ ವೇತನ 01.08.2024 /Difference of Pay</th>
									</tr>
								</thead>
								<tbody>
									<tr>
										<th>Basic Pay/ ಮೂಲ ವೇತನ</th>
										<td>₹. {sixthPay2022.basicPay}</td>
										<td>₹. {sevenPay2022.basicPay}</td>
										<td>₹. {sixthPay2024.basicPay}</td>
										<td>₹. {sevenPay2024.basicPay}</td>
										<td>₹. {sevenPay2024.basicPay - sixthPay2024.basicPay}</td>
									</tr>

									<tr>
										<th>Dearness Allowance/ ತುಟ್ಟಿ ಭತ್ಯೆ</th>
										<td>₹. {sixthPay2022.da}</td>
										<td>₹. {sevenPay2022.da}</td>
										<td>₹. {sixthPay2024.da}</td>
										<td>₹. {sevenPay2024.da}</td>
										<td>₹. {sevenPay2024.da - sixthPay2024.da}</td>
									</tr>
									<tr>
										<th>House Rent Allowance/ ಮನೆ ಬಾಡಿಗೆ ಭತ್ಯೆ</th>
										<td>₹. {sixthPay2022.hra}</td>
										<td>₹. {sevenPay2022.hra}</td>
										<td>₹. {sixthPay2024.hra}</td>
										<td>₹. {sevenPay2024.hra}</td>
										<td>₹. {sevenPay2024.hra - sixthPay2024.hra}</td>
									</tr>
									<tr>
										<th>Medical Allowance / ವೈದ್ಯಕೀಯ ಭತ್ಯೆ</th>
										<td>₹. {sixthPay2022.medAll}</td>
										<td>₹. {sevenPay2022.medAll}</td>
										<td>₹. {sixthPay2024.medAll}</td>
										<td>₹. {sevenPay2024.medAll}</td>
										<td>₹. {sevenPay2024.medAll - sixthPay2024.medAll}</td>
									</tr>
									<tr>
										<th>Interim Relief / ತಾತ್ಕಾಲಿಕ ಪರಿಹಾರ</th>
										<td>₹. {sixthPay2022.IR}</td>
										<td>NA</td>
										<td>₹. {sixthPay2024.IR}</td>
										<td>NA</td>
										<td>₹. {0 - sixthPay2024.IR}</td>
									</tr>
									<tr>
										<th>Gross Salary / ಒಟ್ಟು ವೇತನ</th>
										<td>₹. {sixthPay2022.gross}</td>
										<td>₹. {sevenPay2022.gross}</td>
										<td>₹. {sixthPay2024.gross}</td>
										<td>₹. {sevenPay2024.gross}</td>
										<td>₹. {sevenPay2024.gross - sixthPay2024.gross}</td>
									</tr>
								</tbody>
							</table>
						</div>
					</div>
				</div>
				<div class="card-footer text-end border-primary">
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
