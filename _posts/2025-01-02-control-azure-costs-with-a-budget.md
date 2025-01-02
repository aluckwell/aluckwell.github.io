---
title: "Control Your Azure Costs With Budgets"
categories:
  - blog
tags:
  - Azure
  - Cost Management
---




In todays world of consumption based cloud services, the responsibility of IT costs has largely shifted to engineering teams. Afterall, they are ones directly spending in the cloud as if the company credit card is in their hands. Their decisions are often driven only by technical requirements, but their actions have both technical and financial consequences.

When financial requirements aren't clearly set impulse spending occurs. A bit more resiliency, availability and compute is all too tempting without spending limits. Why settle for ford when I can have a Ferrari?



Resources get over-sized.

Resources get over-provisioned.

New services are briefly tested, forgotten, then orphaned indefinitely.



Here's just a few examples of common technical decisions that many wouldn't even think twice about:

Globally redundant instead of locally redundant storage.
Premium SSD instead of standard SSD Disks.
Enabling diagnostics logging.
Over-sizing VMs to cover for traffic spikes.



Individually these decisions seem simple, logical. These decisions however can double resource costs and cost thousands a month wasted logging. Stack a few of these up together and they compound rapidly into hefty bills which often go unnoticed for months.



To help avoid the problem we need a mechanism for bringing resource costs into the heads of engineers. The aim isn't to set any strict rules. That would create blockers and defeat the point of the cloud. The aim is raise financial awareness, provide an easy way to track spend and ultimately build cost effective solutions.



The good news is this is an easy fix. No fancy FinOps tools or Udemy courses needed. This could be squeezed out in a lunch and learn.

 So head to portal.azure.com and perform your MFA ritual. Were going back to finance basics, with Budgets.



Budgets
A budget is a financial planning tool used to determine how much money should be spent. The great thing about budgets is they are universally known and understood, they need no introduction. Organisations and individuals use budgets continuously to manage and track their spending. Budgets are so fundamental that they are behind every financial decision.

There is a good reason budgets have been around for centuries. They truly work!



A budget:

Sets a spending goal.
Creates cost awareness during buying decisions.
Creates financial discipline.
Promotes spend tracking.
Ensures spending remains within means.
Reduces the temptation of and risk unnecessary purchases.



These benefits exist in all budgets. Simply setting a budget, even just verbally, is enough to get people thinking about costs. The same is true for a budget in Azure. An Azure budget will massively improve cost visibility, enable continuous spend tracking and notify everyone who needs to know when it's going to be exceeded.



An Azure budget:

Defines the financial requirements for a project.
Can be scoped to subscriptions or tags such as cost centre.
Tracks both actual AND forecast spend at multiple thresholds. No more nasty surprises!
Supports a variety of notification options, so nobody ever misses an alert!



Lets take a look...

To set a budget go to Cost Management > Budgets > Add:


See content credentials

I don't like the look of that forecast
First lets review the graph. Back in March we see a significant cost spike which was resolved. The spend is forecast to increase again in September, as per the darker green. Signs of a recent changes that has spiked costs and is going to get expensive...

Without a budget we rely on luck to spot these things early. Lets add a budget.

Set the scope, filter as needed.
Set the reset period to monthly.
Set the monthly budget amount.




See content credentials

Above Red line = Danger zone
If your business hasn't defined a budget or you aren't sure on the amount don't worry. Use the graph for guidance but avoid setting it too high. The above example suggests $3710 but this is a poor suggestion. We don't want a budget based on a bad forecast. $2000 is reasonable, based on the history plus room for future growth.

Whatever happens, just be sure to set something. It can always be tweaked later.



We should now have a budget, great! But we need more than a red line on a graph. Red lines need to make some noise! Lets move on to alerts.



Alerts
This is where the real magic starts to happen. An alert is an immediate call to action to key stakeholders. “You need to look at this!”.

Who are the Stakeholders? Me? My team? My boss? Finance?

Well… we all are….

Managing cloud cost these days is a shared responsibility. When gifted the power to create services that will cost the organisation money, we need to be responsible with spend.

A budget alert can have multiple trigger conditions based on the forecast cost, actual cost and the % intervals. The aim here is to notify stakeholders before budgets reach 100%.



For this we need:

At least one actual alert lower than 100%. To tell us we are “this close” to budget. A good approach is 25, 50, 75% which tracks well against the four weeks in every month.

A forecast alert of 100%. To tell us we are forecast to exceed budget.

An actual alert at 100%. Telling us we’ve exceeded budget.

Lets set these in the Alert Conditions:




See content credentials

Notice how the budget is exceeded since the last screenshot? I was slow to set a budget and even slower investigating the cost spike. This cost me 500 bucks...
We now need to set some notifications. It is essential that these alerts reach those who can take action, or rally others who can.

We have two options. Email recipients and Action Groups:

Email recipients are an easy starting point, though not very flexible. Add email addresses for all key stakeholders and will be emailed when each criteria is reached.
Action Groups massively expand notification options to SMS, voice, push notification, Email Azure Role members, logic apps, webhooks and runbooks. Each budget alert can use a seperate action group with it's own unique preferences. Your notification options are practically limitless and completely customisable. They require a bit more work but are completely worth it!



Action Groups
Lets say we want to email subscription owners and contributors when all budget intervals are reached. This will help them easily track costs throughout any month. We can use the ‘Email Azure Role’ notification preferences in Action Groups to ensure they are all notified.

For the 100% Forecast and Actual Budget notifications we additionally want this to reach an escalation point, such as the Head of IT or member of the Finance Team. Here we could add their direct email addresses.

For this example, four Action Groups will be used for flexibility at each threshold:


See content credentials



Go to Azure Monitor > Alerts > Action Groups > Create New.

Work through the steps, on the Notifications Tab add the notification preferences for each of the budget alerts.
The Actions tab is for Logic Apps, Function Apps and other automated actions. Not immedietely needed, but good to explore another time.


See content credentials

Repeat until each budget alert has the Action Group and notification preferences it needs:


Each alert with an Action Group assigned.


Save all the things, job done!



By now we should have a reasonable budget and several alerts at different intervals which will inform all key stakeholders depending on severity.

This will:

Improve visibility into cost consumption moving forward.
Provide ongoing tracking of cloud spend without much manual effort. Threshold alerts will do this for you.
Show spending patterns and cost spikes.
Allow us to take action before a budget gets exceeded.
Promote conversation and collaboration between finance and IT, including agreements on budget increases when justified.



Not bad for an hour of work.



But wait, there's more...



Anomaly Alerts
Whilst Budgets track spend consumption against an overall high-level financial target, Anomaly Alerts monitor for cost fluctuations on Resource Groups and provide notifications for:

New costs introduced, like a new VM.
Removed costs, like a deleted or deallocated VM.
Changes in costs, such a VM resized to a larger or smaller SKU.



Cloud pricing is complex and erratic. A change to one resource can affect the costs of another. It's hard to predict the true cost ahead of time.

With anomaly alerts we don't need a crystal ball. Instead, Azure alerts us of a cost change around 24-36 hours after it occurs. We can simply verify the change is expected.

Did a planned change recently occur?

Is the cost what we expect?

If these are both "yes" then great! No surprises. If "no" then we can deal with it before they eat into our budgets.



Let look at an example:


See content credentials

The result of 8 vCPU VMs when they should have been 2 vCPU.
The alert shows us the top five Resource Groups by cost changes, both up and down. Immedietly we can see a significant cost spike on the top Resource Group.

Was a change expected? Yes.

Should this change cost this much? Absolutely not!



Anomaly Alerts flesh out these things long before they cause a larger problem. Knowing within 24 hours rather than several weeks can save thousands in accumalated costs.



Go to Cost Management > Cost Alerts > Add:

Check that 'anomaly alert' is selected.
Add email addresses for teams or users making changes. Only supports email today sadly.
Add optional message.
Create.




See content credentials

All done! Within five minutes of work we have an almost guaranteed method for saving hundreds, even thousand in costs!





That's it!

A couple of hours of work to implement some of the most powerful financial tools in the battle against cloud cost struggles. These WILL improve visibility, create financial discipline and control costs for the long term.



If you don't have these today, set them up today!



Be sure to cover every subscription, cost center and project. We want every resource covered and accounted for to maximise the benefits.





What next?
If you've setup budgets already and want to further customise notifications and add additional automation, check out: Azure Logic Apps

Automate budget deployments at scale with Azure Policy, never miss a budget again. The exact policy for this is here: Azure Policy for Deploying Budgets at scale



If you want to explore the documentaion on Budgets, Anomaly Alerts and Cost Management in general check out the below links:

Azure Cost Management

Azure Anomaly Alerts

