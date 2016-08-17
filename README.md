# Viral Coefficient Investigation
Johan Jordaan  
16 August 2016  



## Background


## Model
The model is very simple :  $U_{t+1} = U_t * (1+k)$ , were $k$ is the Viral Coeficient.  

## Assumptions
This study is based on the following two assumptions:

1 The Viral Coeficient $k$ is constant. 
2 All new users are aquired based on the strength of the Viral Coeficient.

## Exploring the model

```r
calc <- function(start, factor, steps) {
  calc_next <- function(a,b) { return(a*(1+factor)); }   
  retVal <- Reduce(calc_next,rep(start,steps),accumulate=TRUE);
  return(retVal);
}

start <- 1000
steps <- 30
k_vals <- c(0.1,0.05,0,-0.05,-0.1)

m <- sapply(k_vals,function(k) { calc(start,k, steps) });
m <- cbind(seq(1,steps),m);
m <- data.frame(m);
names(m) <- c("t",k_vals);

tm <- gather(m,"k","U",2:(length(k_vals)+1));
```



```r
p <- ggplot(tm, aes(x=t,y=U,color=k)) + geom_line()
print(p)
```

![](README_files/figure-html/graphs-1.png)<!-- -->


