TW5-randVal
===========

a random value generator for use with tiddlywiki

This plugin contains a widget that generates a random number and stores it in a specified field. It is a modification of the action-setfield widget and acts identically with the exception of the value the field is set to.

This plugin also contains a javascript macro that acts similarly to the widget.

The macro will take the following inputs:<br>
lower - the lower bound of the random numbers generated, defaults to 1.
upper - the upper bound on the random numbers generated, defaults to 6.
step - the step size of the random numbers generated (that is all random numbers will be in the form rand = lowerBound+n*stepSize where n is an integer and lowerBound <= rand <= upperBound) stepSize defaults to 1 (so integer outputs). If stepSize > upperBound-lowerBound than the output will always be lowerBound
numrolls - the number of times to roll a random number and sum the results, defaults to 1 if no value is given.

The Widget takes these additional inputs:<br>
tiddler- the tiddler that will contain the random value
field - the field of the specified tiddler that will hold the random value.

!Widget example code:

```
<$button>
<$action-randval $tiddler=tiddlerName $field=fieldName $lower=lowerBound $upper=upperBound $step=stepSize $numrolls=numberOfRolls/>
Generate Random Value
</$button>
```

The code will put a random number in the field `fieldName` of the tiddler `tiddlerName`. The number will be the sum of numberOfRolls numbers between `lowerBound` and `upperBound` inclusive.

!Another example:

```
<$button>Roll Dice!
<$action-randval $field=fieldName/>
</$button>
```

When the button is pressed, the code will generate a random integer between 1 and 6 inclusive and store it in the field fieldName. So it is equivalent to rolling a normal 6 sided dice.

!How randVal is generated (pseudocode):

num_steps = (upperBound-lowerBound)/stepSize+1

output = 0

for i=1 to num_rolls

  n = floor(num_steps*random())
  
  output = output + lowerBound+n*stepSize
  
end

return output
  