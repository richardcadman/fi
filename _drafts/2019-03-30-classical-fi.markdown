---
layout: post
title:  "Classical FI"
date:   2019-03-30 15:10:18 +0100
categories: maths
---

## The classical approach to financial independence

Mr Money Mustache (MMM) popularised the ["shockingly simple maths behind retirement"](http://www.mrmoneymustache.com/2012/01/13/the-shockingly-simple-math-behind-early-retirement/) back in 2012, and it's generally seen as the 'classical' way to become financial independent (FI).

To quickly recap, financial independence, is a state where you have enough wealth to live on, or assets generating enough income, such that you don’t need to work a “normal job” anymore.

As long as you're investing your savings, and getting a decent `interest rate`, they'll grow and eventually generate enough returns that you can live off the returns alone. At that point you're financially independent and can stop working if you want.

The percentage you withdraw every year should be slightly less than the interest you're earning, known as a `safe withdrawal rate (SWR)`, that way the money shouldn't run out, and you've got a little margin for poor performing years.

## Savings rate is key, not the absolute numbers

MMM explains that the absolute numbers (how much you earn, and how much you save) aren't as as important as your `savings rate` which `= amount you save / amount you earn after tax`.

To illustrate why, here are the two extremes:
- **Save 0%, and spend 100% of your income**, you'll never save a penny, and you'll have to bank on the state pension at 60something (or more likely 70something) when you eventually retire
- **Save 100%, and spend 0% of your income** (i.e. live for free) and you could stop working and retire now (assuming you can maintain this lack of spend if you stopped working)

If your savings rate is somewhere in the middle, you'll become financially independent somewhere in the middle too. Here's a chart that shows a little more - _years to FI vs savings rate_.

## Years to FI vs Savings Rate

<iframe width="746.3611859838275" height="461.5" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vRvEiL3wkLkXr_K55ur9ORXZepSQA8Fs0Dw2ZqwgDxwRbgj0UHyXDQ7AmoduBsILNpdPggXj9wFiW43/pubchart?oid=313112970&amp;format=interactive"></iframe>

## A higher savings rate accelerates the time to FI

The beauty of having a higher savings rate is that you're not only _saving more money, faster_ but you're also _spending less_, and need less money overall to retire. These two things have a compounding effect, and can rapidly accelerate financial independence. That's why the graph isn't linear, it's exponential.

## How does the maths work?

I've dug into this to understand more.

We want to work out for different savings rates, how long will it take to become financially independent (FI)? Let's call this time period "n".

Financially independent means your expenses are covered by the safe amount you can withdraw from your "futureSavings". So we're going to write an equation that helps us to find 'n' when the futureSavings have grown big enough to support a withdrawal rate of 3% that covers your expenses.

#### There are six key variables

```
startingPot: £X,000
interestRate: 3.5%
withdrawalRate: 3%
annualIncome: variable
savingsRate: variable
futureSavings: variable
```

#### Equation 1: your future expenses

```
FIExpenses  = withdrawalRate * futureSavings
```

We'll assume you'll spend the same in retirement as you will now. So FIExpenses = currentExpenses

```
currentExpenses = withdrawalRate * futureSavings
```

Our current expenses are _also_ a function of our savings rate:

```
currentExpenses = (1 - savingsRate) * annualIncome
```

#### Equation 2: your future savings

After n years, your savings will be a combination of the pot of money you started with, and the money you saved along the way (a function of your savings rate). Both of these will be growing with a particular interest rate.

```
futureSavings after n years = [Starting pot after n years] + [Ongoing monthly payments after n years]
```

We can calculate how the starting pot will grow, using a compound interest calculation. We'll call this `futureSavings A`.

The ongoing payments are a little tricker (a future value series, see the reference below. We'll call this one `futureSavingsB`.

Here are those equations:

```
futureSavings = futureSavingsA + futureSavingsB

futureSavingsA = startingPot * (1+interestRate)^n
(this is just compound interest)

futureSavingsB = (annualIncome * savingsRate) * ((1+interestRate)^n - 1) / interestRate
(this is a future value series, see reference below)
```

#### Combine the two equations and rearrange

We take these, combine with the expenses formulas for earlier, and rearrange to remove `FutureValue` and `CurrentExpenses`.

```
Equation 1) currentExpenses = futureSavings * SWR%
Equation 2) currentExpenses / withdrawalRate = [startingPot * (1+interestRate)^n] + [(annualIncome * savingsRate) * ((1+interestRate)^n - 1) / interestRate]
Combined Equations) ((1 - savingsRate) * annualIncome)) / withdrawalRate = [startingPot * (1+interestRate)^n] + [(annualIncome * savingsRate) * ((1+interestRate)^n - 1) / interestRate]
```

We do some fairly heavy rearranging, using logs.

#### An equation to find 'n' (years to FI) based on savings rate

```
n = (ln((annualIncome * (interestRate * (-savingsRate) + interestRate + savingsRate * withdrawalRate)) / (withdrawalRate * (annualIncome * savingsRate + initialValue * interestRate)))) / (ln(interestRate + 1))

^^NOTE: this uses logarithms
```

And that's what you pop into Excel to generate the chart above.

References:
- [Safe withdrawal rates for the UK](https://retirementresearcher.com/4-rule-work-around-world/)
- [Future value of an annuity](http://financeformulas.net/Future_Value_of_Annuity.html)
- [Natural logarithm](https://en.wikipedia.org/wiki/Natural_logarithm)
