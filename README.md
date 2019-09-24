# A-series-of-unfortunate-events
This repository is dedicated to the study of the failure rate in a multi-stage manufacturing process

### Case 1: Fail without Jamming

Consider a manufacturing process with *n* stages connected in series. Let *P<sub>i</sub>* be the probability for the *i*-th stage to generate a faulty part. 

Probability for having a faulty part:  
<img src="https://latex.codecogs.com/gif.latex?=~1-{\text{Prob~(~not~having~a~single~faulty~part~in~all~}}n{\text{~stages)}}" />  
<img src="https://latex.codecogs.com/gif.latex?\Rightarrow~1-\Pi_{i=1}^{n}(1-P_i)" />  

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
