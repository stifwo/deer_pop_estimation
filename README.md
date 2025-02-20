# deer_pop_estimation
This repo provides the data and code underlying Omholt, S.W, Gamelon, M. and Meisingset, E.L. (2025): **Robust abundance estimation of harvested populations from low quality time series data: a red deer case study** (submitted) 

**Abstract:
Reliable estimates of the size and composition of harvested populations over time are key to designing adequate population management plans, regardless of management objectives. In Norway, a national system for collecting and analysing hunter-reported data on red deer (Cervus elaphus) has been operational for about 20 years. The system was expected to provide population metrics that would substantially improve deer population management routines at the municipal level. This has proven to be challenging when using existing state-of-the-art estimation methodology. The main reasons are that the variation in the observation data is generally much larger than population abundance variability, and that one does not have a clear understanding of the stochastic process generating the observation data. Here, using hunter-reported observation data and harvest data from six Norwegian municipalities collected in the period 2007-2023, we show that a straightforward estimation methodology based on population modelling can produce robust abundance estimates despite frequent low quality of the observation data. Its major assets are that it does not involve strong assumptions about the stochastic processes underlying the observation process and that it does not involve assumptions about initial population size and structure in terms of prior statistical distributions. We anticipate that the method can be applied in several other population management contexts, and we think that the results offer fresh perspectives on to what extent noisy citizen-collected time series data can be used to inform management decisions.**

It is recommended that you have read the paper and the accompanying Supplementary material before you start to run the scripts.

The scripts are written in Jupyter lab (version 3.6.1), using Python (version 3.8.5), Pandas (version 1.2.1), and IPython Parallel (version 7.20.0).

**Explanation of how to reproduce the figures and the supplementary figures in the paper:** 

**Basic layout**:

The script **data_municipalities.ipynb** contain all raw data for the six municipalities (except slaugther weight data shown in Fig. S1, which are provided in the script **figure_S1.ipynb** producing Fig. S1). 

Scripts named **msp_ipypar_xx_L2_xx.ipynb** makes large sets of hypothetical population projections for the period 2007-2023 for all six municipalities under study, based on the mathematical model provided in Table S2 in Supplementary material. The scripts differ in terms of the initial parameter sets and whether they use stochastic or deterministic winter mortality and fertility parameters. They do L2 norm fitting of each hypothetical population trajectory and saves only a specified number of trajectories with the lowest L2 norm values. All scripts use trivial parallelization, where you can define the number of engines used. We have used 52 engines.  The scripts produce pandas files containing detailed information about each stored population trajectory and the parameter values that created it.

Scripts named **figure_2.ipynb, figure_3.ipynb, figure_4.ipynb, figure_5.ipynb, figure_6.ipynb** produce five of the six figures in the main paper. The script **figure_2.ipynb** plots empirical data stored in **data_municipalities.ipynb**, while the other scripts are in addition based on the information stored in the data frames **top_hits_xxxxx.pkl**.

Scripts named **figure_S1.ipynb, figure_S2.ipynb, figure_S3_and_S4.ipynb, figure_S5.ipynb** produce the five figures in the Supplementary material. The scripts **figure_S1.ipynb** and **figure_S2.ipynb** produce plots based on emprirical data only. The scripts **figure_S3.ipynb** and **figure_S4.ipynb** produce plots related to the analytical foundation of the proposed estimation method. The script **figure_S5.ipynb** produce plots based on the information produced by the scripts **msp_ipypar_xx_L2_xx.ipynb**.


**Script execution to obtain Figures 2-6 in main paper:**

1. Run **data_municipalities.ipynb**. Stores the empirical data for each municipality in IPython’s database as a Python variable for easy access by other scripts.

2. Run **figure_2.ipynb** to reproduce Fig. 2. 

6. Run **msp_ipypar_stoch_L2.ipynb**. The script produces the pandas files needed to make Fig. 3 and Fig. 6.

7. Run **figure_3.ipynb** to reproduce Fig. 3. 

8. Run **figure_6.ipynb** to reproduce Fig. 6. 

9. Run **msp_ipypar_stoch_L2_no_emig.ipynb**. This script is identical with **msp_ipypar_stoch_L2.ipynb**, except that it does not open for any stag emigration.

11. Run **figure_4.ipynb** to reproduce Fig. 4.

12. Run **figure_5.ipynb** to reproduce Fig. 5.  


**Script execution to obtain Figures S1-S5 in Supplementary material:**

1. Run **figure_S1.ipynb** to reproduce Fig. S1. Uses empirical data stored in the script. 

2. Run **figure_S2.ipynb** to reproduce Fig. S2. Uses empirical data stored in **data_municipalities.ipynb**. 

3. Run **figure_S3_and_S4.ipynb** to reproduce Fig. S3 and Fig. S4. 

4. Run **msp_ipypar_stoch_L2_fixed_sph.ipynb** twice with the parameter **number_of_replicates** set to 1 and 50, respectively, to produce data needed for making Fig. S5. The script is identical with **msp_ipypar_stoch_L2.ipynb** except that the values of the parameters **initial_hinds_per_stag** and **stags_per_hind_threshold** are fixed to 1.7 and 0.58, respectively.

5. Run **msp_ipypar_det_L2_fixed_M.ipynb** with the parameter **det_type** set to "det_mean", to produce data needed for making Fig. S5.  

8. Run **figure_S5.ipynb** to reproduce Fig. S5.


**Auxiliary scripts (located in the subdirectory auxiliary_script):**

**test_trends.ipynb:** assesses trends in the reported time series data by use of various techniques and calculates cv and max relative distance from mean for the seen_deer data.

**msp_ipypar_stoch_L2_spring_count.ipynb:** Same as **msp_ipypar_stoch_L2.ipynb**, except that the script uses the spring count data instead of the seen-deer-per_hour data for L2 norm evaluation, for municipalities Tingvoll, Surnadal, Sunndal, Vestnes and Lærdal (Averøy did not have sufficient spring count data). Move the file into the main directory before running.

**figure_3_spring_count.ipynb:** Same as **figure_3.ipynb** except that it is based on spring count data. This figure is only referred to in the paper. Move the file into the main directory before running.

