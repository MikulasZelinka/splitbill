SplitBill
=========

Simple script for calculating the minimum number of payments needed to settle
all debts among a group of people.

Example
-------

Imagine five friends who have taken part in a puzzle hunt. Honza paid the fee,
Adéla bought stuff to make sandwiches (for four of them, as Tomáš took his own
food), Martin bought group train ticket for himself, Adéla and Tomáš and
separate one for Karel, who has discount card. Tomáš got the map for the whole
team. Then in pub at the finish line Karel paid for Martin's kofola, as he
couldn't find his wallet at the moment. Adéla bought the train ticket back for
four, Karel got his own. Now they are luckily back, relaxing and trying to
figure out how to make everyone get the money they should get in possibly the
easiest way.

Let's write all the expenses in `hunt.csv` file:

```
Name,What,Amount,Currency,For
Honza,fee,500,CZK,All
Adéla,sandwiches,105,CZK,AllBut Tomáš
Martin,group train ticket,375,CZK,Martin Adéla Tomáš
Martin,train ticket,95,CZK,Karel
Tomáš,map,79,CZK,All
Karel,kofola,25,CZK,Martin
Adéla,group train ticket back,490,CZK,AllBut Karel
Karel,train ticket back,95,CZK,Karel
```

Now let's run `splitbill.py` script with the above input:

```
$ python3 splitbill.py -p 'Adéla,Karel,Martin,Honza,Tomáš' -c CZK hunt.csv
```

The script outputs the transactions our friends should perform to be even:

```
     Who  ToWhom  HowMuch
0  Tomáš   Honza   284.30
1  Karel   Adéla   212.05
2  Adéla  Martin     6.60
3  Honza  Martin    48.85
```

Command line options
--------------------

`-c, --currency`: Currency in which the debts will be settled (default CZK)
`-x, --exchange-rates`: Exchange rates in the form 'USD:20,EUR:27.09'
`-p, --people`: Required, list of all the people involved, for example
    `'Adam,David'`. Spaces in names are not allowed.
`-d, --decimal_places`: Number of decimal places to which amounts should be
    rounded. Default 2.
