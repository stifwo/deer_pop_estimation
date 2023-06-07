# deer_pop_estimation
This repo provides the data and code underlying Omholt, S.W, Gamelon, M. and Meisingset, E.L. (2023): **Robust abundance estimation of harvested populations from sloppy time-series data: a red deer case study**. 

**Abstract:
Reliable estimates of the size and composition of harvested populations over time are key to designing adequate population management plans, regardless of management objectives. Strong theoretical tools exist to provide such estimates when the population abundance variability is comparable with the variation in the observation data (census) and one has a clear understanding of the stochastic process generating the observation data. When this is not the case, these tools are prone to give dubious estimates. In Norway, a national system for collecting and analyzing hunter-reported data on red deer (Cervus elaphus) has been operational for about 20 years. The system was anticipated to provide population metrics that would substantially improve deer population management routines at the municipal level. This has proven to be challenging, and the administrative and scientific value of continuing to collect these data has been questioned. A major reason for this situation is that the variation in the observation data is overall much larger than what is biologically feasible. Using hunter-reported data including census and harvest bags, from six Norwegian municipalities collected in the period 2007-2021, we report that robust abundance estimates can still be obtained if the data are assessed in the context of a large family of hypothetical long-term population projections generated by a stochastic sex- and stage-structured discrete dynamic population model. Furthermore, the model-guided analysis of the time series data suggests that a female-biased harvest regime causes a substantially enhanced net emigration of stags. This indicates that, depending on the relative abundance of adult stags versus adult hinds, stags migrate to prospect future reproductive success. Our approach is widely applicable to any exploited populations for which age and sex-specific counts and hunting bags are available, in the absence of individual long-term monitoring.**

It is recommended that you have read the paper before you start to run the scripts.

**What the deposited Jupyter lab scripts do**:

**data_municipalities.ipynb**: Contains all empirical data used for each of the six municipalities studied, except slaughter weight data which are embedded in figure_3.ipynb that produces figure 3. 

**make_synthetic_populations.ipynb**: Creates a large set of hypothetical population projections for each of the six municipalities by use of a stochastic sex- and stage-structured population model, using reported harvest data specific to each municipality.

**rss_seen_deer.ipynb**: Performs a residual-sum-of-squares analysis based on the hypothetical population projection set and the reported seen_deer_per_hour data, for each of the six municipalities studied.

**rss_no_emigration_seen_deer.ipynb**: Performs a residual-sum-of-squares analysis based on the seen_deer_per_hour data and the subset of hypothetical population projections where stag emigration is not allowed.

**rss_spring_census.ipynb**: Performs a residual-sum-of-squares analysis based on the hypothetical population projection set and the reported spring census data, for each of the five municipalities providing data.

**rss_seen_deer_shuffle.ipynb**: Here the seen-deer-per-hour time-series data are reshuffled 40x for each municipality, according to a set of criteria, in order to show how robust the estimation procedure is to a marked change of the observation data.

**figure_2.ipynb**: Produces figure 2 in the paper based on data in data_municipalities.ipynb.

**figure_3.ipynb**: Produces figure 3 in the paper. The underlying data are contained in the script.

**figure_4.ipynb**: Produces figure 4 in the paper based on data provided by data_municipalities.ipynb and rss_seen_deer.ipynb.

**figure_5.ipynb**: Produces figure 4 in the paper based on data provided by data_municipalities.ipynb and rss_seen_deer_no_emigration.ipynb.

**figure_6.ipynb**: Produces figure 6 in the paper based on data provided by data_municipalities.ipynb and rss_seen_deer_no_emigration.ipynb.

**figure_7.ipynb**: Produces figure 7 in the paper based on data provided by make_synthetic_populations.ipynb* and rss_seen_deer.ipynb.

**figure_8.ipynb**: Produces figure 8 in the paper based on data provided by rss_seen_deer_shuffle.ipynb.

**Program flow - what to execute when:**
1. After you have cloned the repo and are ready to run the scripts in Jupyter lab, make two new subdirectories **\figures** and **\synthetic_data** as the scripts expect these to be in place for storing results.

2. To make the set of hypothetical population projections you have to run **data_municipalities.ipynb** and then **make_synthetic_populations.ipynb**. Note that the latter is memory-greedy, so you will need to run it on a computer with sufficient RAM. 100 GB RAM will probably be fine. The code has not been parallelized, so the script will take several hours to finish. 

3. To do the residual-sum-of-squares analysis based on the hypothetical population projection set and the seen_deer_per_hour data you run **rss_seen_deer.ipynb** and **rss_no_emigration_seen_deer.ipynb**. The latter uses only those hypothetical projections where there is no stag emigration per definition.

4. To do the residual-sum-of-squares analysis based on the hypothetical population projection set and the spring census data you  run **rss_seen_deer.ipynb**.

5. Now you can generate figures 2, 3, 4, 5, 6 and 7 in the paper by running **figure_2.ipynb, figure_3.ipynb, figure_4.ipynb, figure_5.ipynb, figure_6.ipynb and figure_7.ipynb**.

6. To generate figure 8 in the paper, you have to first run **rss_seen_deer_shuffle.ipynb**. You can generate the whole data set by running this script alone. But this takes a very long time, so it is recommended that you make several copies of it and run them in parallel in Jupyter lab. Then you merge the generated lists and put the merge into **figure_8.ipynb** before you run it.


**Additional scripts in this repo:**

The script **parameter_distributions.ipynb** generates plots showing (i) the variation in the winter survival parameters and the fertility parameters in the 15-year period for each of the top 20 RSS hits for each municipality (seen-deer data), (ii) corresponding variation in Shapiro-Wilk p-values and how these p-value distributions compare with the mean Shapiro-Wilk p-value obtained by drawing 15 numbers 50 times from the associated normal distribution, (iii) corresponding variation in mean winter survival and mean fertility parameters and how these compare with the mean of the mean value obtained by drawing 15 numbers 50 times from the associated normal distribution, and (iv) corresponding variation in the standard deviation of winter survival and  fertility parameters and how these compare with the mean standard deviation value obtained by drawing 15 numbers 50 times from the associated normal distribution.

The script **parameter_correlations.ipynb** generates plots for all municipalities showing the top 20 RSS hits (seen-deer data) distributions of correlations between winter survival parameters and fertility parameters over the 15-year period. And it plots a correlation matrix based on random sampling from the underlying normal distributions. 

The plots generated by these two scripts are referred to in the paper, but not shown there.
