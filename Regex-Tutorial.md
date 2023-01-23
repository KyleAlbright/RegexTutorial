# Regex Tutorial: Matching an Email

In this tutorial we will discuss the characteristics and usefulness of regular expressions or regex for short. Regular expressions are "a series of special characters that define a search pattern." By using this specified pattern, the regular expression engine matches the pattern of the input text. A pattern consists of character literals, operators, or constructs.

## Summary

In this tutorial, we will go over the regex expression to match email needed for verification. ``` `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` ```
Examples of this format could be something like FirstName.LastName@google.com, or myemail@yahoo.com etc etc. There are various components that comprise a regular expression that we will discuss below. 

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors

Anchors are tokens that do not match any characters in the string, but they do tell us something about the string. Anchors can tell us where the string or line begins (```^```) or ends (```$```) This is important because you may want to only match strings or digits at a certain point in the input. This will make your search more efficient, since it will only be searching within a certain point. Without a beginning and ending anchor, the matching process could take longer as the engine will spend time searching to find that pattern in other locations.


### Quantifiers

There are many different types of quantifiers( ```?, *, +``` ), but we will be discussing the curly-brace quantifier. These quantifiers will be be found within curly braces ```{}```, and give some parameters to your match. In our example at the top, our quantifiers are ```{2,6}```. This means that the match for the top-level-domain in the email verification, must be between 2 and 6 characters. (.com, .net, .org etc) Quantifiers can also be used to make sure a value is exactly a certain amount of characters. This is achieved by only having 1 digit in the curly braces. Ex: ```{5}```, would ensure that only matches would be found that have exactly 5 characters. You can also set a minimum match parameter by adding a comma after the digit. Ex: ```{5,}```, would ensure that all matches have to be at least 5 characters long. Quantifiers are found within a grouping. 


### Grouping Constructs

Grouping constructs can be found within "```()```" and are most often used to delineate sub-expressions within a regular expression. In our example at the top you can see we have three groupings. ```(myemail)```@```(yahoo)```.```(com)```  Within each of the parenthesis' parameters are set within in them to allow a certain type, or number of characters. This comes in handy when you are wanting to make sure that an email has a valid domain. Ex: ```myEmail12_34@yahoo.com``` - we are allowing numbers and some special characters in the username of the email, but after the period we do not. Without these groupings, we would not be able to apply these parameters to specific parts of the string we are trying to match.   


### Bracket Expressions

Bracket expressions are essentially a set of rules for a certain set of characters. Any individual character between the brackets will have to abide by the set parameters that are defined. So in the example at the top, the first set of brackets will allow lowercase characters a-z, numbers 0-9, and special characters (_ . -). In short, the bracket expressions notate a set of rules to follow.


### Character Classes

Character classes distinguish the different kinds of characters you wish to check for or match. These are the character classes used in our expression.

* ```[a-z0-9_\.-]``` - The notation here is telling us a few things. It is matching all lowercase letters (```a-z```), all numbers (```0-9```), and the special characters of an underscore, a period, and a dash (```_\.-```). As you notice there is a backslash in this last part of the expression. The reason for this is to escape what a period does on it's own in a regular expression. The period or dot in a regular expression will allow for any character. (This is not to be confused for a lack of a character. There must be a character there to match.) 
* ```[\da-z\.-]``` - The notation here is telling us to allow for any digit (```\d```). You may be asking yourself how is this any different than what we did previously with ```0-9```? In short, it's really not much different. ```0-9``` is searching for a range of numbers, while ```\d``` is matching any digit. ```\d``` is a shorthand for ```0-9```. It is more common to see the shorthand version, as it is more readable. The next part of this expression (```a-z\.-```) follows the rules previously discussed. It is matching all lowercase letters a-z, periods, and dashes. 

* ```[a-z\.]``` - This follows all the rules previously discussed as well. It is matching all lowercase letters a-z, and allows for a period. 

### The OR Operator

The "OR Operator" is represented by a vertical bar or pipe ```|```. We are not using one in our example, however we could use it if we wanted to only allow emails from a certain domain to be added. Say we worked at a company and had three vendors supplying us a product. We could use the OR operator to validate a form, and ensure that only email addresses from those specific companies where being used. It would look something like this.  ``` `/^([a-z0-9_\.-]+)@([company|buisness|industry]+)\.([a-z\.]{2,6})$/` ``` This would promise that we only get an email address that would match something like billybob@company.com, jennysue@buisness.net, or tommyjoe@industry.org. Any other input would not be permitted since we have only allowed the three domains specified. 

### Flags

Flags are added to the end of expressions that will effect the search. We are not using any in our example, but here are three of the most common flags. 

* ``` `i` ``` - By adding an "```i```" in our regular expression, we would be able to make our search or match less case sensitive. This is something we could add into our expression that could prove useful, since sometimes people like to add capital letters to their email address. We could allow for capital letters easily by just adding an i after the closing forward slash. This would look like this ``` `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/i` ```

* ``` `g` ``` - The "```g```" flag in an regular expression stands for Global. When used it can change the way that pattern matching works. Without this tag a the search would stop when it matched the first correct instance or occurrence. Say we needed to collect multiple emails in a form from a supervisor, and all employees working under them. We would want to add a "```g```" at the end of our expression like so. ``` `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/g` ``` It is worth mentioning that you can use flags in conjunction with each other. So adding "```i```" and "```g```" to our expression would make it both not-case-sensitive and global.  (``` `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/ig` ```)

* ``` `m` ``` - The "```m```" tag or "multiline" flag in a regular expression changes how the [anchors](#anchors) work in an expression. We can use the "```m```" tag at the end of our expression to search and match multiple lines. This helps to find our match even though the string may be split between multiple lines in an input. For example lets say that some one had a very long email address and it took up two lines of an input field.  

Example: 

" ```MyFirstName_MyMiddleName_MyLastName@```
                                                                                                                                  
```google.com``` "
 
 Our tag would ensure that we search and match both lines of this input. (``` `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/m` ```). 
 
 Again, we could also use this flag with the other ones discussed if we wanted to make sure we where able to use lower and upper case letters, search for multiple email matches, and on multiple lines. (``` `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/igm` ```)


### Character Escapes

We briefly talked about escapes when we where discussing our [character classes](#character-classes), but now we can go into more detail. Character escapes are a way to specify a special character that would otherwise have a different or special meaning. This is accomplished by adding a backslash "```\```" before the character. In our previous example we used this backslash to match a period. Without this backslash the "```.```" would search for a match of a single character. We also used a character escape to search for any digit using "```\d```". Character escapes are not isolated to Regular Expressions. They have been a native JavaScript property from the very beginning.  

## Author

Kyle Albright is an aspiring future software developer living in Austin Texas. 

* Follow me here at my [Github](https://github.com/kylealbright) 

* Add me on [LinkedIn](https://www.linkedin.com/in/kyle-albright-atx512/) 

* Email me at kyle_albright@hotmail.com
