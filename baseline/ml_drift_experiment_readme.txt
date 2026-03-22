motivation: 
I was curious about a recurring paradox in ML systems. 
We define the data pipeline, preprocessing steps, 
model architecture, and evaluation metrics. 
Each component behaves as expected in isolation.
 Yet in deployment, performance still degrades. 
That led me to investigate where instability enters a
 system that appears structurally correct. I wanted to 
identify the hidden variables that introduce drift even 
when no explicit bug exists.

another one:
I wanted to understand why ML systems degrade even when
 their implementation is technically correct. My hypothesis 
was that the failure doesn't originate from faulty components,
 but from hidden distributional shifts introduced upstream. 
This project became an investigation into identifying those 
hidden sources of instability.