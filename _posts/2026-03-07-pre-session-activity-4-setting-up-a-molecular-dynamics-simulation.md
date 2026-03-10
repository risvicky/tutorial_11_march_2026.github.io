
## Context
You have read the materials on molecular dynamics concepts and workflow. 

Now, you will perform a molecular dynamics simulation using open-source software GROMACS.

Have you ever wondered why water dissolves salt?

What happened inside this system?

We could model this phenomenon with an MD simulation. 

## What you should do

Discuss with your group how you would set up your MD simulation, and write your step-by-step instructions for setting up the simulation using this [template]({{ '/file/template_setting_up_simulation.doc' | relative_url }}) (right click to download and save it).

Rename the file by this format: group_name_setting_up_simulation.doc and submit it a week before the Tutorial 2 is conducted.
Feedback and comment will be returned 2 days after the submission. 

This series of questions will help you set up your simulation.

1. Choose any type of cation and anion that you want to simulate!
    - In the previous tutorial, Tutorial 1, you have learnt to draw an ion or molecule, you can use that knowledge to build your system.

2. You will solvate your system in water molecules. How would you proceed to do that?
    - For the same condition, let's use a cubic box of 3.5 nm in each direction (x, y, z).

3. You need to describe the interactions between different atoms and molecules in your system. How would you proceed to do that?
    - In the previous tutorial, Tutorial 1, you have learnt about the parametrisation routine; you can use that knowledge to describe the interactions in your system.
    - There are several ways to model water, a helpful article related to this [here](https://pubs.acs.org/doi/10.1021/acs.jcim.1c00794)

4. Now that you have all the information about your system, how would you bring your system into a more favourable state so that the forces between them are reasonable?

5. How do you check that your system has now reached a more favourable state?
    - You should use VMD in part and consider other approaches as well.

6. You need to run the simulation until the stationary state (equilibrium) is reached (energy redistribution). How would you proceed to do that?
    - In the reading material, we have talked about different thermodynamic ensembles. 

7. Now, you need to continue the simulation over a desired timescale and collect measurements. How would you proceed to do this?

8. How would you analyse the trajectory output files you get from the simulations?

### References
References are incorporated appropriately throughout the step-by-step instructions through the use of in-text citation.

## Restricted use of generative AI tools only for this assignment
You may use generative AI to help your understanding and for troubleshooting. However, you **may not** use it to generate data or responses to questions.

Remember that this tutorial accounts for 25% of your module mark, so try your best and submit your work on time to maximise your chances of achieving a high score.
Please ensure you submit all necessary files and materials in the **correct format**.
Failure to do so will result in points being deducted.

## Question Forum 
If you have any questions related to this activity, you can write your question on this whiteboard [here](https://padlet.com/risnitalistyarini/question-forum-4v2mzxuc9q03mgyc)
<div class="padlet-embed" style="width:720px;height:480px; border:1px solid rgba(0,0,0,0.1);border-radius:2px;box-sizing:border-box;overflow:hidden;position:relative;max-width:100%;"><p style="padding:0;margin:0;width:100%;height:100%"><iframe src="https://padlet.com/embed/4v2mzxuc9q03mgyc?play=1" frameborder="0" allow="camera;microphone;geolocation;display-capture;clipboard-write;clipboard-read" style="width:100%;height:100%;display:block;padding:0;margin:0" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></p></div>