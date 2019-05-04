# How to solve problem

## Introduction

Solving problem is one of the most important skills you can learn and imporving as a person solver is a lifelong challenge.



We will study how to approach more complicated problems in particular problems.



The goal by looking to particular problems is not just solve that particular problems, but draw some general lesson about how we can get better to solve problem in general.

## Days Between Dates

### The Problem introduction

This lesson will focus on one problem: calculating the number of days between two dates.

### The first thing to solve a problem is making sure we understand the problem.

We are talking about computional problem, they have in common is that they have inputs and desired outputs.This is usually an infinite set for most problems and the relationships between those inputs and outputs.

So, that mean a solution to a problem is a procedure that can take any inputs in that set and produces outputs, and that output is satisfies the relationship.

### The Rules

>0.Don't panic.
>
>1.what are the inputs.
>
>2.what are the output
>
>3.understand the relationship between inputs and outputs.
>
>4.simple machanical solution

### The inputs

1. two dates
2. the second date is not before the first
3. how are inputs represented ?

### The outputs

1. return a number, giving the number of days between the first date and the second day.

### Do next

1. we'll do some excemple to understand the relationship.
2. Trying through a few case in a very systematic way in human.
3. Trying a difficult case that covers many of things we would need to think about in an algorithm.

``````
# In this case using human way to solve this problem, 
  2013.1.24 - 2013.6.29
     1.24 - 1.31 = 7
    + Feb = 28
    + Mar = 31
    + April = 30
  	+ May = 31
  	+ Jun 1-29 = 29
    = 156

# Concluding a algorithm
days = the number of days in current month minus the day we're starting on
     month1 += 1
     while month1 < target month:
         days += # of days in month1
         month1 += 1
     days += day2 # The month we arrived at
     while year1 < year2:
     			days += days in year1
``````

### Should we implement this algorithm? 

No, we should try to find simple way.Because this algorithm it doesn't handle lots of cases.

1. initail days are in the same month.
2. month2 is before month1
3. days in leap years

### 'Brain-dead' solution

``````
days = 0
while day1 is before day2:
	date1 = day after date1
	days += 1
return days
``````

### Write first

Defining nextDay funtion to get the next for simple case.

&nbsp;

Key point: Writing small bits of code test them and to know what they do.

``````python
###
### Define a simple nextDay procedure, that assumes
### every month has 30 days.
###
### For example:
###    nextDay(1999, 12, 30) => (2000, 1, 1)
###    nextDay(2013, 1, 30) => (2013, 2, 1)
###    nextDay(2012, 12, 30) => (2013, 1, 1)  (even though December really has 31 days)
###

def nextDay(year, month, day):
    """Simple version: assume every month has 30 days"""
    if day < 30:
        return year, month, day + 1
    else:
        if month == 12:
            return year + 1, 1, 1
        else:
            return year, month + 1, 1
``````

### Do next

Writing a procedure daysBetweenDates for giving approximate answers with our nextDay procedure.

``````python
def nextDay(year, month, day):
    """Simple version: assume every month has 30 days"""
    if day < 30:
        return year, month, day + 1
    else:
        if month == 12:
            return year + 1, 1, 1
        else:
            return year, month + 1, 1
        
def daysBetweenDates(year1, month1, day1, year2, month2, day2):
    """Returns the number of days between year1/month1/day1
       and year2/month2/day2. Assumes inputs are valid dates
       in Gregorian calendar, and the first date is not after
       the second."""
    a = (year2, month2, day2)
    days = 1
    while nextDay(year1, month1, day1) < a:
        days += 1
        year1, month1, day1 = nextDay(year1, month1, day1)
    return days
    
def test():
    test_cases = [((2012,9,30,2012,10,30),30), 
                  ((2012,1,1,2013,1,1),360),
                  ((2012,9,1,2012,9,4),3)]
    for (args, answer) in test_cases:
        result = daysBetweenDates(*args)
        if result != answer:
            print "Test with data:", args, "failed"
        else:
            print "Test case passed!"
test()
``````

### Solution in Three Parts

1) **Step One Pseudocode** 

``````python
days = 0
while day1 is before day2:
	date1 = day after date1
	days += 1
return days
``````

2) **Step Two Helper Function**

``````python
def datesIsBefore(year1, month1, day1, year2, month2, day2):
  	if year1 < year2:
      return True
    else:
      if month1 < month2:
        return True
      if month1 == month2:
        return day1 < day2
   	return False
``````

3) **Step Three daysBetweenDates**

``````python
def daysBetweenDates(year1, month1, day1, year2, month2, day2):
    """
    Calculates the number of days between two dates.
    """
    resultDays = 0
    while isBeforeDate(year1, month1, day1, year2, month2, day2):
        resultDays += 1
        year1, month1, day1 = nextDay(year1, month1, day1)
    return resultDays
``````

### Add assertion

We should raise a exception when input a invalid date

``````python
def datesIsBefore(year1, month1, day1, year2, month2, day2):
    assert not dateIsBefore(year2, month2, day2, year1, month1, day1)
  	if year1 < year2:
      return True
    else:
      if month1 < month2:
        return True
      if month1 == month2:
        return day1 < day2
   	return False
``````

### Real World Problem

One of the good ways about solving the problem.This way is getting close to an answer without dealing with all that complexity.But we’ve gotta deal with it at some point.Now we're gotta deal with how many days there actually are in a month.



The most efective way to finish the problem:

1. Write stub daysInMonth that always return 30.
2. Modify nextDays to use daysInMonth.
3. Test nextDays using stub daysInMonth.
4. Modify daysInMonth to be correct except for leap years.
5. Test daysInMonth using stub daysInMonth.
6. Write isLeapYear
7. Test isLeapYear
8. test daysBetweenDates for all test cases.



``````python
# Step 1:
def daysInMonth(year, month):
    return 30
#############################################################

def datesIsBefore(year1, month1, day1, year2, month2, day2):
    if year1 < year2:
        return True
    else:
        if month1 < month2:
            return True
        if month1 == month2:
            return day1 < day2
    return False



def nextDay(year, month, day):
    """Simple version: assume every month has 30 days"""
    if day < daysInMonth(year, month): # Step 2
        return year, month, day + 1
    else:
        if month == 12:
            return year + 1, 1, 1
        else:
            return year, month + 1, 1


def daysBetweenDates(year1, month1, day1, year2, month2, day2):
    """Returns the number of days between year1/month1/day1
       and year2/month2/day2. Assumes inputs are valid dates
       in Gregorian calendar, and the first date is not after
       the second."""
    assert not datesIsBefore(year2, month2, day2, year1, month1, day1)
    days = 0
    while datesIsBefore(year1, month1, day1, year2, month2, day2):
        year1, month1, day1 = nextDay(year1, month1, day1)
        days += 1
    return days

# Step 3:
def t():
    assert daysBetweenDates(2013, 1, 1, 2013, 1, 1) == 0
    assert daysBetweenDates(2013, 1, 1, 2013, 1, 2) == 1
    assert daysBetweenDates(2013, 1, 1, 2014, 1, 1) == 360
    assert nextDay(2013, 1, 1) == (2013, 1, 2)
    # assert nextDay(2013, 4, 1) == (2013, 2, 2)
    assert nextDay(2012, 12, 30) == (2013, 1, 1)
    print("Test Finished!")
#############################################################
t()
``````



``````python
# Step 4:

day_list = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]

def daysInMonth(year, month):
    if day < day_list[month - 1]:
        return year, month, day + 1
    else:
        if month == 12:
            return year + 1, 1, 1
        else:
            return year, month + 1, 1
#############################################################

def datesIsBefore(year1, month1, day1, year2, month2, day2):
    if year1 < year2:
        return True
    else:
        if month1 < month2:
            return True
        if month1 == month2:
            return day1 < day2
    return False



def nextDay(year, month, day):
    """Simple version: assume every month has 30 days"""
    if day < daysInMonth(year, month):
        return year, month, day + 1
    else:
        if month == 12:
            return year + 1, 1, 1
        else:
            return year, month + 1, 1


def daysBetweenDates(year1, month1, day1, year2, month2, day2):
    """Returns the number of days between year1/month1/day1
       and year2/month2/day2. Assumes inputs are valid dates
       in Gregorian calendar, and the first date is not after
       the second."""
    assert not datesIsBefore(year2, month2, day2, year1, month1, day1)
    days = 0
    while datesIsBefore(year1, month1, day1, year2, month2, day2):
        year1, month1, day1 = nextDay(year1, month1, day1)
        days += 1
    return days

# Step 5:
def t():
    assert daysBetweenDates(2013, 1, 1, 2014, 1, 1) == 365
    assert nextDay(2012, 12, 31) == (2013, 1, 1)
    print("Test Finished!")
#############################################################
t()
``````



``````python
# Step 6:
def isLeapYear(year):
    if year % 400 == 0:
        return True
    if year % 100 == 0:
        return False
    if year % 4 == 0:
        return True
    return False

# Step 7:
def t():
    assert isLeapYear(2013) == False
    assert isLeapYear(2012) == True
``````



``````python
# All
def isLeapYear(year):
    if year % 400 == 0:
        return True
    if year % 100 == 0:
        return False
    if year % 4 == 0:
        return True
    return False


def datesIsBefore(year1, month1, day1, year2, month2, day2):
    if year1 < year2:
        return True
    else:
        if month1 < month2:
            return True
        if month1 == month2:
            return day1 < day2
    return False

dayList = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]

def daysInMonth(year, month):
    if isLeapYear(year) and month == 2:
        return 29
    return dayList[month-1]

def nextDay(year, month, day):
    """Simple version: assume every month has 30 days"""
    if day < daysInMonth(year, month):
        return year, month, day + 1
    else:
        if month == 12:
            return year + 1, 1, 1
        else:
            return year, month + 1, 1


def daysBetweenDates(year1, month1, day1, year2, month2, day2):
    """Returns the number of days between year1/month1/day1
       and year2/month2/day2. Assumes inputs are valid dates
       in Gregorian calendar, and the first date is not after
       the second."""
    assert not datesIsBefore(year2, month2, day2, year1, month1, day1)
    days = 0
    while datesIsBefore(year1, month1, day1, year2, month2, day2):
        year1, month1, day1 = nextDay(year1, month1, day1)
        days += 1
    return days


def test():
    assert daysBetweenDates(2013, 1, 1, 2013, 1, 1) == 0
    assert daysBetweenDates(2013, 1, 1, 2013, 1, 2) == 1
    assert daysBetweenDates(2013, 1, 1, 2014, 1, 1) == 365
    assert nextDay(2013, 1, 1) == (2013, 1, 2)
    # assert nextDay(2013, 4, 1) == (2013, 2, 2)
    assert nextDay(2012, 12, 31) == (2013, 1, 1)
    assert nextDay(2012, 8, 30) == (2012, 8, 31)
    assert daysBetweenDates(2012, 1, 1, 2013, 1, 1) == 366
    assert daysBetweenDates(2012, 2, 13, 2012, 3, 1) == 17
    assert daysBetweenDates(2012, 2, 13, 2012, 3, 1) == 16
    print("Test Finished!")

test()
s
``````





### My current solution before study this lesson

``````python
'''
Before study this lesson, I solve this problem by this way.
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

