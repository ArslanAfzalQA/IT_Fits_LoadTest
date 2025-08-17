# JMeter Load Test Script for ITFits Mobile App

## Overview
This repository contains JMeter performance tests for the ITFits mobile application API. The test plan simulates real user workflows including authentication, food logging, activity tracking, sleep monitoring, and water intake logging.

## Key Features
- Dynamic data generation for timestamps and test data
- CSV-based parameterization for test inputs
- JSON response extraction for session management
- Modular test structure with transaction controllers
- Response validation and error checking

## Test Scenarios Covered
1. **Login & Dashboard**
   - User authentication
   - Home dashboard data retrieval
   - Restaurant list loading

2. **Food Log Management**
   - Food item search
   - Food logging
   - Daily food log retrieval

3. **Activities**
   - Step counting
   - Exercise logging
   - Activity details retrieval

4. **Sleep**
   - Sleep session logging
   - Sleep calculations
   - Sleep details retrieval

5. **Water**
   - Water intake logging
   - Daily water consumption details

## Prerequisites
- JMeter 5.6+
- Java 11+
- Basic understanding of JMeter concepts

## Setup Instructions

1. **Clone the repository**
Git Clone https://github.com/ArslanAfzalQA/IT_Fits_LoadTest.git


2. **Configure test parameters**
- Update `base_url` in User Defined Variables
- Modify CSV file paths if needed
- Adjust thread counts in Thread Group

3. **Prepare test data**
- Populate CSV files with required test data
- Ensure proper file paths in CSV Data Set Config elements

## Running Tests
jmeter -t ITFits_LoadTest.jmx

### GUI Mode (for debugging)
### CLI Mode (For Testing)

jmeter -n -t ITFits_LoadTest.jmx -l results/results.jtl -e -o results/dashboard



## Test Data Management
The test uses these CSV files for parameterization:
- `foodId.csv` - Contains food item IDs for testing
- (Add other CSV files as needed)

## Dynamic Data Generation
The script includes JSR223 PreProcessors that generate:
- Current date in YYYY-MM-dd format
- Dynamic timestamps for activity periods
- (Add other dynamic elements as needed)

## Session Management
- Authentication tokens are extracted from login responses
- User IDs are captured for subsequent requests
- Tokens are automatically added to request headers

## Validation
- Response assertions verify success flags in API responses
- View Results Tree provides detailed debugging (disable for load tests)

## Results Analysis
After CLI execution, view the HTML report in:


## Customization Guide
To adapt for your environment:
1. Update all `${base_url}` references
2. Modify CSV file paths and contents
3. Adjust thread counts and ramp-up periods
4. Update assertion criteria as needed

## Troubleshooting
| Issue | Solution |
|-------|----------|
| Token extraction fails | Verify JSON path matches API response |
| CSV data not loading | Check file paths and permissions |
| Dynamic date errors | Confirm Groovy is selected in JSR223 |
| SSL errors | Import certificates into JMeter's keystore |

## Notes
- Disable "View Results Tree" during load tests
- Monitor system resources during high-load tests
- Consider using distributed testing for heavy loads

For questions or issues, please contact Arslan at marslan.sqa@gmail.com