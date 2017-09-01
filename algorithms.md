# [Big O notation Cheat Sheet](http://bigocheatsheet.com/)
# Gradient Descent Algorithm in R for 2 variables (x and y)

Basic Equations of Gradient Descent Algorithm
![Basic Equations](https://snag.gy/5ByKSs.jpg)
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
# Normal Equation Method and Gradient Descent 

```r
# In this page, we will look at normal equation method and gradient discent 
# method for the same data set 

# Data are normalized using the following procedure 
# x - mean(x) / (range(x))
# Example from Andrew Ng's Machine Learning course (Just consists of 4 rows of data)

# Normal Equation Method 

x1 <- c(2104, 116, 1534, 852) 
# Normalize x1 variable
x1 <- (x1-mean(x1))/diff(range(x1))
x1

# Assign x2 variable
x2 <- c(5,3, 3, 2)
# Normalize x2 variable
x2 <- (x2 - mean(x2))/diff(range(x2))
x2

# Assign y variable
y <- c(460, 232, 315, 178) 
# Normalize y variable 
y <- (y - mean(y))/diff(range(y))
y
#y <- y/460
x0 <- c(1,1,1,1) 

# Create a matrix with x0, x1 and x2 using cbing 
mat <- as.matrix(cbind(x0,x1,x2))
mat
x1;x2;y;x0

mat_y <- as.matrix(y)

# Now solve for thita
# thita = (XT X)-1 XT Y
# In R in order to multiply two matrices we need to use operator %*% not "*"
# To find the inverse we use the function solve()
# To find the transpose we use the function t()
thita <- solve(t(mat) %*% mat)%*%t(mat) %*% mat_y

thita

# Second Part 
# Gradient Descent Method 

data <- data.frame(x1,x2,y)
data$x1 <- data$x1 / 2104
data$x3 <- data$x3 / 460

# For 2 variable
gd_2var <- function(data, thita_0, thita_1, thita_2, alpha,no_iteration){
  # Browser is a function in R to debug. It is very helpful to insert this 
  # function to understand what's going on.
  # browser()
  # Compute cost function 
  # sum((thita_1 * data$x + thita_0 - data$y)^2) calculates summation from i = 1,m
  costfun <- (1/2*nrow(data))*sum((thita_2 * data$x2 + thita_1 * data$x1 + thita_0 - data$y)^2)
  # Need to decide the condition till when costfun is run
  i = 1
  while (i < no_iteration){
    # temp0 is the variable to calculate the change in slope of thita_0 
    # Second term in the partial derivative terms of costfunction when thita=0
    temp0 <- thita_0 - alpha*sum((1/nrow(data))*(thita_0 + thita_1*data$x1+thita_2*data$x2 - data$y))
    # temp0 is the variable to calculate the change in slope of thita_0 
    # Second term in the partial derivative terms of costfunction when thita=0
    temp1 <- thita_1 - alpha*sum((1/nrow(data))*(thita_0 + thita_1*data$x1 + thita_2 *data$x2 - data$y) * data$x1)
    temp2 <- thita_2 - alpha*sum((1/nrow(data))*(thita_0 + thita_1*data$x1 + thita_2 *data$x2 - data$y) * data$x2)
    # Update thita_0 and thita_1
    thita_0 <- temp0
    thita_1 <- temp1
    thita_2 <- temp2
    # Calculate cost function again
    costfun <- (1/2*nrow(data))*sum((thita_2 * data$x2 + thita_1 * data$x1 + thita_0 - data$y)^2)
    i <- i + 1
  }
  # After the while loop is finished output thita_0 and thita_1
  return(data.frame(thita_0, thita_1, thita_2, costfun))
}

# Different tests for gradient descent method using two features to predict y
gd_2var(data = data, thita_0 = 0.8, thita_1 = 1.5, thita_2 = 10, alpha = 0.1, no_iteration = 10)
gd_2var(data = data, thita_0 = 0.8, thita_1 = 1.5, thita_2 = 10, alpha = 0.1, no_iteration = 100)
gd_2var(data = data, thita_0 = 0.8, thita_1 = 1.5, thita_2 = 10, alpha = 0.1, no_iteration = 1000)
gd_2var(data = data, thita_0 = 0.8, thita_1 = 1.5, thita_2 = 10, alpha = 0.1, no_iteration = 10000)
gd_2var(data = data, thita_0 = 100, thita_1 = 105, thita_2 =10 , alpha = 0.1, no_iteration = 100000)
```
