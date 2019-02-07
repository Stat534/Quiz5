# Quiz5

## Question 1. (8 points)

Recreate the 1-D Gaussian Process Example, but now set the nugget term to be 1 and updating the Omega matrices. This can be done by modifing the code below. Comment on how the results (both the mean and interval) differ.

```{r}
set.seed(02012019)
num.pts <- 6
sigma.sq <- 1
tau.sq <- 0
phi <- .75
x2 = runif(num.pts, max = 10)
mu2 <- rep(0, num.pts)
d2 <- dist(x2, upper=T, diag = T) %>% as.matrix()
Omega22 <- sigma.sq * exp(-d2 * phi)
y2 = rmnorm(1, mu2, Omega22)
GP.dat <- data.frame(x2=x2, y2 = y2)

GP.dat %>% ggplot(aes(x=x2, y=y2)) + geom_point() + xlim(0,10)  + ylab('Response') + xlab('x coordinate') + ggtitle('1D GP example')
```

## Question 2. (1 point)

What is your favorite part of this class?

## Question 3. (1 point)

What could be changed to improve your learning?
