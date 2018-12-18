---
title: "Edge Case: Nested and Mixed Lists"
categories:
  - Edge Case
tags:
  - content
  - css
  - edge case
  - lists
  - markup
---

Nested and mixed lists are an interesting beast. It's a corner case to make sure that

* Lists within lists do not break the ordered list numbering order
* Your list styles go deep enough.

### Ordered -- Unordered -- Ordered

1. ordered item
2. ordered item 
  * **unordered**
  * **unordered** 
    1. ordered item
    2. ordered item
3. ordered item
4. ordered item

### Ordered -- Unordered -- Unordered

1. ordered item
2. ordered item 
  * **unordered**
  * **unordered** 
    * unordered item
    * unordered item
3. ordered item
4. ordered item

### Unordered -- Ordered -- Unordered

* unordered item
* unordered item 
  1. ordered
  2. ordered 
    * unordered item
    * unordered item
* unordered item
* unordered item

### Unordered -- Unordered -- Ordered

* unordered item
* unordered item 
  * unordered
  * unordered 
    1. **ordered item**
    2. **ordered item**
* unordered item
* unordered item


-----------------

---
title: "Introduction to Data Science"
date: 2018-10-04
tags: [En Español]
header:
mathjax: "True"
---
# H1 Heading 

## H2 Heading

### H3 Heading

This is some basic text...

And here is text with *italics*

Here's some **bold** text.

Bulleted lists:
* First item
+ Second item
- Third item

Here's a numbered list:
1. First
2. Second
3. Third

Python code block:
```python
  import numpy as np

  def test_function(x,y):
    z = np.sum(x,y)
    return z
```

R code block:
```r
  library(tidyverse)
  df <- read_csv("example.csv")
  head(df)
```


Here's some inline code 'x+y'

Here's an image using HTML:

<img src="{{ site.url }}{{ site.baseurl }}/images/IMG_0880.jpg" alt="Apollo">

Here's an image using Kramdown:
![alt]({{ site.url }}{{ site.baseurl }}/images/IMG_0880.jpg)

Here are some equations by adding $$:

$$z=x+y$$

Or inline $$z=x+y$$
-->












