# jrvFinance

This R package implements the basic financial analysis functions
similar to (but not identical to) what is available in most
spreadsheet software. This includes finding the IRR and NPV of
regularly spaced cash flows and annuities. Bond pricing and YTM
calculations are included. In addition, Black Scholes option pricing
and Greeks are also provided.

## NPV, XNPV, IRR and XIRR functions

```{r}
npv(cf=c(100,250,300), rate=5e-2)
npv(cf=c(1,3,2), rate=10e-2, cf.t=c(0.3,1.9,2.5))
irr(c(-600,300,400))
irr(cf=c(-450,100,300,200), cf.t=c(0, 0.3,1.9,2.5)) 
```

## Annuity functions

```{r}
annuity.pv(rate=10e-2, n.periods=15)
annuity.pv(rate=10e-2, n.periods=15, immediate.start = TRUE)
annuity.pv(rate=10e-2, instalment = 450, n.periods=360, cf.freq=12, comp.freq=2)
annuity.rate(pv=50000, instalment = 450, n.periods=360, cf.freq=12, comp.freq=2)
annuity.instalment(rate=9e-2, pv=10000, n.periods=8)
annuity.instalment.breakup(rate=9e-2, pv=10000, n.periods=8, period.no=5)
```

## Bond Price, Yield and Duration

```{r}
bond.price(settle="2012-04-15", mature="2022-01-01", coupon=8e-2,
           yield=8.8843e-2)
bond.price(settle="2012-04-15", mature="2022-01-01", coupon=8e-2,
bond.price(settle="2012-04-15", mature="2022-01-01", coupon=8e-2,
           yield=8.8843e-2, freq=1, comp.freq=2)
bond.yield(settle="2012-04-15", mature="2022-01-01", coupon=8e-2,
           price=95) 
bond.duration(settle="2012-04-15", mature="2022-01-01", coupon=8e-2,
              yield=8.8843e-2)
bond.duration(settle="2012-04-15", mature="2022-01-01", coupon=8e-2,
              yield=8.8843e-2, modified=TRUE)
coupons.dates(settle="2012-04-15", mature="2022-01-01")
coupons.next(settle="2012-04-15", mature="2022-04-01")
coupons.prev(settle="2012-04-15", mature="2022-04-01")
coupons.n(settle="2012-04-15", mature="2017-07-01")
```

##  (Generalized) Black Scholes Formulas


```{r}
GenBS(s=100, X=100, r=0.1, Sigma=20e-2, t=1, div_yield=0)
GenBS(s=100, X=120, r=0.1, Sigma=15e-2, t=1, div_yield=5.8e-2)
GenBSImplied(s=100, X=900, r=0, price=7.97, t=1, div_yield=0)
```

## Utility functions


```{r}
equiv.rate(10e-2, from.freq = 12, to.freq = 2) 
equiv.rate(15e-2, from.freq = 1, to.freq = Inf)
edate("2005-05-17", -8) 
edate("2007-02-28", 4) 
```

## Newton Raphson and bisection root solver

The package implements a Newton Raphson root solver that is used
internally to calculate IRR and YTM. It is available for general use.


```{r} 
fn1 <-function(x){list(value=sin(x)-cos(x), gradient=cos(x)+sin(x))} 
newton.raphson.root(fn1) 
```

The package implements a bisection root solver that does a geometric
grid search to bracket the root and then calls `uniroot` to find the
root within this interval. The package uses the function internally to
calculate IRR and YTM, but `bisection.root` is available for general
use.

```{r}
bisection.root(sin, guess = 7, lower=1, upper=13)
bisection.root(sin, guess = 12, lower=1, upper=13) 
```

