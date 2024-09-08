<script>

    let da = 31 ;
    let fixationRate = 27.5 ; 
    let newDA = 8.75 ;
    let minPension = 13500 ;
    let maxPension = 120600;
    
    let formValues = {
      "oldPay" : 0,
      "newPay" : 0,
      "newPayAug" : 0,
      "da" : 0,
      "payScale" : "Select",
      "hraGroup" : "",
      "gross" : 0,
      
    }
  
    function calculateSalary() {
          let newPayCalculated = formValues.oldPay + Math.round((formValues.oldPay*da)/100) + Math.round((formValues.oldPay*fixationRate)/100)
  
          if (newPayCalculated > maxPension) {
            formValues.newPayAug = maxPension;
          } else if(newPayCalculated < minPension) {
            formValues.newPayAug = minPension;
          } else {
            formValues.newPayAug = newPayCalculated;
          }
          formValues.da = Math.round((formValues.newPayAug*newDA)/100)
          formValues.gross = formValues.newPayAug + formValues.da;
    }
  
  </script>

<svelte:head>

<title>7th Pay Pension Fixation Karnataka Government , Basic Pension Salary , Gross Pension </title>

</svelte:head>
  
  <main>
    <div class="container-xl">
      <div class="row row-card">
      <div class="col-md-4">
          <div class="card  h-100 rounded-0 border-primary">
            <div class="card-header rounded-0 bg-blue">
              <h3 class="card-title text-white">6th Pay  Details/6ನೇ ವೇತನ ಮಾಹಿತಿ</h3>
            </div>
            <div class="card-body">
              
              <div class="mb-3">
                <label class="form-label required" for="">Present Pension Pay/ಈಗಿನ ಪಿಂಚಣಿ ವೇತನ</label>
                <div>
                  <input type="number" class="form-control" bind:value={formValues.oldPay} placeholder="Curren Basic Pay">
                  <small class="form-hint">
                      ಈಗಿನ ಮೂಲ ನಿವೃತ್ತಿ ವೇತನವನ್ನು ತಮ್ಮ ಪಿಂಚಣಿ ಪಾವತಿ ಆದೇಶದಲ್ಲಿ ಪಡೆಯುವಬಹುದಾಗಿದೆ. ಸರಿಯಾಗಿ ನಮೂದಿಸಿ.
                  </small>
                </div>
              </div>
              <div class="mb-3">
                    <small class="form-hint">
                      * ತುಟ್ಟಿ ಭತ್ಯೆಯನ್ನೂ ಆಯೋಗದ ವರದಿಯಂತೆ ಕೇಂದ್ರ ಸರಕಾರದ ತುಟ್ಟಿ ಭತ್ಯೆಗೆ 0.722% ರಷ್ಟು ರಾಜ್ಯ ಸರ್ಕಾರವು ತನ್ನ ನೌಕರರಿಗೆ ನೀಡುತ್ತದೆ.
                    
                    </small>
                
              </div>
              
            </div>
            <div class="card-footer border-primary text-end">
                <button type="submit" class="btn btn-danger">Clear</button>
                <button type="submit" class="btn btn-primary" on:click={calculateSalary}>Submit</button>
            </div>
          </div>
      </div>
      <div class="col-md-8">
          <div class="card h-100 rounded-0 border-primary">
            <div class="card-header rounded-0 bg-blue">
              <h3 class="card-title text-white">7th Pay Details/7ನೇ ವೇತನ ಆಯೋಗದ ವರದಿಯಂತೆ</h3>
            </div>
            <div class="card-body">
              
  
              <div class="table-responsive">
                <table
                      class="table table-vcenter table-bordered table-wrap">
                  <thead>
                    <tr>
                      <th>Current Pension Pay /ಈಗಿನ ಪಿಂಚಣಿ ವೇತನ </th>
                      
                      <th>New Pension Pay /ಪರಿಷ್ಕ್ರತ ಪಿಂಚಣಿ ವೇತನ As on 01-08-2024 </th>
                      
                    </tr>
                  </thead>
                  <tbody>
                    <tr>
                      <td>{formValues.oldPay}</td>
                      
                      <td>{formValues.newPayAug}</td>
                      
                    
                    
                    </tr>
                  </tbody>
                </table>
              </div>
              <div class="table-responsive pt-1 ">
                <table
                      class="table table-vcenter table-bordered table-wrap">
                  <thead>
                    <tr>
                      
                      <th>DA/ತುಟ್ಟಿ ಭತ್ಯೆ </th>
                      
                      <th>Gross Pension/ ಒಟ್ಟು ನಿವೃತ್ತಿ ವೇತನ </th>
                      
                    </tr>
                  </thead>
                  <tbody>
                    <tr>
                      <td>{formValues.da}</td>
                      <td>{formValues.gross}</td>
                     
                      
                    
                    
                    </tr>
                  </tbody>
                </table>
              </div>
                
              
            </div>
            
          </div>
      </div>
      </div>
    </div>
  </main>