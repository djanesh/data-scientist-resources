# Glass door interview Questions 
https://www.glassdoor.com/Interview/data-scientist-interview-questions-SRCH_KO0,14.htm

1. Data Scientist at Yammer was asked...	Apr 5, 2013  
You are compiling a report for user content uploaded every month and notice a spike in uploads in October. In particular, a spike in picture uploads. What might you think is the cause of this, and how would you test it?  
**Ans a.** Hypothesis: the photos are Halloween pictures. Test: look at upload trends in countries that do not observe Halloween as a sort of counter-factual analysis.  
Ans b. We cannot say what has caused the spike since causal relationship cannot be established with observed data. But we can compare the averages of all the months by performing a hypothesis testing and rejecting the null hypothesis if the F1 score is significant.  
2. Three data structure questions: a) Difference between linked list and array b) The difference between stack and queue c) Describe hash table 
3. How would you test if survey responses were filled at a random by certain individuals, as opposed to truthful selections ?
**Ans a** I would design the test in a way that certain information is asked two different ways. if two answers disagree with each other I would seriously doubt the validity of the answers.  
**Ans b** This is a very basic psychometrics question. Calculate Cronbach's alpha for the survey items. If it is low (below .5), it is very likely that the questions were answered at random.
4. Data scientist as Facebook was asked : You're about to get on a plane to Seattle. You want to know if you should bring an umbrella. You call 3 random friends of yours who live there and ask each independently if it's raining. Each of your friends has a 2/3 chance of telling you the truth and a 1/3 chance of messing with you by lying. All 3 friends tell you that "Yes" it is raining. What is the probability that it's actually raining in Seattle?  
**Ans a** Bayesian stats: you should estimate the prior probability that it's raining on any given day in Seattle. If you mention this or ask the interviewer will tell you to use 25%. Then it's straight-forward: P(raining | Yes,Yes,Yes) = Prior(raining) * P(Yes,Yes,Yes | raining) / P(Yes, Yes, Yes) P(Yes,Yes,Yes) = P(raining) * P(Yes,Yes,Yes | raining) + P(not-raining) * P(Yes,Yes,Yes | not-raining) = 0.25*(2/3)^3 + 0.75*(1/3)^3 = 0.25*(8/27) + 0.75*(1/27) P(raining | Yes,Yes,Yes) = 0.25*(8/27) / ( 0.25*8/27 + 0.75*1/27 ) **Bonus points if you notice that you don't need a calculator since all the 27's cancel out and you can multiply top and bottom by 4. P(training | Yes,Yes,Yes) = 8 / ( 8 + 3 ) = 8/11 But honestly, you're going to Seattle, so the answer should always be: "YES, I'm bringing an umbrella!" (yeah yeah, unless your friends mess with you ALL the time ;)
**Ans b** 
5. Write a function that takes in two sorted lists and outputs a sorted list that is their union. (Merge sort problem)
