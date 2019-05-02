# How to solve problem

## Introduction

Solving problem is of the most importan skills you can learn and imporving as a person solver is a lifelong challenge.



We will study how to approach more complicated problems in particular problems.



The goal by looking to particular problems is not just solve thar particular problems, but to draw some general lesson about how we can get better to solve problem in general.

## Days Between Dates

#### The first thing to solve a problem is making sure we understand the problem.

We are talking about computional problem, they have in common is that they have inputs and desired outputs.This is usually an infinite set for most problems and the relationships between those inputs and outputs.

So, that mean a solution to a problem is a procedure that can take any inputs in that set and produces outputs, and that output is satisfies the relationship.

>Rules:
>
>0.Don't panic.
>
>1.what are the inputs.
>
>2.what are the output
>
>3.solve the problem

``````python
'''
Days Between Dates
This lesson will focus on one problem: calculating the number of days between two dates.
s
This workspace is yours to use in whatever way is helpful. You might want to keep it open in a second tab as you go through the videos.

inputs: 1. two dates
						the second date not be before the first date(check)
        2. how are inputs represented?
        
outputs:1. return a number giving the number of days between the first date and the second day.

do next:
	 1.we'll do some example to understand the relationship
	 2.Trying through a few case in a very systematic way in human.And trying a difficult case that covers many of things we would need to think about in an algorithm.
   
   
   2.1 2013.1.24 - 2013.6.29
     1.24 - 1.31 = 7
    + Feb = 28
    + Mar = 31
    + April = 30
  	+ May = 31
  	+ Jun 1-29 = 29
    = 156
   2.2 
     days = the number of days in current month minus the day we're starting on
     month1 += 1
     while month1 < target month:
         days += # of days in month1
         month1 += 1
     days += day2 # The month we arrived at
     while year1 < year2:
     			days += days in year1
   2.3 should we implement this algorithm?
			No.we should try to find simple way.Because this algorithm it doesn't handle lots of cases.
      1)initail days are in the same month.
      2)month2 is before month1
      3)days in leap years
   
'''
day_list = [31, 28, 31, 30, 31, 30, 31, 30, 31, 30, 31, 30]

def get_days(y, m, d):
    
    yd1 = y * 365
    md1 = 0
    for i in range(1, m+1):
        md1 += day_list[i-1]
    total1 = yd1 + md1 + d
    return total1

def daysBetweenDates(year1, month1, day1, year2, month2, day2):
    """
    Calculates the number of days between two dates.
    """
    
    # TODO - by the end of this lesson you will have
    #  completed this function. You do not need to complete
    #  it yet though! 
    total1 = get_days(year1, month1, day1)
    total2 = get_days(year2, month2, day2)
    result = total2 - total1
    print(total2)
    print(total1)
    return result

def testDaysBetweenDates():
    
    # test same day
    assert(daysBetweenDates(2017, 12, 30,
                              2017, 12, 30) == 0)
    # test adjacent days
    assert(daysBetweenDates(2017, 12, 30, 
                              2017, 12, 31) == 1)
    # test new year
    assert(daysBetweenDates(2017, 12, 30, 
                              2018, 1,  1)  == 2)

    # test full year difference
    print(daysBetweenDates(2012, 6, 29,
                              2013, 6, 29))
    assert(daysBetweenDates(2012, 6, 29,
                              2013, 6, 29)  == 365)
    
    print("Congratulations! Your daysBetweenDates")
    print("function is working correctly!")
    
testDaysBetweenDates()
``````

