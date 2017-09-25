```ruby
** Summary stats for married unmarried workers: all, men, women
** Estimating marriage wage premiums by ols for all, men, women
**
** The sample is full-time workers in the state of Nebraska aged 24 to 64 years old from the
** 2016 current population Survey, March supplement.

* use 80 columns
set nowide

* read in the data, skipping header line
* data should be placed in the same directory as the workspace
read(cps2016_NE.dat) female married nevermar wkswork &
 wsal age hsdeg somecol colldeg msdoc hrswkd nonwht hispanic state / skiplines=1

* total hours worked
genr hours=wkswork*hrswkd

* set option to not throw warnings when data is skipped
set nowarnskip

* calculate wage per hour
genr wsalphr=wsal/hours

** Throughout the rest of this program, we will only consider workers who earned at >4 dollars/hour **

* wsalphr, married descriptive statistics for ALL workers
* delete skip$ to eliminate all skipif commands in effect
skipif (wsalphr.le.4)
stat wsalphr married
delete skip$

*** Part 1:
*** a.

** ALL workers considered

* Finding wsalphr sample means and sample variances for MARRIED workers
skipif (wsalphr.le.4)
skipif (married.eq.0)
stat wsalphr 
delete skip$

* Finding wsalphr sample means and sample variances for UNMARRIED workers
skipif (wsalphr.le.4)
skipif (married.eq.1)
stat wsalphr 
delete skip$

*** b.

** MEN

* Finding wsalphr sample means and sample variances for MARRIED MEN
skipif (wsalphr.le.4)
skipif (female.eq.1)
skipif (married.eq.0)
stat wsalphr 
delete skip$

* Finding wsalphr sample means and sample variances for UNMARRIED MEN
skipif (wsalphr.le.4)
skipif (female.eq.1)
skipif (married.eq.1)
stat wsalphr 
delete skip$

** WOMEN

* Finding wsalphr sample means and sample variances for MARRIED WOMEN
skipif (wsalphr.le.4)
skipif (female.eq.0)
skipif (married.eq.0)
stat wsalphr 
delete skip$

* Finding wsalphr sample means and sample variances for UNMARRIED WOMEN
skipif (wsalphr.le.4)
skipif (female.eq.0)
skipif (married.eq.1)
stat wsalphr 
delete skip$

*** Part 2:

* Estimating marriage wage premium for ALL workers using OLS command
skipif (wsalphr.le.4)
ols wsalphr married
delete skip$

* Estimating marriage wage premium for MEN using OLS command 
skipif (wsalphr.le.4)
skipif (female.eq.1)
ols wsalphr married
delete skip$

* Estimating marriage wage premium for WOMEN using OLS command 
skipif (wsalphr.le.4)
skipif (female.eq.0)
ols wsalphr married
delete skip$

*** Part 3:

* Enter the values of the relevant sampe wave statistics and sample sizes from your state's CPS
* sample in the table below

stop
```
