# Collateral-Optimization
Collateral Optimization using MILP and QUBO formulations. 
<img src="bipartite.png" alt="" width="340" height="200" align="right" style="margin-left: 10px; margin-bottom: 10px;">

<h2>Generic Information</h2>

In this repository we provide the code used to generate the numericall illustrations on [arxiv identifier]. In the paper we study the problem of collateral optimization wherein we:
1. Review the problem of collateral optimization with a small appetizer (that serves to explain our approach) using the Knapsack Problem.
2. Provide a Mixed Integer Linear Programming (MILP) formulation. 
3. Provide two approaches to reformulate the MILP problem as a Quadratic Unconstrained Binary Optimization (QUBO) problem. These include:   
  a) Slack-based (balanced) formulation (see, for example, [arXiv:1302.5843](https://arxiv.org/abs/1302.5843)).  
  b) Unbalansed formulation (see [arXiv:2211.13914](https://arxiv.org/abs/1302.5843)).
4. Provide some numerical illustrations done with emulators (i.e. by utilizing simmulated annealing) and discuss the results.

We have several types of constraints for our collateral optimisation problem: 
1. Consistency constraints - This is about ensuring we don't post more than 100% of a single asset. 
2. Exposure constraints - The values of all assets posted to an account must be above the exposure for the account. 
3. Single limits - There is a maximum limit on how much asset i can be posted to account j. 

Remark: Consistency constraints are hard constraints and we cannot have any violations. Exposure constraints are soft constraints but we still want the solution values to be as close as possible to the requirements. For simplicity, we are currently solving it without the single limits but all files contain the function and the user can choose to activate it or not. Finally, let us note that we also add code for implementing haircuts. The data for all those constraints are given as .csv files.


<h2>Contents</h2>

Firstly we provide the code for the MILP formulation (file [HiGHs_no_single_limits.ipynb](HiGHs_no_single_limits.ipynb)) which utilizes the HiGHS solver, see [https://highs.dev/](https://highs.dev/).

<h3>D-Wave's neal with PyQUBO</h3>
Here we provide two notebooks, each implementing one of the QUBO form we propose. We use the [PyQUBO](https://pyqubo.readthedocs.io/en/latest/) library to map the problem into a QUBO form, which is then solved using the SimulatedAnnealingSampler() from Dwave's (neal)[https://docs.ocean.dwavesys.com/projects/neal/en/latest/] library. The two files are:

1. File [balanced_collateral_pyqubo_nosinglelimits.ipynb](./balanced_collateral_pyqubo_nosinglelimits.ipynb)
2. File [unbalanced_collateral_pyqubo_nosinglelimits.ipynb](./unbalanced_collateral_pyqubo_nosinglelimit.ipynb)


<h3>Fujitsu's Digital Annealer</h3>
Here we also provide two files that, using the QUBO reformulations provided in the paper, solve the problem approximately using [Fujitsu's Digital Annealer Emulator](https://www.fujitsu.com/de/themes/digitalannealer/get-started/get-started-en.html). Concretely: 

1. File [balanced_collateral_fujitsu_nosinglelimits.ipynb](./balanced_collateral_fujitsu_nosinglelimits.ipynb) provides the code for the balanced (slack-based) formulation.  
2. File [unbalanced_collateral_fujitsu_nosinglelimits.ipynb](./unbalanced_collateral_fujitsu_nosinglelimits.ipynb) provides the code for the unbalanced formulation.  

<h4>Results</h4>

At a high level we were able to obtain results comparable to classical MILP solvers with potential sources of discrepancy being the bit allocation restrictions by the emulators. 

<h4>Contributors</h4>
This body of research has been conducted by: Megan Giron*, Georgios Korpas, Waqas Parvaiz* and Prashant Malik, Johannes Aspman (* = Equal contribution). 

<h5>Contact</h5>

Questions, corrections and comments should be directed to:  [megancharrisze@gmail.com](mailto:megancharrisze@gmail.com) and/or
[waqasparvaiz1@gmail.com](mailto:waqasparvaiz1@gmail.com) 

