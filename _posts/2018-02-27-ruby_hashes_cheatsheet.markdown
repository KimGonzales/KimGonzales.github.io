---
layout: post
title:      "Ruby Hashes CheatSheet!"
date:       2018-02-27 13:56:18 -0500
permalink:  ruby_hashes_cheatsheet
---

**How to Create, Add to and Retrieve Data from Hashes**



**What is a Hash?**

A hash, also known as an associative array, is a collection of stored data in key/value pairs.  A key/value pair is a set of linked data. Like words in a dictionary, hash keys serve as reference points to access specific data. Each key is unique and points to an assigned value.  

As an example, the my_dog hash below contains 3 key/value pairs. The three keys are the three symbols ":name", ":breed" and ":favorite_food". Each unique key points to it's own value. The key ":breed" points to the value of "Wheatador". 

``` 
my_dog = { :name => "Bowser", :breed => "Wheatador", :favorite_food => "garbage" }

```

**Creating Hashes**

The my_dog hash above is created using the literal constructor. Below we've made an empty hash using that same method. 

```
hash = {}
```

The literal hash constructor wraps key/value pairs in curly brackets. Each key becomes associated to its value by using a hash-rocket =>. 

Another way to create an empty hash is by using the class constructor:

```
 hash = Hash.new
 
 => {}
```


Hash keys can be strings, integers or symbols, but it is important to note that each key MUST be unique. If we tried to add a duplicate key, it would merely overwrite the old one as opposed to adding a second instance of it.

**Adding Data To Hashes**

```
my_dog = { :name => "Bowser", :breed => "Wheatador", :favorite_food => "garbage" }
```

Say I wanted to add another key/value pair to my_dog. I want to add his size attrribute. I would do so by using the bracket equals method [] =. To use this method, we call the hash, place the key in the brackets and set that equal to the new key's value:

```
my_dog[:size] = "medium"

my_dog

# = >  {:name=>"Bowser", :breed=>"wheatador", :favorite_food=>"garbage", :size=>"medium"}
```

Now there are 4 key/value pairs in my_dog hash!


**Retrieving Data from Hashes**

```
artists = { :name => "Odezsa", :top_song => "Sun Models", :people => ["Harrison Mills", "Clayton Knight"] } 

```

If we know the key of the value we are try to retreive we can use the bracket method on a hash in a way that is similar to using an index to retrieve an element from an array. 


If I wanted to know the artist's top song, I would retrieve the data as follows:

```
artists[:top_song]

# = > "Sun Models"

```

What if we didn't know the keys to the artists hash? No problem! 

Call .keys on the hash to retrieve an array containing all the available keys in the hash:

```
artists.keys

# => [:name, :top_song, :people]

```
If we try to retreive values for a key that does not exist in a hash, we are given the default value nil:

```
artists = { :name => "Odezsa", :top_song => "Sun Models", :people => ["Harrison Mills", "Clayton Knight"] } 

artists[:hometown]

# => nil
```
Similar to the .keys method, calling the .values method will give us all the values of the hash in an array. 

```
artists.values 

# =>["Odezsa", "Sun Models", ["Harrison Mills", "Clayton Knight"]]
```


As you can see, the value of the 3rd key value pair is an array.  If we only wanted to retrieve "Clayton Knight", we would use our bracket method similar to before. First we call it's key and then its index since that key's value is an array!


```
artists[people][1]

# => "Clayton Knight"
```

There you have it. We've reviewed how to create, add and retrieve data from a hash. I hope this read deepens your understanding and helps you the next time you need a reminder of hash techniques. 





