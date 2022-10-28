# election-analysis-module-3
This is the repository for the third module of the data analytics bootcamp. 
# Election Analysis for U.S. Congressional Precinct in Colorado

## Project Overview
The purpose of this project is to analyze the vote count for Congressional Preceinct of Colorado and more specifically to determine the following:
    - The total number of votes casted.
    - The complete list of counties in the congressional precinct. 
    - The percentage of votes from each county out of the total count.
    - The voter turnout for each county. 
    - The county with the highest turnout.
    - The complete list of candidates who received votes. 
    - The percentage of votes each candidate won and the total number of votes each candidate received.
    - The winner of the election based on popular vote.

## Results
### Per Candidate Basis
- The analysis of the election shows that:
  - There were **369,711** votes cast in the election.
- The candidates were:
    - Charles Casper Stockham
    - Diana DeGette
    - Raymon Anthony Doane
- The candidate results were:
    - Charles Casper Stockham received **23.0%** of the vote and **85,213** of votes.
    - Diana DeGette received **73.8%** of the vote and **272,892** of votes.
    - Raymon Anthony Doane received **3.1%** of the vote and **11,606** of votes.
- The winner of the election was:
    - **Diana DeGette**, who received **73.8%** of the vote and **272,892** of votes.

### Per County Basis
- The analysis of the election shows that:
- The counties results were:
    - Jefferson with a **10.5%** vote of the total count and **38,855** voter turnout.
    - Denver with an **82.8%** vote of the total count and **306,055** voter turnout.
    - Arapahoe with a **6.7%** vote of the total count and **24,801** voter turnout.
- The county with the largest voter turnout was:
    - **Denver** with an **82.8%** vote of the total count and **306,055** voter turnout.
    
### Overview of Methods and Code

#### Opening, Reading, and Writing Code
In order to ecexecute the election analysis, it is important to correctly import the requisite datafiles needed to run the analysis. In this case, we were required to pull in a .csv file with the election data utilizing the correct import dependencies. Below I have provided an example of the process. 

***1. Import Dependencies.***

```python s=
import csv
import os
```

From a functional standpoint, the breakdown of data looks as follows:

- `import csv` - allows us to easily pull in data from external CSV files and perform operations on them. This dependency also includes the following functions:
   - `next()` - skips the row.
   - `reader()` - reads each row from the csv file and return data as a lists of strings.
      
It is important to know how the data are returned after reading, and to know the properties of a dataset! `reader()`, returns data as a list (each row is a new list). Lists are mutable and ordered (indexed), so we can access (loop through) the elements via indexes.

- `import os` - allows to interact with the operating system. This dependency also includes the following functions:
   - `path()` - allows us to access files on different operating systems.
   - `join()` - joins file path components together when they are provided as separate strings; then, it returns a direct path with the appropriate operating system separator, forward slash for macOS or backward slash for Windows.

***2. Declaring Variables and Loading File Paths.***

This provides the framework for future file reading and mappipng file paths for storage and retrieval. 

```python s=
file_to_load = os.path.join("Resources", "election_results.csv")
```
- `file_to_load` - declares a variable for the file.
- `Resources` - represents the directory of the file.
- `election_results.csv` - the ultimate name of the file.

Directory has to be provided exactly in order to be able to correctly pull files into the terminal and interpret.

***3. Open and read the file.***

```python s=
with open(file_to_load) as election_data:
   file_to_read = csv.reader(election_data)
```

- `with open()` - This represents the statement opens the file and ensures the proper acquisition of data.
- `as <new_variable_name>` - assigning alias to a variable. It can be whatever you need it to be. 
- `csv.reader()` - reads each row from the csv file and returns data as lists of strings. 
- `file_to_read` - a new variable that will be used in the for loop to access the elements via indices.

Function `with open(file_to_load, “r”)` doesn’t have to be declared by method “r” as in “read mode”. If you omit the mode argument, Python will open the file in read-only mode by default so the the demarcation is unecessary. 

***4. Additional Code for Writing a File.***

```python s=
file_to_save = os.path.join("Analysis", "election_results.txt")
```
This line of code will create a file "election_results.txt" in the “Analysis" folder if the file doesn’t exist yet. The folder must already exist, otherwise an error (Error02) will occur.

```python s=
with open(file_to_save, "w") as txt_file:
```
In this function, we must specify the method `“w”` as in `write mode` in order to be able to write any text in the given file. When using "w" method, Python will owerwrite existing contents if the file already exists. To avoid that, we can use `"a"` as in `append` method which simply adds to the given file. If a file does not exist, it creates one, if a file has been created the data will be added to the file (i.e append).

```python s=
txt_file.write(election_results)
```
With the Python function `write()` we declare what to write in a txt_file that already exists in our given file path. txt_file is a new variable that is passed on from “original variable file_to_save”. In parentheses (election_results) is a name of a variable that contains data about what we want to write in a file and ultimately use as an output.

#### Looping Through Dictionaries
In order to correctly retrieve elements or loop through specific data sets, it is important to know the properties of those specific lists. Lists are mutable and therefore we are able to index, slice, and manipulate. Dictionaries are mutable and unordered which means we are not able to slice, index, or edit them. Dictionary keys are also immutable and have to be unique, while values are mutable.

Below is an example line of code from the module. 

```python s=
   #Retrieving unique values with a conditional statement and membership operator (not in).
   if candidate_name not in candidate_options:
          #Appending new values(candidate_name) the list (candidate_options) with the append() method.
          candidate_options.append(candidate_name)
            
          #Creating a new key [candidate_name] in a dictionary (candidate_votes) and assigning a new value to its key by initializing the value `=0`.
          #And begin tracking key's value (candidate's voter count). 
          candidate_votes[candidate_name] = 0
   # Add a vote to that candidate's count. Indentation is important 
   # and it has to be aligned with if statement, otherwise values wouldn’t be increment properly.
   candidate_votes[candidate_name] += 1
```

#### The get() method 

There are two ways to retrive values from a dictionary by its keys. With **"square brackets"** or with **"get()" method**:
Here is an example with square brackets:
```python s=
for candidate_name in candidate_votes:
   votes = candidate_votes[candidate_name]
```
Here is an example with the get() method:
```python s=
for candidate_name in candidate_votes:
        votes = candidate_votes.get(candidate_name)
```
- `votes` - accessing/retrieving values with a new variable
- `candidate name` - dictoinary's key
- `candidate_votes` - dictionary

Both methods allow us to retrieve values from a dictionary based on their defined keys. There is a difference in syntax `[] brackets` vs `() parentheses` yet, the idea is the same. get() method looks up values in a dictionary, but unlike square brackets, get() returns "None" or a default value of your choice, if the key is not found. If you expect look-ups to sometimes fail, get() might be a better tool than normal square brackets look-ups because errors can crash your program where the get() is less likely to.

#### Determing the Election Winner
The following code determines a winner based on the highest total vote count. 

First, it is important to declare and initialize variables:
```python s=
winning_candidate = ""
winning_count = 0
winning_percentage = 0
```
Then, determine the winning vote count, winning percentage, and candidate:
```python s=
if (votes > winning_count) and (vote_percentage > winning_percentage):
    winning_count = votes
    winning_candidate = candidate_name
    winning_percentage = vote_percentage
```           

All values votes are then compared against each other by declaring a new variable `wining_count` which shows the total amount of votes for the determined victor. When the condition is  met and set to `True`, meaning the highest value is found, and the value is passed to the new variables `winning_count` `winning_candidate` ` winning_percentage`.

## Summary
Leveraging Python to manipulate larger data sets can be an effective way to draw insights from unstructured or slightly structured data. Python allows us to quickly sort and manipulate the data but also allows us to layer the code on top of exapnded datasets. With the manipulation of certain lines of code we can augment the study to include data from more counties and/or states etc. 

This code specifically accesses the dataset in a specific directory and writes a report to a specific file. The specific lines of code file_to_load = os.path.join("Resources","election_results.csv") and file_to_save = os.path.join("Analysis", "election_analysis.txt") can be easily fixed by renaming a directory and file in the code itself. This allows for significant flexibility in adding new datasets. 

Below I have included an output of the data generated in the terminal after running the PyPoll_Challenge code. 

<p align="center">
![Challenge 3 Ouput](https://user-images.githubusercontent.com/115036844/198426563-91d8f9f3-a181-4ef9-a3b1-cc7c390a9761.png)
</p>
