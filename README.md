# Introduction to Enumerables


## Learning Goals

* Define the "Character of Enumerable Methods"
* Pseudocode a Real-World Use of Enumerables
* Consult Ruby's Enumerable Documentation

## Introduction

As programmers, we wonder about the world, come up with questions and then
ask a computer to help us manipulate data to find answers. Many of those
questions can be resolved by either:

1. "Polling" every member in a collection and collecting the results into a
   new collection through a process called "mapping" (or)
2. "Polling" every member in a collection and joining those poll's results together
   into a single value through a process called "reducing"

In fact, Twitter user Steven Luscher managed to explain the big take-aways of these
ideas in a single tweet! 

![Enumerables in a Tweet](https://curriculum-content.s3.amazonaws.com/ruby-enumerables/introduction-to-enumerables/enumerables_in_a_tweet.png)

[_Original Source_](https://twitter.com/steveluscher/status/741089564329054208)

For example, we might work through a collection of food and apply the process
of "heat the thing" to each and create a collection of new
things. In Steven's example, we turn "corn/maize", "cow", and "chicken" into
"popcorn", "hamburger", and "fried egg." Or think about asking a collection of staff
members whether they want "Sushi Menu 1," "Sushi Menu 2," or "vegan option"
for the upcoming team meeting. We poll each staff member, get a result, and store
that result in a list.

In both these cases we're polling
every member in a collection and collecting the results into a new collection.
That's "mapping," but you might not have called it by that name before.

In Steven's reduce example, after we apply the "eat" process to "fried egg" and "popcorn,"
we are left with combined and processed food, or "💩". For
a slightly less gastric example, what if we asked our classmates how much cash they have
in their pocket so that we can "reduce" each person's money to a collective total which we can use to buy
our favorite teacher a nice present. That's "reducing," but you might not have called it by that name before!

### Uses of "map" and "reduce"

Oftentimes we "map" or "reduce" a collection so that we can ask a question
of that new collection.

* Did more than half of the staff choose the vegan option?
* Is the collected cash on hand greater or equal to 20% of the bill for staff lunch?

Mapping and reducing let us take "general data" and "groom it" to become
the data we need to answer a question.

### Think About It

Here are some real-world questions. See if you can identify whether to "map"
or "reduce" these collections.

* "If these projected profits turned to losses, what would those losses be?"
* "What numbers in this data set are larger than 200? Larger than 2,000? Larger
  than an argument a user might provide?"
* "Which painting is the most valuable?"
* "Which painting is the least valuable?"
* "Do any of these children have a wet cough?"

### Wrapping Map and Reduce

It's very common to put a "map" operation or a "reduce" operation _inside_ a method
so that we provide meaning or abstraction. Here's some Ruby-like pseudocode:

```ruby
def values_greater_than(dividing_number, array_of_numbers)
  # visit each member in array_of_numbers, "collect" it, if its value is greater than `dividing_number`
end

values_greater_than(200, [200, 2000, 3000, 0]) #=> [2000, 3000]
values_greater_than(5000, [200, 2000, 3000, 0]) #=> []
```

"Map" and "reduce" help you accomplish powerful work. By putting that work inside of
a meaningful method name, you help other programmers understand your conversation
with the computer on how to solve a problem. Also, by wrapping these operations
we've just seen how we can make them more abstract.

### The Word "Enumerable"

"Enumerable" is what we call a method provided by Ruby that:

1. "visits" each element or pair in a collection and then...
2. tests each of those elements or calculates something with them and returns a result and which ***then***...
3. returns a new collection of those returned results **or** which accumulates those returned results to a single value

In this module, we'll learn to use Ruby's Enumerable methods to answer the type
of question which involves "polling each member."

## Define the "Character of Enumerable Methods"

"Enumerate" comes from the Latin root words that mean "according to the
number." Ruby "visits" each element or pair "according to the number" of
elements or pairs present in the collection. The essential character of all
Enumerable methods or "Enumerables" is:

1. Given a collection
2. Based on the number, visit each one by its number in the series (Latin: _ex
   numero_, the source of "enumerate")
3. Do some "work" or "test" the elements or pairs in the collection
4. THEN:
  1. Accumulate those elements-after-work-was-applied into a new collection
  2. _OR_, determine some special value like: maximum, minimum, `true` if all
  values were truthy, `true` if any value was truthy, `true` if no values were
  truthy, etc.

This template applies **to all Enumerable methods**. We call it the "Character
of Enumerable Methods." This isn't a term you'll hear programmers use
day-to-day, but all of them know that all Enumerables follow this template and
have this "character."

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

> **PSEUDOCODE**: Below we're going to use "pseudocode." It's something that
> looks a bit like code, but we're not expecting that it would run, it's just a
> convenient way to express a problem's solution in a way like code, but far
> less demanding. It's common to find programmers "sketching" a problem or a
> phenomenon in pseudocode because it's usually shorter to write than English
> and, once you learn programming, it's a handy way to communicate with other
> programmers.

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
  # Given a collection of passengers' sounds ["coughing", "yawning", "sneezing", "singing Jamaican traditional folksong"]
  # If any of them are sick sounds: coughing, sneezing
  # return `true`; else, return `false`
end
```

If we were to encode this, we might write the (real code, not pseudocode) the
method as:

```ruby 
def i_hear_a_sick_sound(passengers_sounds)
  i = 0 # set up a i for the enumeration of the passengers collection
  while i < passengers_sounds.length do # a loop for each passenger
    # Stop enumerating and return true if any passenger is
    # coughing or sneezing
    if (passengers_sounds[i] == "coughing" || passengers_sounds[i] == "sneezing")
      return true
    end
    i += 1
  end
  return false
end

i_hear_a_sick_sound(["coughing", "foo", "bar", "bin", "bat"]) #=> true
i_hear_a_sick_sound(["sneezing", "foo", "bar", "bin", "bat"]) #=> true
i_hear_a_sick_sound([            "foo", "bar", "bin", "bat"]) #=> false
```

This is but one tiny example. If you don't live in a big city with public
transport, maybe you "poll" all the cars at a four-way stop sign to see who
arrived first. Perhaps you're a bit lax on your laundry and you "sniff test"
all the clothes on the floor _until_ you find the one that's least-offensive.  We 
use Enumerables all the time in real life! They're everywhere in life so
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
the return values for applying such-and-such Enumerable?

### Enumeration Versus Enumerables

You might think, "OK, I get it, Enumerables follow this 'Character of
Enumerables' thing and that seems sensible enough. What's so hard here?"

If you're thinking that, then GREAT! You're on the right track. The good news
here is that you understand "enumeration" as an abstract practice and that's
_exactly_ where we'd hope you'd be. You're doing great!

The trouble comes in when we talk about _coding_ with Ruby's Enumerable
methods. Specifically, the code can get confusing when we need to _abstract_
out the "work" that we should apply to each element. To feel truly comfortable
with Enumerable methods, we have to understand the challenging coding ideas of:

* Capturing work (but not _doing_ it) using a thing called a _block_
* Doing the work and passing it arguments based on visiting each element or
  pair in the collection. This is called _yielding_ to a block
* Gathering a new collection **or** combining the individual results into an
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

[enumdoc]: https://ruby-doc.org/core-2.6.5/Enumerable.html
