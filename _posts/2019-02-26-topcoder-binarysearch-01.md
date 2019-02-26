---
title: "BinarySearch 'Auto Loan' Algorithm"
date: 2019-02-26
layout:
tags: topcoder
---


## Problem
A typical auto loan is calculated using a fixed interest rate, and is set up so that you make the same monthly payment for a set period of time in order to fully pay off the valance.
The balance of your loan starts out as the sticker price of the car. Each month, the monthly interest is added to your balance, and the amount of your payment is subtracted from your balance.
The monthly interest rate is 1/12 of the yearly interest rate. Thus, if your annual percentage rate is 12%, then 1% of the remaining balance would be charged as interest each month.

An salesman said about how you can have the car you are looking at for a payment of only *monthlyPayment* for only *loanTerm* months!
You are to return a *double* indicating the annual percentage rate of the loan, assuming that the initial balance of the loan is *price*.

- price : 1 ~ 1000000
- monthlyPayment : 0 ~ price/2
- loanTerm : 1 ~ 600
- returns : 0 ~ 100


## Solution
