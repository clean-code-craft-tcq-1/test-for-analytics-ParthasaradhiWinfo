# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file.
2. PDF Generator.
3. Notification provider.
4. File Validator.

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No 			| Need to use mock functionality to test behaviour
Counting the breaches       | Yes			| Need to test the logical written for counting becauses not I/O
Detecting trends            | Yes			| Need to test the logical written for trends becauses not I/O
Notification utility        | No 			| Need to use mock functionality to test behaviour

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write test case for count of breaches reaching threshold in month.
4. Write test case for record trends in 30 mins.
5. Test case for PDF Generator.
6. Test Case for Notification provider.


### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | PDF File	  | Sent/error		            | Mock it is a IO Operation
Report inaccessible server | csv file path| success/ file not found     | Fake file path
Find minimum and maximum   | csv data 	  | Maximum/ minimum            | None - it's a pure function
Detect trend               | mock csv data| count of trend              | None - it's a pure function
Write to PDF               | mock data 	  | pdf report                  | Mock it is a IO Operation
