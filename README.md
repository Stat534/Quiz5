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

num.grid <- 1000
x1 <- seq(0,10, length.out = num.grid)
d11 <- dist(x1, upper=T, diag = T) %>% as.matrix()
Omega11 <- sigma.sq * exp(-d11 * phi)

d.big <- dist(c(x1,x2), upper=T, diag = T) %>% as.matrix()
d12 <- d.big[(1:num.grid),((num.grid+1):(num.pts + num.grid))]
Omega12 <- sigma.sq * exp(-d12 * phi)

cond.exp <- rep(0, num.grid) + Omega12 %*% solve(Omega22) %*% (y2 - mu2)

cond.cov <- Omega11 - Omega12 %*% solve(Omega22) %*% t(Omega12)

exp.df <- data.frame(x = x1, y = cond.exp, upper = cond.exp + 1.96 * sqrt(diag(cond.cov)), lower = cond.exp - 1.96 * sqrt(diag(cond.cov)))

GP.dat %>% ggplot(aes(x=x2, y=y2)) + geom_point() + xlim(0,10)  + ylab('Response') + xlab('x coordinate') + ggtitle('1D GP example with conditional mean and intervals') + geom_line(data = exp.df, aes(x=x, y=y), linetype = 2) +geom_line(data = exp.df, aes(x=x, y=upper), linetype = 3, color='red') + geom_line(data = exp.df, aes(x=x, y=lower), linetype = 3, color='red') 
```

## Question 2. (1 point)

What is your favorite part of this class?

## Question 3. (1 point)

What could be changed to improve your learning?
