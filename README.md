# A-series-of-unfortunate-events
This repository is dedicated to the study of the failure rate in a multi-stage manufacturing process

### Case 1: Fail at least once

Consider a manufacturing process with *n* stages that are connected in series. Let *P<sub>i</sub>* be the probability for the *i*-th stage to generate a faulty part. 

Probability for having a faulty part:  
<img src="https://latex.codecogs.com/gif.latex?=~1-{\text{Prob~(~not~having~a~single~faulty~part~in~all~}}n{\text{~stages)}}" />  
<img src="https://latex.codecogs.com/gif.latex?\Rightarrow~1-\Pi_{i=1}^{n}(1-P_i)" />  

Here is the Matlab code for showing the probability of having a faulty part under different values of *n*.

```
close all
clear all
clc

n=1:100; %number of stages
P_i=0.02; % probability to generate a faulty part

P_faulty=zeros(1,max(n)); %Probability for having a faulty part in systems with different values of n

P_faulty(1)=1-(1-P_i)^1;

for i=2:max(n)
  P_faulty(i)=1-(1-P_i)^i;
end

P_heuristic=zeros(1,max(n));

P_heuristic(1)=1*P_i;

for i=2:max(n)
  P_heuristic(i)=i*P_i;
end

figure(1);
hold on;
plot(n,P_faulty,'r','DisplayName','Probability of having at least 1 faulty product');
plot(n,P_heuristic,'b','DisplayName','Probability (A heuristic estimate)');
xlabel('n');
ylabel('Probability');
ylim([0 1]);
legend;
hold off;

```


Here is the Matlab code for finding the maximum number of stages for the heuristic estimate to stay valid (within the give tolerance).

```n=1;
P_i=0.02; % probability to generate a faulty part
epsilon=0.01; % tolerance


while abs(1-(1-P_i)^n-n*P_i)<=epsilon
    n=n+1;
end

disp(['The max number of stages is: ', num2str(n-1)]);
```

### An alternative expression

Now consider the case that whenever a stage fails, the product will be considered as a faulty product immediately. Denote <img src="https://latex.codecogs.com/gif.latex?=\bar{P_i}=1-P_i" />.  

Under such a condition, the probability of having a faulty part :  
<img src="https://latex.codecogs.com/gif.latex?=P_1+\bar{P_1}P_2+\bar{P_1}\bar{P_2}P_3+\cdots" />  
Suppose all <img src="https://latex.codecogs.com/gif.latex?P_i" /> are the same, we have  
<img src="https://latex.codecogs.com/gif.latex?=P_i+\bar{P_i}P_i+\bar{P_i}\bar{P_i}P_i+\cdots+\bar{P_i}^{n-1}P_i" />  
<img src="https://latex.codecogs.com/gif.latex?=P_i(1+\bar{P_i}+\bar{P_i}^2+\cdots+\bar{P_i}^{n-1})" />  
<img src="https://latex.codecogs.com/gif.latex?=P_i(\frac{1-\bar{P_i}^{n}}{1-\bar{P_i}})" />  
<img src="https://latex.codecogs.com/gif.latex?=1-\bar{P_i}^{n}" />

Which is the same as case 1.

