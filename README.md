# Introduction to Enumerables


## Learning Goals

* Define the "Character of Enumerable Methods"
* Pseudocode a Real-World Use of Enumerables
* Consult Ruby's Enumerable Documentation
* Consult Ruby's Enumerable Documentation

## Introduction

As programmers, we ask wonder about the world, come up with questions and then
ask a computer to help us manipulate data to find answers. Many of those
questions can be resolved by "polling" every member in a collection. We'd
typically "poll" each number in the collection and feed that value to a
calculation (French Word For _x_) _or_ aggregate that value into a running
value (like a total).

Here are some real-world questions:

* "If these projected profits turned to losses, what would those losses be?"
* "What numbers in this data set are larger than 200? Larger than 2,000? Larger
  than an argument a user might provide?"
* "Which painting is the most valuable?"
* "Which painting is the least value?"
* "Do any of these unvaccinated children have a wet cough?"

These real-world questions that involve:

1. Finding a collection of data, typically stored in an `Array` or `Hash`
2. Visiting each element (`Array`) or pair (`Hash`) in the collection
3. Doing some "work" with that element or pair
4. Returning a new collection **or** a new value based on the "work" that
   touched each element

When we say "work" we mean the evaluation of some expression that uses the
"current element."

We call the built-in methods provided by Ruby that "visit" each element or pair
in a collection, test those elements or pairs with "work," and then return a
new collection **or** a value "Enumerables." In this module we'll learn to use
Ruby's Enumerable methods to answer the type of question which involves
"polling each member."

## Define the "Character of Enumerable Methods"

"Enumerate" comes from the Latin root words that mean "according to the
number." Ruby "visits" each element or pair "according to the number" of
elements or pairs present in the collection. The essential character of all
Enumerable methods or "Enumerables" is:

1. Given a collection
2. Based on the number visit each one by its number in the series (Latin: _ex
   numero_, the source of "enumerate") or "enumerate" the collection
3. Do some "work" or "test" the elements or pairs in the collection
4. THEN
  1. Accumulate those elements after work was applied into a new collection
  2. _OR_, determine some special value like: maximum, minimum, `true` if all
values were truthy, `true` if any value was truthy, `true` if no values were
truthy, etc.

This template applies **to all Enumerable methods** therefore we call it the
"Character of Enumerable Methods." This isn't a term you'll hear programmers
use day-to-day, but all of them know that all Enumerables follow this template.

> **LOOKING AHEAD**: In fact, as you become more experienced with creating new
> things in Ruby (`StudentRoster`s or `PayrollWeek`s) you'll learn to make it
> possible to make them answer Enumerable questions. To do so you'll have to
> have this "Character" or "template" in the back of your mind.

## Pseudocode a Real-World Use of Enumerables

Let's consider how a real-world need might drive us to think and behave in
accordance with the "Character of Enumerable Methods."

True story: someone close to us got married last year. In anticipation of his
destination wedding and fabulous honeymoon in Italy, he was determined to
reduce his chances of getting sick. The only problem, he takes public transit
every day to work.

His **Question** was: "How can I avoid being sick for these special occasions?"

Doing some research, he realized he could reduce airborne infection risk by
_wearing a surgical mask_. But he didn't want to wear one all the time so he
decided to implement the following modification to his behavior:

> **PSEUDOCODE**: Below we're going to use "pseudocode." Its something that
> looks a bit like code, but we're not expecting that it would run, it's just a
> convenient way to express a problem's solution in a way like code, but far
> less demanding. It's common to find programmers "sketching" a problem or a
> phenomenon because it's usually shorter to write than English and, once you
> learn programming, using programming to communicate, even in "normal life"
> settings becomes handy.

```ruby
while on_the_train
  if i_hear_a_sick_sound
    my_mask_status = true
  end
end
```

The method name `i_hear_a_sick_sound`'s pseudocode looks like
this:

```ruby
def i_hear_a_sick_sound(passengers)
  # Given a collection of passengers' sounds ["coughing", "yawning", "sneezing", "singing jamaican traditional folksong"]
  # If any of them are sick sounds: cough, yawn
  # return `true`; else, return `false`
end
```

If we were to encode this we might write the (real code, not pseudocode) the
method as:

```ruby 
def i_hear_a_sick_sound(passengers_sounds)
  i = 0 # set up a i for the enumeration of the passengers collection
  while i < passengers.length do # a loop for each passenger
    # Stop enumerating and return true if any passenger is
    # coughing or sneezing
    if (passenger[i] == "coughing" || passenger[i] == "sneezing")
      return true
    end
    i += 1
  end
  return false
end
```

This is but one tiny example. If you don't live in a big city with public
transport, maybe you "poll" all the cars at a four-way stop sign to see who
arrived first. Perhaps you're a bit lax on your laundry and you "sniff test"
all the clothes on the floor to find one that's least-offensive.  We use
Enumerables all the time in our real life! They're everywhere in life so
they're very useful to have in code as well.

## Consult Ruby's Enumerable Documentation

Ruby provides us _lots_ of Enumerable methods. This module _will not_ duplicate
the documentation and teach each one to you. Part of becoming comfortable with
programming is becoming comfortable with finding answers in the documentation.
We'll certainly get you started, but you need to own your own education.

To help make sure you grasp what kinds of methods follow the "Character of
Enumerable Methods," consult Ruby's [Enumerable documentation][enumdoc]. Look
at the list of Methods on the left. You'll see what kind of activities follow
the Enumerable character. Pick a few methods that you find interesting and look
at the code examples.  You don't need to understand the code fully here, just
appreciate what kinds of things you'll be able to do with collections. What are
the return values for applying such-and-such Enumerable.

### Enumeration versus Enumerables

You might think, "OK, I get it, Enumerables follow this 'Character of
Enumerables' thing and that seems sensible enough. What's so hard here?"

If you're thinking that, then GREAT! You're on the right track. The good news
here is that you understand "enumeration" as an abstract practice and that's
_exactly_ where we'd hope you'd be. You're doing great!

The trouble comes in when we talk about _coding_ with Ruby's Enumerable
methods. Specifically, the code can get confusing when we need to _abstract_
out the "work" that we should apply to each element. To feel truly comfortable
with Enumerable methods, we have to understand the challenging coding ideas of:

* capturing work (but not _doing_ it) using a thing called a _block_
* doing the work and passing it arguments based on visiting each element or
  pair in the collection, called _yielding_ to a block
* gathering a new collection **or** combining the individual results into an
  aggregate result

If this sounds complex, don't worry: we've built a stair-step of lessons to
help you get comfortable with the terminology and code of enumeration. If this
all sounds obvious and easy, we hope you're going to be philosophically engaged
and inspired by how well Ruby mirrors human daily activity.

With Ruby's Enumerables on your side, you'll tear through complex questions
with ease &mdash; and surprisingly few keystrokes! We'll start our exploration
in the next lesson.

## Conclusion

A wide number of problems have a solution that involves following the
"character" of enumeration:

Process a collection by visiting each one and do "work" on it in order to
return a new collection **or** an aggregate value. Understanding enumeration in
the big picture is the first step to understanding Enumerable methods, which
we'll begin to study in the next lesson.
