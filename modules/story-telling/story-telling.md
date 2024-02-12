19
Data Storytelling and Automated Reporting/Dashboarding
The skills we've learned so far are important and useful, but often we will need to communicate results to others. Without this communication, the results of our analysis aren't of much use. If the results of our work are more analytic in nature (such as descriptive statistics like standard deviation and histograms), it helps to use data storytelling techniques. Presenting information through a story makes it much more memorable than rattling off a list of statistics. For example, the memory palace technique (where numbers are put into a story) is used by world champion memorizers to remember huge series of arbitrary numbers. Additionally, several people and some studies suggest that emotions are more important than facts in decision making. So, if we are presenting results to a decision maker in our organization, it is usually more effective to tell a story with the data and results rather than simply dump a plethora of numbers on our audience. In the first part of this chapter, Data Storytelling, we'll cover some principles of data storytelling and how we can use it.

In the second part of the chapter, we'll look at using automated reporting to generate a data story. This can be done in several ways, including Python packages such as FPDF, Streamlit, Plotly Dash, and others. There are several other tools out there that can be used independently of Python or with Python, but tend to require a subscription or license fee, such as ReportLab, Tableau, Excel, RapidMiner, and other data science GUIs.

Let's get started by learning about data storytelling and how we can make use of it.

Data storytelling
Data storytelling is a good tool to have in your kit as a data scientist. We'll always need to communicate our results to stakeholders, and using a story is a much better way to communicate something than a list of statistics. To create our data story, we need our data, our visualizations, and our narrative. We've already seen how to take data and create visualizations throughout the book, especially in chapter 5 on EDA and visualization. However, putting together a story and narrative around the data is primarily what's new here.

The steps we'll consider here are:

Consider your audience and the message you are trying to convey
Support your message with your findings, and lead up to your central message or insight
End with some sort of call to action or a recap of your main insight(s)
The first things to consider are our audience and the message we are trying to convey. It's important to consider the technical level of our audience so we know how much we need to explain and how much to simplify our results and visualizations. If we have a more technical audience, like a group of experienced data scientists, we don't need to explain the basics of machine learning. But with executives who may not be ML experts, we probably need to simplify our message somewhat and may need to explain some of the key points of machine learning.

Next, we want to have a central message and insight we want to convey. This central message or insight should also ideally lead to some sort of action. In the example we'll use soon, our dataset will be a credit card default (missing a payment) dataset. We will be conveying which features are most predictive for defaults and if our ML model is ready for deployment. As part of the story, we'll explain what makes the model ready or not ready, such as a lack of data. Our call to action will be a decision from executives and managers on the deployment of our model or authorization for more data collection to improve the model. It's OK to have some other results included, especially if that helps to tell the story, but we want to avoid minor details. For example, we're not going to go over all the approaches that didn't work (such as the ML models that didn't work well) in our data story. However, if a feature engineering step made a big difference in improving the performance of our model, it could be worth including in our story.

In some settings, there isn't necessarily a call to action. One example may be presenting results from a project to peers with the goal of knowledge sharing. In those cases, we can recap our central results at the end of the presentation rather than using a call to action.

Lastly, we need to make visualizations and graphics to tell our story. This should almost completely consist of plots. But, if we have single numbers (for example, an accuracy number or other performance metrics), we can put those in a large, eye-catching fashion, such as using a large font size and making the text bold. However, for a collection of many numbers (such as a time series dataset), it's much better to use visualizations. In the case of a time series dataset, for example, a line chart is often best. If we have a table of data, it's best to put that in the appendix if we must include it, and to only include the relevant important numbers earlier in the presentation. These visualizations and graphics will be used to support and build up to our central message.

With visualizations, the best practices we covered in Chapter 5, Exploratory Data Analysis and Visualization, still apply:

Avoid chart junk
Use color sensibly
Present data properly (for example, line charts for time series data)
Make charts "redundant" in case they are printed in black and white and for the colorblind
Clearly label axes, datasets, and use a single font size with a sans-serif font
Tailor your visualizations to the audience
The only best practice that could be partially avoided is the black and white redundancy issue. If we are presenting the data in a PowerPoint presentation and know that colors can be used, for example, we don't have to worry so much about redundancy. However, we should take care to avoid using colorblind-unfriendly colors (such as red and green for line colors in the same plot).

An aspect that can differ with storytelling versus creating general visualizations is that we can use visual techniques to highlight plot areas to draw the audience's attention there. For example, if we want to indicate that a certain point on a scatterplot is the most important, we can make it a different color or change the pattern of it (for example, make it larger and a different shape than other points).

When telling our story, we need a strategy for getting our point and supporting details across. One way that has been devised by Brent Dykes (described in his book Effective Data Storytelling) is to use a four-part structure that he calls the Data Storytelling Arc:

Setting: Background and hook (and preview of the key insight if needed)
Rising insights: Supporting details that lead up to the key insight
Key insight: The main finding
Solution and next steps: Options and recommendations for action
In the first step, the setting, we provide a background and something to draw the audience in – the hook. This should be something new or interesting that gets the audience's attention, such as a problem with sales or manufacturing numbers, or in our case, a problem with credit card default rates. If the audience is mainly composed of busy executives, we may want to provide a preview or spoiler of the main result of the key insight. This acts as a more potent hook that can draw people in but takes away from any suspense that may be built during the story. You may find some people in management positions tend to not like suspense when data and results are being presented to them. In other settings, such as a conference, the suspense and related storytelling pattern may be more appropriate. If we provide the spoiler to an executive, they may decide they want to hear more or want to skip the rest of the report or presentation. After our setting and hook, we bring any supporting data and visualizations into the picture as necessary. If there was a crucial data cleaning or feature engineering step, or a mini-insight, we could include that here. Next is the key insight, which is our main message. Finally, we wrap up with any options or recommendations for the next steps and actions to take.

Let's look at an example of using data storytelling with the end goal of getting a team of executives to approve the deployment of a machine learning system.

Data storytelling example
For this chapter, we'll use the credit card default dataset we used in earlier chapters and will pretend we're working for the bank that is offering the credit card. Our task is to use machine learning to predict credit card defaults and to help reduce the default rates. The audience, in this case, will be the executives of the bank and our manager, to whom we want to present our results. First, let's load the data:

import pandas as pd
df = pd.read_excel('data/default of credit card clients.xls',
                   skiprows=1,
                   index_col='ID')
This data has a "default payment next month" column, which is our target with binary values. As usual, we want to familiarize ourselves with the data by doing some EDA (which is easy with pandas-profiling). From this, we notice that the PhiK correlations show strong correlations between late payments in previous months (for example, PAY_0 with the target column). We can create a plot of the PhiK correlations to use in our "rising insights" section:

import phik
phik_corr = df.phik_matrix()
sns.heatmap(phik_corr)
Next, we can create a bar plot to show the differences between the default and no default groups for the PAY_0 column, since this one is most correlated with the target:

import matplotlib.pyplot as plt
plt.ylabel('percent')
sns.barplot(data=df,
            x='PAY_0',
            y='PAY_0',
            hue='default payment next month',
            estimator=lambda x: len(x) / len(df) * 100)
Now, we can train a classification model with pycaret:

import pycaret.classification as pyclf
setup = pyclf.setup(data=df, target='default payment next month')
best_model = pyclf.compare_models()
tuned_model = pyclf.tune_model(best_model, search_library='scikit-optimize')
We first set up our autoML environment with pycaret, using the default settings, which detects the PAY_0 column and several other columns as categorical columns (meaning it one-hot encodes them). In our data story, we don't need to describe this one-hot encoding process since it's not such a crucial detail for our main message. We then tune the model to optimize the hyperparameters to maximize the accuracy. For now, we will stick with reporting accuracy since our audience is not composed of data science experts, but we may actually want to optimize something like the recall of the payment default class (to maximize the number of default payments we detect). Our best model here is a Ridge classifier, although a few others had nearly identical accuracy of around 82%.

Next, we can generate a feature importance plot and a confusion matrix with pycaret:

pyclf.evaluate_model(tuned_model)
We need to click on the feature importance and confusion matrix buttons in the resulting output to get the plots. These plots could be used as an appendix or extra information if people have more questions. Now we can put together our story.

As a background and hook, we might talk about how 22% of our customers defaulted in the most recent payment month (which we can see from df['default payment next month'].value_counts(normalize=True)). This is costing  the bank and customers money and causing problems. It would be a win-win if we could detect payment defaults early and work with customers to develop a payment plan, or decrease the credit limit of defaulting customers.

If we could come up with some specific numbers on how much money the bank could potentially save by something like looking at the median value of default payments across all customers, that would make a good hook as well. If we have busy executives who want to hear the punchline right away, we can tell them our ML model has an accuracy of 82% and can be tuned to detect more payment defaults if we wish. Assuming our executives want to hear more after seeing the spoiler, we continue.

Next, we build up our story with the "rising insights." We start with the PhiK correlation plot. Note that we also used a bright blue box to highlight the important part of the plot we want to draw the audience's attention to. This could be complimented by a bright blue arrow pointing the box as well.


Figure 19.1: A heatmap showing the PhiK correlation of our default payment dataset

Our story with this plot would be something like this: in this plot, brighter colors denote higher correlations – in other words, two variables that change together more strongly have brighter colors in the plot. We can see our target column, "default payment next month," is on the bottom row and far-right column of the plot, and the blue box highlights the area of interest. The PhiK correlations between a default payment are strongest with the PAY_0 column, which is a categorical variable with values of 0 or less than 0 for on-time payments and greater than 0 for the number of months the payment is late.

We can see that as the months get farther from our current month (for example, PAY_1 is 2 months before our current month), the correlation weakens. Looking at this PAY_0 feature, we can see that people with default payments tend to more often have a late payment.


Figure 19.2: A bar plot of the PAY_0 column, separated by the default payment status. The negative values are other payment methods, such as revolving credit.

The above plot shows that most people are not defaulting, since the total size of the non-defaulting bars is bigger. We can also see that most non-defaults are 0 months late. The -2 and -1 values denote non-late payments via means such as revolving credit. Looking at the default payments, we can see that a higher proportion has late payments, usually by 1 or 2 months. This correlation of previous late payments to a default payment in the current month can be used to predict if someone will default on a payment.

Next, we discuss our main takeaway or result/insight: we use automatic machine learning, or autoML, to find and optimize the best ML model for the problem and achieved an accuracy of 82%. This is good but only slightly better than the 78% fraction of customers who don't default. However, we can tune the model to be more selective and accurate at predicting defaults at the cost of some false positives (where we predict non-defaults as defaults). From our confusion matrix and recall score, we can see we are only identifying about 1/3 of the defaults. We also found from looking at the feature importances that the most recent month's payment status and extremely late payments from previous months tend to strongly relate to the default rate.

We can see how some of the more important features relate to the distribution of defaults in the data with pandas filtering like this:

df[df['PAY_5'] == 6]['default payment next month'].value_counts()
Finally, we want to give the solution and next steps: we can use this model to predict payment defaults. Depending on the cost of dealing with the default, we can tune our model to more accurately predict defaults at the cost of more false positive predictions of non-defaults as defaults. So, if we want to simply send out an email to customers providing potential solutions for avoiding a default payment if they are at risk, we can afford more false positives. If someone is going to hand-review the default predictions, then we may want to avoid having too many false positives. Additionally, it will be helpful to work more closely with the data team to gain access to more data, as this should improve the performance of the ML algorithm. We will also need to create a data engineering pipeline to feed into the ML algorithm in deployment.

In this last step, we summarized what we can do going forward and proposed some solutions to deploying our model in production, and the decision is up to management now.

Data storytelling can be a powerful way to convey a message and convince others to take the path you think is best. However, we haven't covered all the details of data storytelling here. We did cover several of the important visualization topics in Chapter 5 on EDA and visualization, though. Still, it's not a bad idea to read up more on data storytelling. There are at least two good books on the topic worth reading: Effective Data Storytelling, by Brent Dykes, and Storytelling with Data, by Cole Nussbaumer Knaflic.

The storytelling methodology we covered here is best suited for written reports, presentations, and infographics. Another few useful ways to present data to those who need it are automated reporting and dashboarding.



Referenz:
https://learning.oreilly.com/library/view/practical-data-science/9781801071970/Text/Chapter_3.xhtml#_idParaDest-87