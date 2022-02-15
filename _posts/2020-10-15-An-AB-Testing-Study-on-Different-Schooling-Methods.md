---
layout: post
title: "An A/B testing Study on different schooling methods based on fMRI data"
subtitle: "Which schooling method is better ? Montessori Education or Traditional Education?"
background: '/img/posts/montessori/mon_bkg.jpg'
# image: "/img/posts/web-scraping/imdb.png"
---

<!-- # An A/B testing study on different schooling methods based on fMRI data

## Which schooling method is better ? Montessori Education or Traditional Education ? 

 
Qingwen Wang -->


## Study Description: 

The study I am interested in is “An fMRI study of error monitoring in Montessori and traditionally-schooled children”. [https://rossier.usc.edu/files/2020/07/fmri-study-error-monitoring.pdf](https://rossier.usc.edu/files/2020/07/fmri-study-error-monitoring.pdf). It discusses which kind of students learn better over time, the students who are focused on monitoring their own learning process, or the students who are focused on getting right answers. The unit in this study is 8-12 year-old students from Montessori schools and students educated in traditional schools. Students in the study were asked to solve math problems while an fMRI tracking brain activity. The researchers evaluates potential learning outcomes by both brain activity and students’ quiz answer. Only Montessori students showed coherent changes in brain activity following errors, suggesting that they were engaging with the errors strategically to learn. Traditionally-schooled students, by contrast, showed coherent activity only after correct answers, and the activity pattern suggested that they were trying to memorize that event. Though both groups got the same number of problems right, the Montessori students skipped far fewer and got more wrong, making them learn the task more efficiently by the end. This study gives the conclusion that Montessori-schooled students will learn better over time.

*Y^1*: the potential learning outcomes for students from a Montessori school
*Y*^0: the potential learning outcomes for students from a traditional school <br>
*D*:  taking schooling method of Montessori pedagogy 



## Possible bias:

Family’s economic status can be a factor causing selection bias. Since Montessori school usually has a higher tuition fee than the tradition public school so that family with a worse economic status are less likely to send their children to a Montessori school. So this selection bias will cause the potential learning outcomes to be better, NATE to be higher. *NATE = ATE + Selection bias(positive in this study) + differential bias*. Besides this selection bias, there also could have other problems that may cause bias, such as: children’s intelligence and anxiety, or home pedagogical environment, etc.

## Simple simulation:

The original study evaluate both math quiz outcomes, and brain activity tracked by fMRI. To simplify, here I only simulate the math quiz outcomes. In the original study, there are total 32 participates from different family, and these children are educated in a Montessori school or a traditional school; for math quiz performance, the overall efficiency was higher in Montessori students than in traditionally-schooled students, *M_m* = 3.26, *M_t* = 2.46. Each student has a different family economic status, and family with higher economic status will have higher probability to send their children to a Montessori school. 

So, here I set sample size 3200 ( for a more intuitive graphing of bias and ate); ATE as 0.8; family economic status as a variable causing the selection bias; classify different ‘econ_status’ into different groups:  1)<25%: low; 2)25%~75% :medium;  and 3) >75%: high.

*Yi*0 =total CVD events in the control group (no exercise) <br>
*Yi*1 = total CVD events in the treatment group (do exercise) <br>

<img src="https://paper-attachments.dropbox.com/s_79FE757E816185CBAE89875D215639F3089DEBD90FADED6AE07C9E66C3A79EB4_1603080678000_image.png" width="100%">
<!-- ![](https://paper-attachments.dropbox.com/s_79FE757E816185CBAE89875D215639F3089DEBD90FADED6AE07C9E66C3A79EB4_1603080678000_image.png)width="100%" -->

##  Simulate selection bias
In the picture, we can observe that the blue shade is not totally overlapped by the yellow shade, which means the density of *Y^0* when D=1 is not same with the density of *Y^0* when D=0; so that these two groups do not have the same probability to donate even there is no treatment, selection bias exists. 
    
<img src="https://paper-attachments.dropbox.com/s_79FE757E816185CBAE89875D215639F3089DEBD90FADED6AE07C9E66C3A79EB4_1603080703670_image.png"
width = "100%">

    
Also, we can find the selection bias from a mathematic way: <br>
*NATE* = E[Y^1|D=1] - E[Y^0|D=0]= 1.31; <br>
SelectionBias = E[Y^0|D=1] - E[Y^0|D=0] = 0.51; <br>
ATE = 0.8; <br>
Differential bias = 0 <br>
From the formula, we can get the the selection bias is 0.346, derived from the different economic status.

## Simulate an experiment
Perfect stratification is a good method to remove bias. This means that we will stratify the data into several subgroups (strata). "Perfect" means that we can put each person in the experiment into exactly the right group such that all selection bias is accounted for. With the data split into several strata, we will get a separate estimate of the ATE within each one. Then we will average together the estimates of each of the strata. Besides perfect stratification, regression can also be a convenient tool to implement a stratification. In this case, we can get the correct result by including a dummy variable for each economic status label.

a) Regression (y ~ d) result without stratification: 
ATE = 1.3
    
<img src="https://paper-attachments.dropbox.com/s_79FE757E816185CBAE89875D215639F3089DEBD90FADED6AE07C9E66C3A79EB4_1603080767162_image.png"
width = '100%'>

    
b) Regression (y ~ d + econ_status_label) result with stratification: 
ATE = 0.8

<img src="https://paper-attachments.dropbox.com/s_79FE757E816185CBAE89875D215639F3089DEBD90FADED6AE07C9E66C3A79EB4_1603080875667_image.png"
width = "100%">

Thus, we identify our ATE by removing bias through regression method.
<img src="https://paper-attachments.dropbox.com/s_79FE757E816185CBAE89875D215639F3089DEBD90FADED6AE07C9E66C3A79EB4_1603133141985_image.png"
width = "100%">

## Simulating hypothesis tests
****
Two sampling method: <br>
1) split treatment and control share by 50/50; <br>
2) split treatment and control share by 20/80; 

From the table below, both ‘p_reject’ are around 0.05( alpha is set to be 0.05), so the false positive rate is correctly controlled.

<img src="https://paper-attachments.dropbox.com/s_79FE757E816185CBAE89875D215639F3089DEBD90FADED6AE07C9E66C3A79EB4_1603137117123_image.png"
width = "100%">

<img src="https://paper-attachments.dropbox.com/s_79FE757E816185CBAE89875D215639F3089DEBD90FADED6AE07C9E66C3A79EB4_1603137536271_image.png"
width = "100%">

Compare two simulation results: <br>
1) treatment_share = 0.2 , N = 100, 500, 1000, power increase from 0.224 to 0.967;   <br>
2) treatment_share = 0.5 , N = 100, 500, 1000, power increase from 0.348 to 0.998;  <br>
And from the plot, we can observe that when treatment share = 0.5, the power is always much greater. So 50/50 is a good sampling to method to both control false positive rate and increase power.

<img src="https://paper-attachments.dropbox.com/s_79FE757E816185CBAE89875D215639F3089DEBD90FADED6AE07C9E66C3A79EB4_1603135741066_image.png"
width = "100%">

<img src="https://paper-attachments.dropbox.com/s_79FE757E816185CBAE89875D215639F3089DEBD90FADED6AE07C9E66C3A79EB4_1603136802071_image.png"
width = "100%">

Compare two sampling methods: <br>
Method 1, splitting the treatment and control for 20/80. 
The advantage is that we can have less participates in the treatment group, that we can save experiment cost. And if the treatment effect is uncertain, maybe negative, we can lower our risk as much as possible. The disadvantage is that, our experiment will play less power so that we will have less confidence in our results if there is truly treatment effect.  

Method 2, splitting the treatment and control for 50/50. 
The advantage is that we can get higher power in experiment, and we can be more confidence to make a final decision. However, the cost is that we need more people to take treatment, which leads to higher cost. 


## Power calculation

Power calculation result:

<img src="https://paper-attachments.dropbox.com/s_79FE757E816185CBAE89875D215639F3089DEBD90FADED6AE07C9E66C3A79EB4_1603139741022_image.png"
width = "100%">

<img src="https://paper-attachments.dropbox.com/s_79FE757E816185CBAE89875D215639F3089DEBD90FADED6AE07C9E66C3A79EB4_1603139853465_image.png"
width = "100%">


So the result matches with our previous experiment result. <br>
Four combination of alpha and power: alpha = 0.05 or 0.1,  power = 0.8 or 0.9.<br>

Usually,  the power can increase at the cost of the higher false positive rate. Each combination has its own advantage and disadvantage. To take which combination depends on if you care higher power more or lower false positive rate. Also, how much sample size you can get can also determines which combination is more feasible for your experiment. <br>

If we take ATE = 0.8, alpha  = 0.05, power = 0.8, we can choose sample size N as 52(26 in each group) that our power can reach 0.8.
When we want to increase power or decrease false positive rate we may need to increase sample size.


## Run the experiment
<img src="https://paper-attachments.dropbox.com/s_79FE757E816185CBAE89875D215639F3089DEBD90FADED6AE07C9E66C3A79EB4_1603141398828_image.png"
width = "100%">

From the regression result, the coefficient of ‘D’ is 0.78 which is near to ATE = 0.8 . The standard error is 0.028, which means the variation is small. P-value is 0, it is significantly less than alpha = 0.05, we can be confident to say that there is treatment effect in our experiment. And the confidence intervals is 95% which indicates that the true treatment effect lies have 95% probability of lying between 0.729 and 0.839.

We do this experiment to verify whether Montessori students  truly performance better in academic than traditionally-schooled students. So we design this experiment by adding possible covariance into it to check if bias really exists, does Montessori teaching method will still have such high effect? Thus, we do regression on different economic status( low, medium, and high). From the regression result,  we can see that when family economic status takes accounts in the study, p-value is less than 0.05, the ATE is 0.78, a little bit lower than 0.8, so we can reject the null, and conclude that there is treatment effect.

My experiment so lucky that it is a true positive one, since we correctly reject the null hypothesis that no effect exist, but there is actually treatment effect with ATE very close to 0.8. But for this study, the possible flaw is that the sample size is too small, if we can have more participates in, the result will be more reliable.


## Rerun the experiment with ATE = 0 
<img src="https://paper-attachments.dropbox.com/s_79FE757E816185CBAE89875D215639F3089DEBD90FADED6AE07C9E66C3A79EB4_1603143147305_image.png"
width = "100%">

From the regression result, the coefficient of ‘D’ is 0.01 which is near to ATE = 0 . The standard error is 0.028, which means the variation is small. P-value is 0.566, it is larger alpha = 0.05, so that we cannot reject the null hypothesis which states that there is no treatment effect in our experiment. And the confidence intervals is 95% which indicates that the true treatment effect lies have 95% probability of lying between -0.071 and 0.039. The conclusion is that we accept the null hypothesis that there is no treatment effect.

We do this experiment to verify whether Montessori students  truly performance better in academic than traditionally-schooled students. So we design this experiment by adding possible covariance into it to check if bias really exists, does Montessori teaching method will still have such high effect? Thus, we do regression on different economic status( low, medium, and high). From the regression result,  p-value is larger than 0.05, and coefficient of ‘D’ is close to zero, so that we cannot reject the null hypothesis.

This experiment is unlucky because we cannot reject the null hypothesis that no effect exist, while we want to find Montessori schooling method makes effect.



    

