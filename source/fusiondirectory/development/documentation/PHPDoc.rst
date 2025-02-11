Doxygen
=======

We are using a tool named doxygen which is fantastic to read documented code and offers a visual
reprensentation of the interaction of classes and methods.

If well documented, the visuals helps to quicker understand the codes.

How to document your code
-------------------------

**Within your methods**

You may comment your code inline above your line of code in order to make a clear message on what/why/how
your below code is performing.

**Above your methods**

We use PHPdoc to get an harmonious documentation withing the code.
It basically start like this :
/**
* Your comment here.
*/

Within that comment block we defined : variables and return types.
We mandate our developpers to use strict type and we enforce it in php 8.2+

On tope of your