# Introduction to Enumerables

## Learning Goals

* Define Enumerable methods
* Pseudocode a Real-World Use of Enumerables
* Consult Ruby's Enumerable Documentation

## Introduction

In previous lessons, we built `while` loops to work with arrays. With slight
variations in code, we could create loops that printed out, changed, or copied
every element in an array. This sort of task is very handy and very common. So
much so, that Ruby provides methods specifically for these tasks. These methods
are called "Enumerables," and we will take a look at some of the most common
ones in the next few lessons.

### The Word "Enumerable"

"Enumerable" is what we call a method provided by Ruby that:

1. "visits" every element or pair in a collection and then...
2. does some work with the element - calculate, modify, sum, compare, etc...

_Usually_, the result of any work being done on each element is collected. After
every element is visited, the Enumerable either returns this new collection of
results **or** accumulates them and returns a single value.

**Note:** we say _usually_ because there is one exception - sometimes we to
perform some work using _each_ element but don't care about the results. An
example of this would printing every element in an array to the terminal. In
this case, we wouldn't need to bother with collecting or accumulating the
elements.

## Pseudocode a Real-World Use of Enumerables

Let's consider how a real-world need might drive us to think and behave in
accordance with how Enumerable methods work.

> **PSEUDOCODE**: Below we're going to use "pseudocode." It's something that
> looks a bit like code, but we're not expecting that it would run, it's just a
> convenient way to express a problem's solution in a way like code, but far
> less demanding. It's common to find programmers "sketching" a problem or a
> phenomenon in pseudocode because it's usually shorter to write than English
> and, once you learn programming, it's a handy way to communicate with other
> programmers.

Imagine you are cooking for a group of friends and want to find out if they have
any dietary restrictions. You might 'poll' the group, asking each friend. You
could then use their responses to determine what food you can and cannot cook.
If a friend is vegetarian, for instance, you won't want to cook any meat-based
dishes. We might pseudocode this out as:

```ruby
while cooking_for_friends
  if anyone_is_vegetarian
    vegetarian_meal = true
  end
end
```

We could convert this into a pseudocoded method, `is_anyone_vegetarian?`, like
this:

```ruby
def is_anyone_vegetarian?(list_of_dietary_restrictions)
  # Given a collection of dietary restrictions (["lactose intollerant", "none", "allergic to peanuts", "vegetarian"])
  # If any of them are vegetarian
  # return `true`; else, return `false`
end
```

If we were to encode this, we might write the (real code now, not pseudocode)
the method as:

```ruby 
def is_anyone_vegetarian?(list_of_dietary_restrictions)
  i = 0 # set up a i for the enumeration of the dietary restriction collection
  while i < list_of_dietary_restrictions.length do # a loop for each dietary restriction
    # Stop enumerating and return true if any dietary restriction is
    # equal to 'vegetarian'
    if list_of_dietary_restrictions[i] == "vegetarian"
      return true
    end
    i += 1
  end
  return false
end

is_anyone_vegetarian?(["vegetarian", "none", "paleo", "dairy free", "none"]) #=> true
is_anyone_vegetarian?(["none", "paleo", "dairy free", "none"]) #=> false
is_anyone_vegetarian?(["foo", "bar", "bin", "bat"]) #=> false
```

The Enumerable equivalent to the `while` loop above would be to use the `any?`
Enumerable on the list of dietary restrictions:

```rb
def is_anyone_vegetarian?(list_of_dietary_restrictions)
  list_of_dietary_restrictions.any? do |restriction|
    restriction == "vegetarian"
  end
end

is_anyone_vegetarian?(["vegetarian", "none", "paleo", "dairy free", "none"]) #=> true
is_anyone_vegetarian?(["none", "paleo", "dairy free", "none"]) #=> false
is_anyone_vegetarian?(["foo", "bar", "bin", "bat"]) #=> false
```

This is but one example. If you aren't into cooking, maybe you "poll" all
the cars at a four-way stop sign to see who arrived first. Perhaps you're a bit
lax on your laundry and you "sniff test" all the clothes on the floor _until_
you find the one that's least-offensive.  We use Enumerables all the time in
real life! They're everywhere in life, so they're useful to have in code as
well.

## Consult Ruby's Enumerable Documentation

Ruby provides us _lots_ of Enumerable methods. This module _will not_ duplicate
the documentation and teach each one to you. Part of becoming comfortable with
programming is becoming comfortable with finding answers in the documentation.
We'll get you started, but you need to own your own education.

To help make sure you grasp what kinds of methods follow the "Character of
Enumerable Methods," consult Ruby's [Enumerable documentation][enumdoc]. Look
at the list of Methods on the left. You'll see what kind of activities follow
the Enumerable character. Pick a few methods that you find interesting and look
at the code examples.  You don't need to understand the code fully here, just
appreciate what kinds of things you'll be able to do with collections. What are
the return values for applying such-and-such Enumerable?

### Enumeration Versus Enumerables

You might think, "OK, I get it, Enumerables follow a certain pattern, and that
seems sensible enough. What's so hard here?"

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
and inspired by how well Ruby mirrors daily human activity.

With Ruby's Enumerables on your side, you'll tear through complex questions
with ease &mdash; and surprisingly few keystrokes! We'll start our exploration
in the next lesson.

## Video Review: Debugging

Before we embark on exploring Enumerables any further, it is important that we take a
few moments to review our debugging skills. The video below walks through the process of
debugging code with Pry using the upcoming Hashketball lab. Although you haven't seen this lab
yet, the concepts reviewed are applicable to all of the labs in this section (and beyond).
Check out the [Using Pry][] lesson to review Pry further.

<iframe width="560" height="315" src="https://www.youtube.com/embed/uv6fvdKXAnM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Try using Pry in the next lab!

[Using Pry]: https://github.com/learn-co-curriculum/reading-errors-and-debugging-using-pry

## Conclusion

A vast number of problems have a solution that involves following the
"character" of enumeration:

Process a collection by visiting each one and do "work" on it to return a new
collection **or** an aggregate value. Understanding enumeration in the big
picture is the first step to understanding Enumerable methods, which we'll begin
to study in the next lesson.

[enumdoc]: https://ruby-doc.org/core-2.6.5/Enumerable.html
