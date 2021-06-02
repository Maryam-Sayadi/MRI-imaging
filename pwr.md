# PWR package

### Install

```R
install.packages("pwr", repos="http://cran.r-project.org")

library(pwr)
```

### Test

```R
#f2 <- seq(0.2, 4, 0.02) # define a range of effect-sizes and sampling rate within this range
#nf2 <- length(f2)

pred <- seq(3, 8, 1) # define a range of predictors
npred <- length (pred)

p <- seq(0.5, 0.95, 0.1) # define a range for the power values, and their sampling rate
np <- length(p)

sampleSize <- array(numeric(npred*np), dim=c(npred, np))

for (i in 1:np) {
  for (j in 1:npred) {
    testResult <- pwr.f2.test(u = pred[j], v = NULL, f2 = 0.8, sig.level = 0.05, power = p[i])  # effect size = 0.8

    sampleSize[j, i] <- ceiling(testResult$v)
  }
}

xRange <- range(pred)
yRange <- round(range(sampleSize))
colors <- rainbow(length(p))
plot(xRange, yRange, type="n", xlab="# of predictors", ylab="Sample Size (u)")

# Add power curves
for (i in 1:np) lines(pred, sampleSize[ , i], type="l", lwd=2, col=colors[i])
# add annotations (grid lines, title, legend)
abline(v=0, h=seq(0, yRange[2], 10), lty=2, col="light grey")
abline(h=0, v=seq(xRange[1], xRange[2], 0.5), lty=2, col="light grey")
title("#of predictors vs. Sample-size for \ndifferent Power values in
      (0.5, 0.95),effect size = 0.8 Sigificance=0.05 (MLR)")
legend("topright", title="Power", as.character(p), fill=colors)
```

![effectsizeOF0.08](../assets/effect_0.8.png)



```R
#f2 <- seq(0.2, 4, 0.02) # define a range of effect-sizes and sampling rate within this range
#nf2 <- length(f2)

pred <- seq(3, 8, 1) # define a range of predictors
npred <- length (pred)

p <- seq(0.5, 0.95, 0.1) # define a range for the power values, and their sampling rate
np <- length(p)

sampleSize <- array(numeric(npred*np), dim=c(npred, np))

for (i in 1:np) {
  for (j in 1:npred) {
    testResult <- pwr.f2.test(u = pred[j], v = NULL, f2 = 0.7, sig.level = 0.05, power = p[i])  # effect size = 0.7

    sampleSize[j, i] <- ceiling(testResult$v)
  }
}

xRange <- range(pred)
yRange <- round(range(sampleSize))
colors <- rainbow(length(p))
plot(xRange, yRange, type="n", xlab="# of predictors", ylab="Sample Size (u)")

# Add power curves
for (i in 1:np) lines(pred, sampleSize[ , i], type="l", lwd=2, col=colors[i])
# add annotations (grid lines, title, legend)
abline(v=0, h=seq(0, yRange[2], 10), lty=2, col="light grey")
abline(h=0, v=seq(xRange[1], xRange[2], 0.5), lty=2, col="light grey")
title("#of predictors vs. Sample-size for \ndifferent Power values in
      (0.5, 0.95), Sigificance=0.05,effect size = 0.7 (MLR)")
legend("topright", title="Power", as.character(p), fill=colors)

```

![effect-sizeOF0.07](../assets/effect_0.7.png)


### Side by Side figures

![effect-sizeOF0.07](../assets/effect_0.7.png)
![effect-sizeOF0.08](../assets/effect_0.8.png)
