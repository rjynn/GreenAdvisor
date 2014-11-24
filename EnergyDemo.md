# JUNIT SERVICE

[watch the demo video](https://archive.org/details/junit_greenminer)

Junit service allows users to upload an android app and junit apk and have their tests run on greenminer, with their power consumption measured.

# Example: 
You have an app in Eclipse with a Junit test suite. Follow the steps:
1) Run the Junit test suite.
2) Find the project path by:
   i) Right click on your Android app project
   ii) Click on Properties
   iii) Under Resources, you will find Location field.
   iv) Copy the Location, that is your project path(PROJECT_PATH)
3) Find the TEST project path by:
   i) Right click on your Android Junit test project
   ii) Click on Properties
   iii) Under Resources, you will find Location field.
   iv) Copy the Location, that is your test project path(TEST_PROJECT_PATH)
4) Open a terminal
5) In the terminal run the command:

    wget https://pizza.cs.ualberta.ca/gm/junit_service_client

6) Now run the command in the terminal

    chmod +x junit_service_client

7) Now, run this command:
   
    ./junit_service_client --batch <your Team Name > --schedule <PROJECT_PATH/bin/YOUR_APP.apk>    <TEST_PROJECT_PATH/bin/YOUR_APP.apk> 

8) Write down the ID that it generates, you may need it later.
9) At the end of execution, you will be able to see graphs.


It consists of three major parts:

## web/junit_service.py

This provides an http endpoint for scheduling junit tests and getting the progress

POST: form encoded data:
         app: android app .apk file
         suite: junit test suite .apk

output: json
        repetitions: 5
        id: a uuid that you can call GET with

GET:
    url data:
        id: the id you got from posting

    json output:
        runs_remaining: the number of runs remaining

## util/junit_service_client.py

check the runs_remaining:

        junit_service_client.py --check <id>

schedule tests and then check every 30 seconds to see if they are done

        junit_service_client.py --schedule <app .apk file> <junit .apk file>

## the junit test

gets apks and runs the tests

