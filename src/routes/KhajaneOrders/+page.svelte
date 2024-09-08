<div class="container-xl">
    <div class="row row-card">
    <div class="col-md-4">
        <div class="card rounded-0 border-primary">
          <div class="card-header bg-blue rounded-0">
            <h3 class="card-title text-white">6th Pay  Details/6ನೇ ವೇತನ ಮಾಹಿತಿ</h3>
          </div>
          <div class="card-body">
            
            <div class="mb-3">
              <label class="form-label required" for="">Present Family Pension Pay/ಈಗಿನ ಕುಟುಂಬ ಪಿಂಚಣಿ ವೇತನ</label>
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
    <div class="col-md-8 h-100">
        <div class="card h-100 rounded-0  border-primary">
          <div class="card-header rounded-0 bg-blue">
            <h3 class="card-title text-white">7th Pay Details/7ನೇ ವೇತನ ಆಯೋಗದ ವರದಿಯಂತೆ</h3>
          </div>
          <div class="card-body">
            

            <div class="table-responsive">
              <table
                    class="table table-vcenter table-bordered table-wrap">
                <thead>
                  <tr>
                    <th>Current Family Pension Pay /ಈಗಿನ ಕುಟಂಬ ಪಿಂಚಣಿ ವೇತನ </th>
                    
                    <th>New Family Pension Pay /ಪರಿಷ್ಕ್ರತ ಕುಟುಂಬ ಪಿಂಚಣಿ ವೇತನ As on 01-08-2024 </th>
                    
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
            <div class="table-responsive pt-1">
              <table
                    class="table table-vcenter table-bordered table-wrap">
                <thead>
                  <tr>
                    
                    <th>DA/ತುಟ್ಟಿ ಭತ್ಯೆ </th>
                    
                    <th>Gross Family Pension/ ಒಟ್ಟು ಕುಟುಂಬ ಪಿಂಚಣಿ ವೇತನ </th>
                    
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