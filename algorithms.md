1. [Big O notation Cheat Sheet](http://bigocheatsheet.com/)
2. Gradient Descent Algorithm in R for 2 variables (x and y)
  ```r
  # Simple data set
data <- read.table(text = "
x y
0 0 
1 1
2 2
3 3
4 4
5 5", header = T, sep = "")
```
```r
gd_1var1 <- function(data, thita_0, thita_1, alpha,no_iteration){
  # Browser is a function in R to debug. It is very helpful to insert this 
  # function to understand what's going on.
  # browser()
  # Compute cost function 
  # sum((thita_1 * data$x + thita_0 - data$y)^2) calculates summation from i = 1,m
  costfun <- (1/2*nrow(data))*sum((thita_1 * data$x + thita_0 - data$y)^2)
  # Need to decide the condition till when costfun is run
  i = 1
  while (i < no_iteration){
    # temp0 is the variable to calculate the change in slope of thita_0 
    # Second term in the partial derivative terms of costfunction when thita=0
    temp0 <- thita_0 - alpha*sum((1/nrow(data))*(thita_0 + thita_1*data$x - data$y))
    # temp0 is the variable to calculate the change in slope of thita_0 
    # Second term in the partial derivative terms of costfunction when thita=0
    temp1 <- thita_1 - alpha*sum((1/nrow(data))*(thita_0 + thita_1*data$x - data$y) * data$x)
    # Update thita_0 and thita_1
    thita_0 <- temp0
    thita_1 <- temp1
    # Calculate cost function again
    costfun <- (1/2*nrow(data))*sum((thita_1 * data$x + thita_0 - data$y)^2)
    i <- i + 1
  }
  # After the while loop is finished output thita_0 and thita_1
  return(data.frame(thita_0, thita_1, costfun))
}

gd_1var1(data = data, thita_0 = 0.8, thita_1 = 1.5, alpha = 0.1, no_iteration = 10)
gd_1var1(data = data, thita_0 = 0.8, thita_1 = 1.5, alpha = 0.1, no_iteration = 100)
gd_1var1(data = data, thita_0 = 0.8, thita_1 = 1.5, alpha = 0.1, no_iteration = 1000)
gd_1var1(data = data, thita_0 = 0.8, thita_1 = 1.5, alpha = 0.1, no_iteration = 10000)
gd_1var1(data = data, thita_0 = 100, thita_1 = 105, alpha = 0.1, no_iteration = 100000)
```
