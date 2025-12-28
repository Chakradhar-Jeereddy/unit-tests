Unit Test frameworks
===
- Jest
- Junit

How it works?
===
- We test the components individually (bascially we test the functions)
- It is not apposible to access database in Unit test
- We mock/mimic the database results

Work flow
===
- We call unit test in jenkins pipeline.
```
        stage('Unit Test') {
            steps {
                script{
                    sh """
                        npm test
                    """
                }
            }
        }
```
- It will the test script in package.json
- Also the required dependencies.
```
{
  "name": "catalogue",
  "version": "1.1.0",
  "description": "product catalogue REST API",
  "main": "server.js",
  "scripts": {
    "test": "jest --coverage --forceExit",
    "coverage": "jest --coverage --coverageReporters=lcov --forceExit"
  },

## dependencies
  "devDependencies": {
    "jest": "^29.0.0",
    "supertest": "^6.3.0"
  }
```
- The script will execute the server.test.js file
- All test cases available in the test.js file

Results
===
- The test will generate the results and the results will be stored in location mentioned in sonar-project.properties
- The file would be available in jenkins node where the job was executed.
```
sonar.projectKey=roboshop-catalogue
sonar.projectName="roboshop catalogue"
sonar.sources=.
sonar.exclusions=Jenkinsfile, Dockerfile, **/db/**, **/node_modules/**, coverage/**,__mocks__/**,**/*.test.js
sonar.tests=.
sonar.test.inclusions=**/*.test.js
sonar.javascript.lcov.reportPaths=coverage/lcov.info
```
- The results include **How many tests?**, **How many success?**, **How many failed?** ,**How many lines covered?**
- We send this report to sonarqube
- It will showup under the project.
- We can set quality gate against it to fail or pass the pipeline.
  
#### Vulnerabilities
Security issues in the code that could be exploited by attackers (e.g., SQL injection, hard-coded secrets). These represent real security risks.

#### Bugs
Coding errors that may cause incorrect behavior, crashes, or unexpected results at runtime.

#### Code Smells
Maintainability issues that don’t break functionality but make the code harder to read, understand, or modify (e.g., duplicated code, complex methods).

#### Security Rating
Overall score (A–E) indicating the security quality of the code, based mainly on detected vulnerabilities.

#### Maintainability Rating
Score (A–E) representing how easy the code is to maintain, calculated from code smells and technical debt.

#### Code Coverage
Percentage of code executed by automated tests, showing how well the codebase is tested.
