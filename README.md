java c
CS152
Project 5: Simulating   Elephant   Population   Management
As   noted   in the lab, this   is the first   of a   two-part   project where we'll be simulating the elephant   population   in   Kruger National   Park, South Africa.
The carrying capacity of the   park   is approximately 7000 elephants (1   elephant   per   square   mile of park).   Previous efforts to   manage the population involved culling   approximately   400   animals per year. After the development of an   elephant contraceptive, the current effort to manage the   population   involves using a   contraceptive dart on adult female   elephants to   limit the   birth   rate.
The conceptual goal of this week's simulation is   twofold.
First,   identify differences   in the   population distributions between the two   methods of controlling   the   population.
Second,   identify the   percentage of adult females that   need to be darted with the   contraceptive   each year in order to maintain a   stable   population without   culling.
Following the overall design below, continue to develop   the   simulation   step   by   step   creating   one   function at a time and testing it with the   provided   “test”   scripts.   By   the   end   of the   project   you will      have a program which will allow you to test the   effect   of different   percentages   of darting   on the total elephant   population.   For this   project we will employ “trial and error” to   get   the   best   darting probability.   In the   next   project, we will utilize optimization to programmatically find the   optimum darting percentage.
Project Tasks   (1-9)
Task   1: Write a function to calculate which elephants survive a year
In the lab, you created the newElephant,      initPopulation   and   incrementAge   functions. The next function to create is   calcSurvival. The   calcSurvival   function   processes the elephant population and determines whether each   individual   elephant survives   to   the   next year.
The function takes the   parameter list and population   list as   arguments.   The   function   uses   the   parameters max age and the three survival   probabilities   (calf, adult, senior).
The function should loop over the existing   population   list and   add   each   elephant to   a   new   population list   if it survives, using the elephant's   age   to   determine   which   probability   to   use   to   determine survival.   It should   return the   new   population   list. To do this:
1.       Create a   new empty   list,   new_population.
2.       Loop over the existing population   list.   Use the   age of the   elephant   to   determine which   survival   probability applies, then use the appropriate survival   probability to   see   if the   elephant should   be added to the   new_population list.   Do this   by testing   if a   call to   random.random()   is less   than the survival probability.
3.      After the loop, return the   new_population   list.
4.       Test your function by downloading test_calcSurvival.py, reading the   code to   make   sure   you understand   it.   Read the comments to make sure   you   know what   output   to   expect.
Run   it, examine the output, and   make any necessary   changes   to   your   code.
Task 2: Write a function to randomly dart female   elephants
Write a function, dartElephants, that goes through the adult females and   randomly   selects   individuals for darting based on the comparison of random.random()   and   the   darting   probability   parameter.   Make sure that you generate a   new random   number for each   comparison.   The   function takes   in the   parameter list and the   population list   as   arguments.   It   returns the   updated   population list. The function makes use   of the   probability of darting,   the juvenile age,   and   the maximum age.
1.       The function should   loop over each elephant   in the   population   list.   Inside the   loop,   it
should test   if the elephant   is female and   is older than the juvenile age and   is   less than or   equal to the maximum   reproductive age.
2.       If the elephant   is an appropriate age, then   determine   if the   elephant   should   be   darted   by   testing   if a call to random.random()   is less than the   probability   of darting.
3.       If the animal should   be darted, set   its   pregnancy field to   0   and   set   the   months   of   contraceptive left field to   22.
4.      After the loop, return   the   population   list.
5.       Test your dartElephants   function to make sure some fraction of the   adult females   are   being   modified correctly. You   may use   test_dartElephants.py
Task 3: Write a function to cull elephants from the   population
Write a function, cullElephants, that checks if there   are   more   elephants than   the   carrying capacity.   If there are too   many elephants, the function should remove enough   randomly   chosen   elephants from the   population so there are as many   elephants   as the   carrying   capacity.   The   function takes   in the   parameter list and a   population list   as   arguments.   It   should   return   a   tuple   with the first element   being the   new   population list and second   element   being the   number   of elephants culled. The function makes use of the   carrying   capacity of the   population.
1.       Determine the   number of animals that   need to   be culled   (that   is the total   number   of   animals in the population   minus the   carrying   capacity).
2.       If there are too   many elephants, then randomly   shuffle   the   population   list   (use   random.shuffle()).   Use the appropriate list-slice to keep the first   carryingCapacity number of animals.
3.       Return the   tuple      like   this:
return   (newPopulation, numCulled)


4.       Use the    test_cullElephants.py file to test your   cullElephants   function.


Task 4: Write a function to manage how to control the population
Write a function, controlPopulation, that will determine whether the population should be darted or culled and call the appropriate function. It then returns the new population list and the number culled (which will be zero, if the elephants were darted) as a tuple.
The following is the structure of the controlPopulation function:def controlPopulation( parameters, population ):# if the parameter value for "percent darted" is zero:# call cullElephants, storing the return values in a twovariables#( e.g. newpop, numCulled = cullElephants( parameters,population ))# else# call dartElephants and store the result in a variablenamed newpop# set a variable named numCulled to zero# return (newpop, numCulled)
Test your controlPopulation function to make sure the list is being modified correctly.
This is just a repeat of the individual tests you did on cullElephants and dartElephants making sure that the logic of controlPopulation is working correctly. You may use test_controlPopulation.py


Task 5: Write a function to simulate   a   month
Note: This   is the   number one function that causes   problems for students, so think   carefully and methodically about your logic.   Using a   case   by   case   analysis   will   go   a   long   way   in combating the complexity of this task.Also, as a general   practice you should   NOT add or   remove   elements from   a   list   that   you      are   iterating over (Remember the   homework   program on   lists?) You should create a   new   population   list and add all elephants to   it AND add any   new   calves.


The function   simulateMonth   moves the simulation forward by one month.   It   modifies   only   the   adult females   in the   population, and   it adds a   new calf to the   population   if the female   has reached the end of her gestation.   In the other cases, the   function will   either   add   an   additional   month to the   number months   pregnant variable, or reduce   by one   the   number   of   months contraception remaining.
The function takes   in the   parameter list   and the   population list.   It   returns   a   new   population   list.   The function uses the calving   interval, juvenile age, and   maximum   age   parameters.
1.       Loop over the   population   list. The algorithm   inside the   loop   is given   below. After the   loop   is complete,   return the   population list.
2.       On a   month to   month   basis the   probability of a female elephant   (not already   pregnant   and   not on contraceptive)   becoming   pregnant   is   1.0 / (3.1*12 - 22) where   3.1   is the               calving   interval, and 22   is the length of gestation   in   months.

# make a new population listfor e in population:# assign to sex the IDXSex item in e# assign to age the IDXAge item in e# assign to monthsPregnant the IDXMonthsPregnant item in e# assign to monthsContraceptive the IDXMonthsContraceptiveRemaining item in e#if sex is female and the elephant is of breeding age# if monthsContraceptive is greater than zero#decrement the months of contraceptive left(IDXMonthsContraceptiveRemaining element of e) by 1# else if monthsPregnant is greater than zero# if monthsPregnant is greater than or equal to 22# create a new elephant of age 1 and append it to the population list# reset the months pregnant (the IDXMonthsPregnant element of e) to zero# else# increment the months pregnant (IDXMonthsPregnant element of e) by 1# else# if the elephant becomes pregnant# set months pregnant (IDXMonthsPregnant element of e) to 1


3.       Test your function using test_simulateMonth.py
Task 6:    Write a function to simulate   a year
The   simulateYear   function takes   in the   parameter list and   population list.   It calls
calcSurvival, then   it calls incrementAge, then it   loops twelve times   calling
simulateMonth.   Finally,   it   returns the   population   list. When calling each of the   helper   functions,   pass   in the   population list and assign the result   of the function   back   to   the   population   list.
For example:
population = calc   Survival   ( parameters, population   )
Test your function using test_simulateYear.py   It will ensure that the   basic functionality   is   present. We will test   it   more thoroughly once   more functions have been written.
Task 7: Write a function to calculate statistics on the   simulation
The calcResults   function calculates how many   calves, juveniles, adult   males,   adult females,      and seniors are   in the   population.   It then   returns a list with those   values   in   it,   along   with   the   total   number in the   population, and the   number culled from the   population   that year.   It   takes   as   input      the parameters, the population list, and   the   number   of animals   that   were just culled   from   the population.
1.       Get the juvenile age and   max age   parameters.   Initialize variables to   hold the   number of   calves, juveniles, adult males, adult females, and seniors.
2.       Then loop over the population list.   For   each   elephant,   increment   the   appropriate   variable   (use if statements to figure out the category for each   elephant).
3.      When the loop   is complete,   return a lis代 写Project 5: Simulating Elephant Population ManagementPython
代做程序编程语言t with   the following   items:   the   total   population   size,   the number of calves, the number of   juveniles, the   number of adult   males,   the   number   of   adult females, the number of seniors, and the number of   animals   culled.
4.       Test your function using test_calcResults.py.
Task 8:   Run a   simulation
The runSimulation function takes one parameter–the   parameter list.   Then   it   creates   the new   population, applies any control procedures (e.g.   darts   them),   loops   over N   years,   simulating   the year, and   it   keeps track of the demographics for each year by   appending   them   to   a   list.   Use      the following code as a template and add the function   to   your   elephant.py script.
Note: you   may   need to add a   parameter to your parameter list   (and   indexes)   that   specifies   the   number of years to run the simulation. The default   number of years to   simulate   is   200.   Use
IDXNumYears for the index.

def runSimulation(parameters):

popsize = parameters[IDXCarryingCap]# init the populationpopulation = initPopulation( parameters )[population,numCulled] = controlPopulation( parameters,population )# run the simulation for N years, storing the resultsresults = []for i in range(parameters[IDXNumYears]):population = simulateYear( parameters, population )[population,numCulled] = controlPopulation( parameters,population )results.append( calcResults( parameters, population,numCulled ) )if results[i][0] > 2 * popsize or results[i][0] == 0 :# cancel early, out of controlprint( 'Terminating early' )breakreturn results
Task 9: Write your main functionSetup your main   function and conditional statement   to run elephant.   main(argv) should   take   argv   as an argument and the call to   main should   pass   in   sys.argv.   The   only   command   line         argument you will   need   is the darting   probability so the command line will   look   like   this:
%python3 elephant.py   .5
The first   part of your main   function should be a usage statement which   stops   program
execution   if there are less than two command line   arguments.   Next,   cast   and   assign the   darting   probability from the command line parameter   float(argv[1]).
Next, set   up the   rest of the   parameters and   make the   parameter list just as you did   in   the   test            function.   Next, call runSimulation once and store the   return value   in   a   list.   Make   sure   you   include the probDart parameter based on the command   line   argument.
Test your function and   print out the   last   item   in the   results   list. You   may want to edit   your
runSimulation   function so it prints out the total   population value   each   year   of the   simulation   as a   sanity   check.
Finish your main function by calculating the average results   (average total   population,   average   number of calves, average number of   juveniles, and so   on).   Print   out those   results   nicely   at   the         end of your main function.
Required   Element   1: Screenshot of console output of your program displaying the   current   darting probability and the results   that were   generated.
Follow-up Questions
1.       What   is the difference   between a tuple and   a   list?
2.      What are the benefits of using a   naming   scheme   like   IDXNumYears   instead   of   just   using an   index   number?
3.       Discuss where errors might impact the   simulation?   How   would   you   ensure   the   final   simulation model would produce reliable   results to support well-informed   wildlife
conservation decisions about this elephant population?
Extensions:   Extensions are your opportunity to customize your project,   learn
something else of interest to you,   and improve your   grade.   The   following   are   some suggested extensions, but you are free to choose your   own.   Be   sure   to   describe   any   extensions you complete in your   report.
1.       Run simulations and compare results.   Run   simulations   that   use   the   culling
population-control strategy (set the darted probability   parameter to   0.0).   Determine   how   the   population demographics are different   in this scenario compared to   using   contraception.   Describe those differences. What are the average numbers   of calves,   juveniles, adult males, adult females, and seniors? Where   are the   most   obvious   differences   in demographics between the two groups (think   like   a   tourist).   Does   the   percent to be darted   change with different   carrying   capacities?
2.       How sensitive   is the system to changes   in various variables?   For   example,   modify   the      calf survival   rate to 80% or up to 90%   and   see   how that   modifies   the   culling   rate   or the   percent darted   rate.
3.       Use your   stats.py   file from   Project 3 to compute the average   values   of   each
demographic. The list of results that you accrue when   running   multiple   simulations   can   be thought of as the contents of a spreadsheet.   Each   list   is a   row,   and   each   element   in   the list   belongs   in a column. The first column   is for the   total   population,   the   second
column   is for the count of the calf population, etc. You   may want to   add   a function   that   rearranges data from lists of rows to   lists of columns,   then   you will   be   able   to   use   your   existing functions   in   stats.py   to compute the average value of a given column.
4.      Write the   population data to a CSV file and generate   plots   of total   population--or   demographic subsets--under different scenarios.
5.       Expand on the number of command   line arguments   that   your   program   can   accept.
Write your project   report
Please   read the grading   rubric so that you   know exactly what criteria your code   and   report will   be evaluated   upon.   If you   have any questions, ask!
Reports are   not   included   in the compressed code archive file!   Please don’t   make   the graders hunt for your   report.
You can write your report   in   any word   processor you like   and   submit   a   PDF   document   in   the Google Classroom assignment folder. Or use   a   Google   Document   format.
Review the Writeup Guidelines document in the   Labs and   Projects   folder.
Your intended audience for your report is your   peers who   are   not   taking   CS   classes.
From week to week, you can assume your audience has   read your   prior   reports.   Your   goal should be to explain to peers what   you   accomplished   in   the   project   and   to   give
them a sense of how you did   it. The following   is   a   list   and   description   of the   mandatory   sections you   must   include   in your report.   Do   not   include the descriptions   in your report,      but use them as   a guide   in   writing   your   report.
●         Abstract
A summary of the   project,   in your own words. This should be   no   more than   a few   sentences. Give the reader context and   identify the   key   purpose   of the assignment. An abstract should define the project's   key lecture   concepts   in   your         own words for a general, non-CS audience.   It should also   describe   the   program's   context and output, highlighting a couple of   important   algorithmic   and/or   scientific   details. Writing an effective abstract is an   important   skill.   Consider the following   questions while writing it.
○       Does   it describe the   CS   concepts   of the   project   (e.g. writing   well-organized and efficient code)?
○       Does it describe   the   specific   project   application   (e.g.   generating   data)?
○       Does   it describe your solution   and   how   it was   developed   (e.g. what   code   did you write)?
○       Does   it describe the   results   or outputs   (e.g.   did   your   code work   as   expected and what did the   results tell you)?
○         Is   it concise?
○       Are all   of the terms well-defined?
○       Does   it   read   logically   and   in   the   proper   order?
●         Methods
The   method section should describe in clear sentences   (without   pasting   any
code) at least one example of   your own computational   thinking   that   helped   you   complete your project. This could involve   illustrating   how a   key   lecture   concept   was applied to creating an image,   how you solved   a   challenging   problem,   or explaining an algorithmic feature that is essential to your   program   as well   as why   it   is so essential. The explanation should be   suitable for   a   general   audience who      does   not   know   Python.
●         Results
Present your results   in a clear manner using   human-friendly   images   or   graphs labeled with captions   and interpreted for a general audience   such   as   your   peers   not   in the course.   Explain, for a general, non-CS audience, what your   output means and whether it   makes sense.
●       Reflection   and   Follow-up   questions
Draw connections between lecture concepts   utilized   in this   project   and real-world   problems that   interest you.   How else could these concepts apply to our everyday lives? What are some specific things you   had   to   learn   or   discover   in   order to complete the project?   Look for a set of short   answer questions   in   this section of the report template.
●       Extensions   (Required   even   if you did   not   do   any)A description of any extensions you   undertook, including   text   output   or   images   demonstrating those extensions.   If you added any modules, functions, or other   design components, note their structure and the algorithms you   used.
●       References/Acknowledgements    (Required even   if there   are   none)
Identify your collaborators,   including TAs and   professors.   Include   in that list   anyone whose code you may have seen, such   as   those   of friends who   have   taken the course   in a previous semester. Cite   any   other   sources,   imported            libraries, or tutorials you used to complete   the   project.
Submit your Code
Turn   in your code   by zipping the file and uploading   it to   Google   Classroom   assignment folder.   When submitting your code, double check the following.
1.       Is your name   at   the   top   of   each   Python   file?
2.       Does every function   have a docstring (‘’’ ‘’’)   specifying   what   it   does?
3.       Have you checked to   make sure you   have   included all   required   elements   and   outputs   in   your project   report?
4.       If you   have done an extension,   have you   included this   information   in your   report   under      the   Extension   heading?   Even   if you   have   not done any extensions,   include a section   in   your report where you   state   this.
5.       Have you acknowledged any help you   may   have   received from   classmates,   your
instructor, the TAs, or outside sources (internet,   books, videos,   etc.)?   If you   received   no   help at all,   have you   indicated that under the Sources   heading   of the   report?
   



         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
