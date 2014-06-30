---
title: Data Structure Manipulation
date: 2014-06-29 22:12 UTC
---

A common theme recently, in both our class warm-ups and in doing Exercism exercises has been reading things from a CSV, 
storing the data in a sorted hash or array. So I thought I would solidify it a little bit by posting here. One thing 
that I have been reminded of time and time again is to make things very small and then you can extrapolate from there. 
For me, it helps to conceptualize what I am doing and not get overwhelmed over-complicating things. Anyway, let's get started. 
 
We will assume the data came from a CSV and we know how to read it using the CSV class. The CSV docs can be found [here](http://ruby-doc.org/stdlib-2.0.0/libdoc/csv/rdoc/CSV.html)
if you want to reference them. If we read it by row, we will get an array of arrays. Here are a few lines of the 
initial CSV file:

```
Person,Week,Day,Mode,Inbound,Outbound,Distance
Emily,4,Monday,Walk,12,15,0.65
Gerard,1,Wednesday,Drive,14,12,5
Emily,5,Tuesday,Walk,12,15,0.65
```

Reading the file using the CSV method will result in an array of arrays as shown below: 

```
[['Emily', 4 ,'Monday', 'Walk', 12, 15, 0.65],
['Gerard', 1, 'Wednesday', 'Drive', 14, 12,5],
['Emily', 5, 'Tuesday', 'Walk', 12, 15, 0.65]]
```

Let's first start by sorting by the name. This is what our end product will look like: 

```
     {
     "Emily" => [
        {
          week: 4,
          day: "Monday",
          mode: "Walk",
          inbound: 12,
          outbound: 15,
          distance: 0.65
        },
        {
          week: 5,
          day: "Tuesday",
          mode: "Walk",
          inbound: 12,
          outbound: 15,
          distance: 0.65
         }
      ],
      "Gerard" => [
        {
          week: 1,
          day: "Wednesday",
          mode: "Drive",
          inbound: 14,
          outbound: 12,
          distance: 5
        }
      ],
      }
```

And here is my implementation: 

```
def sort_by_name
  sorted_hash = Hash.new
  @input.each do |info_array|
      if sorted_hash.has_key?(info_array.first)
        sorted_hash[info_array.first] << {:week => info_array[1],
                              :day => info_array[2],
                              :mode => info_array[3],
                              :inbound => info_array[4],
                              :outbound => info_array[5],
                              :distance => info_array[6]}
      else
        sorted_hash[info_array.first] = [{:week => info_array[1],
                              :day => info_array[2],
                              :mode => info_array[3],
                              :inbound => info_array[4],
                              :outbound => info_array[5],
                              :distance => info_array[6]}]

      end
    end
  sorted_hash
end
```

Above, the instance variable @input is the array of arrays that comes in after parsing the CSV. We want to go through each
array, pick out the person's name and assign it to be the key of the sorted hash. The if statement says that if the key
sorted hash already has the key, then shovel in the other information, but if it doesn't have the key, then we will make
an array with the rest of the hash. That is all there is to it!

The next steps are to sort by week, and then by day but that is a topic for another post. Maybe next week. Enjoy!