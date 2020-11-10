---
layout: post
title:      "Algorithms & (allieviating) your blues!"
date:       2020-11-09 09:55:20 -0500
permalink:  algorithms_and_allieviating_your_blues
---


Today I want to write about some new concepts I've been learning. I thought writing a blog post about it might help solidify my understanding of the subject as well as maybe help anyone else who is daunted by the very word itself.... **ALGORITHM**

<iframe src="https://giphy.com/embed/5dYeglPmPC5lL7xYhs" width="480" height="200" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/uafairbanks-math-algorithms-you-cant-handle-5dYeglPmPC5lL7xYhs">via GIPHY</a></p>

I've got an interview coming up this week and everywhere I look I'm being advised that they might ask me about algorithms. Having, before these past couple of weeks,  never considered algorithms, I was a bit nervous. Just hearing the word gave me a serious case of [imposter syndrome](https://hbr.org/2008/05/overcoming-imposter-syndrome#:~:text=Imposter%20syndrome%20can%20be%20defined,external%20proof%20of%20their%20competence.). However, if you take the time to calm down and look at them, you'll realise they're not so bad and are usually just a complicated way of explaining methods and functions you've been using since your very first days as a developer. So lets jump in. 

A quick note before we do. This is going to be a series, where I will write about one algorithm per post, so keep an eye out for more in the near future!

**Sorting Algoritms**

So there are a few things to conisder before you want to tackle algorithms. Firstly take a look at [Big O Approximation ](https://en.wikipedia.org/wiki/Big_O_notation)(tl;dr It is essentially the cost of running an algorithm), another thing that is helpful is having a good understanding of  [recursion in Javascript](https://javascript.info/recursion) (tl;dr Where a function calls on itself).

If you're familiar with programming languages like Javascript or Ruby etc. you will have probably come across a very helpful function called ``.sort()``. This function will take an array of elements and return it sorted  from lowest to highest. Check out this example below to get a better idea of what I mean:

``` 
let array = [1, 4, 5, 2, 17, 12]
array.sort()
=> [1, 2, 4, 5, 12, 17]
```

Neat right! But how is it actually sorting the array. When it comes to figuring out algorithms, I find it very helpful to try and think how I would go about sorting the array. Try and put these thoughts into words, and then try and translate that into code. So lets have a go.

1.  To try and order from lowest to highest I would first try and find the lowest element of the array.
2. I would then take this element and write it down.
3. I would then go back to the array, cross out the element I had removed and then find the next lowest and repeat the process until I had crossed out all the elements in the array and written a new list in order of lowest to highest.

Sounds simple enough right? How would we go about translating this into code? A good place to start is to look at each step of your thought process and go from there. I am going to be writing this in Javascript.

First we'll start by creating a new array to store the elements as we remove them:

``` let sorted = [ ] ```

 Okay now that done we have to take a look at our array:
 
 ```let array = [1, 4, 5, 2, 17, 12]```

We need to find the lowest element and remove it from the array, lets create a function to do this:

```
function minAndRemove(array) {
  let min = array[0]; 
	// here we're assuming the lowest element to be the first in the array
  let minIndex = 0;
	// we're assing the value of zero to the varibale minIndex
  for (let i = 0; i < array.length; i++) { 
	// here we are calling a for loop, that will iterate through each element of the array
	// it will compare each element in the array to min 
    if (array[i] < min) {
		// if the element is less than than min it will reassign min to this element, also assigning minIndex to this elements index
      min = array[i];
      minIndex = i;
    }
  }
  array.splice(minIndex, 1);
	// it will then use Javascriptis .splice method to remove this element from the array.
  return min;
	// and will return the lowest value to be used in our next step
}
```
 
 How're we following along so far? It can be confusing at first, but think of it like this. The function compares all of the elements against each other to find the one with the lowest value. It then removes and returns the lowest as the return value of this function. This means that when we call this function we will always be returned the lowest element of an array. 
 
 How do we use this to order an array? We have already figured out how to find the lowest element of an array, so now we can go ahead and add that to our `` sorted; `` array. Now if we could go back to that array that has had the lowest element removed and run the process again and get the next lowest and added that to the ``sorted;`` array we'd begin to get a picture of what the new sorted array would look like. Now we'd just need to do this for each element of the array and we'll have sorted it won't we.
 
 To do this we can write another function:
 
 ```
 function selectionSort(array) {
  let newMin;
	// first we'll create a variable that we'll assign later on in the function
  let sorted = [];
	// here is where we create out blank array that is going to be filled with the sorted elements
  while (array.length != 0) {
	// we call a while loop. Which iterates through each element of the array while its length is not equal to 0
    newMin = minAndRemove(array);
	// we assign the return value of each loop to the newMin variable
    sorted.push(newMin);
	// we then push this onto our blank sorted array
  }
  return sorted;
	// finally we return the sorted array, which will no be in order.
}
 ```
 
 
 There you have it! This is called selection sorting or the [selection sort algorithm](https://en.wikipedia.org/wiki/Selection_sort). It is a nice easy place to start, but it has its drawbacks. The Big O of this algorithm is n^2, which compared to other sorting algorithms like merge sort, with a Big O of n log n. It is considerably more costly.
 
 So I hope this helped explain one method for sorting arrays. Next I will be looking in details at merge sorting. 
 
 <iframe src="https://giphy.com/embed/1jkVi22T6iUrQJUNqk" width="480" height="473" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/fallontonight-nope-bye-1jkVi22T6iUrQJUNqk">via GIPHY</a></p>

