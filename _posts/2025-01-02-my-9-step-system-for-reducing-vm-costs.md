---
title: "My 9-step System For Reducing Virtual Machine Costs"
categories:
  - blog
tags:
  - Azure
  - Cost Management
  - Virtual Machines
---

When using Virtual Machines in Azure we have many options for reducing costs. These options also boast the highest discounts. As high as 90% with options like Spot, Reserved Instances and Stop/Start automation.

We have options available for almost any Virtual Machine scenario:

Deleting the VM
Using the right series
Using the latest version
Rightsizing the VM
Rightsizing the Disk
Spot instances
Auto-shutdown
Stop/Start automation
Reservations



With many available it can be tricky to work out which are best. Something is better than nothing, but we want to really squeeze the juice out of the available savings.



To achieve this we need a system. One which:

Prioritizes non-committing options before long term commitments.
Covers all options in a logical order.
Makes committing to reservations easier.
Works for almost any Virtual Machine, Windows and Linux.
Is easy to repeat.



The system needs to cover the 3 key areas the savings options falls in. Compute, Uptime and Life Expectancy. To maximize results, we need to take a 3 phase approach:

First, we tackle compute. We want our VMs properly sized for their workload before addressing uptime and commitments.
Second is uptime. Solutions that optimise VM uptime provide the best savings, all without the need for long term commitments which keeps them super flexible. Also improves sustainability. Win-win.
Finally, we examine Life Expectancy and identify the best candidates for reservations.





The 9-Step System
The 9-step system is a simple Yes-No flow guiding us through almost every Cost Optimisation option for almost every Virtual Machine that lives in Azure.

The system covers compute first, then uptime and then reservations. This ensures we squeeze out every ounce of savings




The Summary
Not needed = Delete the VM.
Wrong Series = Change the VM Series. e.g. D-Series to E-Series
Old version = Update Version. e.g. Dsv3 to dsv5
Oversized = Resize to smaller VM
Disk SKU too high = Change the Disk SKU. e.g. Premium to Standard SSD
Can be Interrupted = Enable Spot (Batch, Sandbox, Rendering, Analytics)
Only Needed Ad-Hoc = Stop Automation (Ad-Hoc, Sandbox, Demos, Test)
Not Needed 24/7 = Stop/Start Automation (Business hours, Dev/Test)
Long Life = Reservations (Production and 24/7 Workloads)



The 9-step System detailed


Step 1 - Delete The VM
Whether idle, stopped or deallocated, if we don’t need it, delete it.

Remember we still have to pay for Disks even when a VM is deallocated. Delete the VM, Disks and all other VM components for a 100% cost reduction. Hard to beat.

If we must keep a data copy change the disk to standard HDD, take a snapshot, then delete the disk. With snapshots we only pay for used storage. e.g. 50gb used instead of the full 128gb.





Step 2- Update the VM Series
With many VM Types and Series designed for different workloads, we want to ensure Virtual Machines are correctly aligned. A correctly aligned VM compliments this whole process. A misaligned VM type will always be sub-optimal.

Is my General Purpose D-Series VM better suited to a Burstable B-Series?
Does my VM need moving to Compute Optimized, for a higher CPU-to-Memory ratio?
Should my Relational Database be running on an E-Series instead of L-Series?



Ensure the VM type matches the intended workload and make any adjustments where needed.



NOTE: When it comes to Reservations there is good incentive for limiting the variety of VM series used. Reservations apply to Virtual Machines Instance Groups, not just a single VM.

This allows for fewer, larger Reservation orders which maximizes flexibility and total VM coverage. Makes our lives easier later.





Step 3 - Update the VM Version
Azure is regularly releasing new VM versions on the latest hardware. D and E-series are now on v6, yet many VMs are running versions as far back as v2. Newer versions provide better performance for an often identical price. A free upgrade in many cases.



Upgrade all VMs to the latest versions. The free performance boost is always welcome and may be enough justify reducing the size later.



NOTE: Reservations work similarly to the VM version as they do the VM series. A reservation for a v5 will only work on a v5. Align VMs to the same version to achieve maximum flexibility.





Step 4 - Resize The Virtual Machine
With our Virtual Machines series and version optimised we can now look at resizing.

Virtual Machine size and price scales by a factor of two. Half the size, half the costs:




This can often lead to massive overprovisioning. We might only want an extra 25% compute but end up paying for significantly more.

Identify VMs that can be easy resized to a lower size. Use historical Metrics, Azure Advisor and VM Insights to help affirm decisions. We are looking for VMs that run consistently below 50%. If below 50% then it can logically be halved.

Review all VMs in all environments here. Over-provisioning Production workloads often happens and may just be wasting a lot of money.





Step 5 - Resize The Disk
Virtual Machines need Disks. Disks support several performance SKUs. Each SKU upgrade almost doubles the costs.

All too often Premium SSD is used for every disk, regardless of environment. With large VM estates this small choice can cost thousands per month. Easily justified in production. Less so in Non-Prod and Sandbox.

Review the VMs disks and ensure the SKU aligns to the VM workload and environment. Focus on Non-Prod and Sandbox environments but consider production too. You never know…





With step 5 complete our VMs should be near perfectly aligned to the workloads they serve, without negative performance impact. In fact we may even have gained performance in some areas with version upgrades.

The steps so far may have only yielded small cost savings and that’s totally fine. The biggest value from these steps is in preparing the VMs to get the most out of the massive savings from the upcoming steps.





Step 6 - Spot Instances
The uptime phase begins with Azure Spot Instances, offering up to 90% savings by utilizing unused capacity in Azure. While Spot Instances can technically run 24/7, Microsoft may evict them with minimal notice, deallocating the VM. We have no control of uptime.



High reward for high risk.



Spot instances are best suited for dev/test environments, sandboxes, and interruptible workloads such as Batch processing and Databricks—scenarios where potential interruptions won't cause significant issues.

Spot VMs can also be evicted based on price. We set a maximum price we're willing to pay, and as long as this price remains above the 'market rate' the VM will continue running.



Note that Spot instances can be deallocated and turned on just like a normal VM. Its only when a Spot instance meet it’s eviction criteria will it not be able to turn back on again.





Step 7 - Auto-Shutdown / Stop-Only Automation
We often have Virtual Machines that only need to run infrequent, ad-hoc workloads.

We can use Stop-Only Automation or Auto-Shutdown to ensure these VMs are turned off during long idle periods. This is perfect for sandboxes, Proof of concepts, and any other environments that needs to be online on an ad-hoc basis. A daily shutdown task will ensure the VM isn’t left running idle indefinitely and can keep VMs offline for the vasty majority of their lifecycle.



This simple act can reduce VMs costs to almost nothing.



We can use VM Auto-Shutdown for a quick and easy solution for stopping VMs on a daily basis. This is a bit too basic for our goals however.

Instead use VM Stop/Start solution with Azure Automation or Function Apps to provide a full flexible and scalable solution. We can simply skip the ‘start’ operation for VMs that can remain offline.

Microsoft have a Function App based Stop/Start Solution readily available on their GitHub page to help get started:

https://github.com/microsoft/startstopv2-deployments

There are other solutions available, or create your own if preferred. Stop/Start will be needed for the next step too.





Step 8 - Stop/Start Automation
Get ready for some BIG savings.

Stop/Start Automation is the super-heavyweight of all cost optimization options. The amount of Virtual Machines that fit the brief for Stop/Start automation makes it the best cost saving option available.

Any environment which isn’t 24/7 can be turned off during “off hours” and automatically back on during “on hours”. This can save tens of thousands per month!



A VM running 10 hours per day, 5 days per week reduces costs by over 70%.

Each hour a VM isn’t running reduces it’s costs by 0.6%.



Stop/Start can provide better savings than reservations, without any long term commitments. We can almost gamify this process and get as many hours of downtime as possible, with every hour reducing our costs.

Remember we maintain full flexibility of schedules and can change them whenever needed. If uptime requirements change simply adjust as needed.

Use Stop/Start Automation to turn off environments that don’t need to be running outside of business hours. Consider all environments, especially non-production.





Step 9 - Reservations
By now we have applied Stop/Start automation to VMs which don’t need to run 24/7. We now have our Virtual Machines that run 24/7. Our production workloads.

We can now look at Reservations.



The challenge with Reservations is the commitment. Purchasing compute for 1 to 3 years sounds like a long time. That’s because it is!

By performing the previous steps however, we will have built up the confidence to commit. We don’t need to buy reservations for all VMs at once. We can always start with small coverage and expand over time.

We can use the Azure Advisor to assist with decisions. Azure Advisor can help guide decisions and also provides estimated savings.



Added up this often reaches hundreds of thousands.



Also consider the expected lifecycle of the workload. If a project will end in 6 months a Reservation isn’t needed. If a project has no end date a Reservation can save hundreds of thousands over the course of the project. Even if the project does end, remember that we reserve the compute and not the VM itself. Just use the compute on another project.





Ready to save some money?
Before you do, check your last 1, 6 and 12 months spend for Virtual Machines. Be sure to include disks, they count too.



Note the figures down. Quite a bit?



Run through the system and see how much you can save.



How did you do? Leave a comment and tell your boss. He and I would like to know!