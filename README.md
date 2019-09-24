# A-series-of-unfortunate-events
This repository is dedicated to the study of the failure rate in a multi-stage manufacturing process

### Case 1: Fail without Jamming

Consider a manufacturing process with *n* stages connected in series. Let *P<sub>i</sub>* be the probability for the *i*-th stage to generate a faulty part. 

Probability for having a faulty part: 
<img src="https://latex.codecogs.com/gif.latex?=~1-{\text{Prob~(~not~having~a~single~faulty~part~in~all~}}n{\text{~stages)}}" />
<img src="https://latex.codecogs.com/gif.latex?\Rightarrow~1-\Pi_{i=1}^{n}(1-P_i)" />
