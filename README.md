# GAWS_LOCAL
GAMLSS Akaike Weights Algorithm Instructions for Running on Local Machine

This quick guide will help people looking to reproduce results as described in this working paper:
https://www.researchgate.net/publication/338866907_Detecting_Anomalous_Time_Series_by_GAMLSS-Akaike-Weights-Scoring?_sg=MEG1nT-Zofhq3h7VQ78CxArG5ImY1PEd5pPaD5c5FGUqNIKkPaPqVeIEhwOXrtGrcVE43NgiBEGW9hJJpKt07yqTYUQkf4Ww9ri9ROsQ.X3tu9FulttOyMuKgDimMYkAcXQ7-oR2I5V2kFAmFOwmgqB_vBylKJvtpx8fSU_j4zczCBmLPMEKPR2cjW_FGUg

--- Important Notes:
-code was tested running each script in R studio in Windows environment. Suggest running R under this environment
-Local implementation of GAWS algorithm uses multiple loops and is slow. Expect about 10-25 minutes per run
-Run in an environment with both read/write privileges
-Requires access to internet to download CRAN packages
-Besides running the script "1.install.packages.r" everything else can be executed in any desired order
-Results might slightly diff re-running simulation experiments 1-5 due to sampling of different time series

--- Directory Structure:
It is assumed that you will run R scripts under the main working directory which contains these folders:
data
results
sim
src

--- Setup:
-Run the script: 1.install.packages.r
This will check if all necessary packages are present and if not try to install.
DO NOT PROCEED TO RUN ANY OTHER SCRIPTS UNTIL CHECKING ALL PACKAGES WERE SUCCESSFULLY INSTALLED!!!


--- Real Data: Pedestrian Hourly Count Time Series
-Run the script GAWS_classify_ped_series_shift.r

-Should see csv file under results folder containing GAWS ranking: gaws_ranking_ped_series.csv

-Note that Col = 32 corresponds to the anomalous Southbank time series

Assuming you are running from R studio then you should get two time series plots showing the top 6 GAWS ranking
and plot of all other series.


--- Real Data: Normalized/Peturbed Cloud Traffic 30-minute Time Series
-Run the scripts: (can be ran independently!)
GAWS_detect_cloud_traffic_shape_anomalies.r
stray_detect_cloud_traffic_shape_anomalies.r

-Should see two csv files under results folder containing rankings:
ranks_gaws_cloud_traffic.csv
ranks_stray_cloud_traffic.csv

-note that the 4 anomalous time series correspond to Col: 139 140 141 142


--- Simulation Experiment 1: Subspace with multiple seasonality and 10 Anomalous Series
-Run the scripts: (can be ran independently!)
Detection_Performance_HDR_E1
Detection_Performance_stray_E1
Detection_Performance_GAWS_E1

-Should see 3 csv files with pattern "_results_1.csv" under results folder. 
The files contain the fScore, excess_rank_abs performance metrics averaged over number of simulation runs.

-if interested in mean ranking per each anomalous time series then also look at files with pattern "_ranks_1.csv".

-using existing script arguments expect Detection_Performance_GAWS_E1 to take between 1-2 hours to complete!

--- Simulation Experiment 2: Multiple subspaces: Seasonality, Pulse, Upward Step, Autoregressive Term and 10 Anomalous Series
-Run the scripts: (can be ran independently!)
Detection_Performance_HDR_E2
Detection_Performance_stray_E2
Detection_Performance_GAWS_E2

-Should see 3 csv files with pattern "_results_2.csv" under results folder. 
The files contain the fScore, excess_rank_abs performance metrics averaged over number of simulation runs.

-if interested in mean ranking per each anomalous time series then also look at files with pattern "_ranks_2.csv".

-using existing script arguments expect Detection_Performance_GAWS_E2 to take between 2-4 hours to complete!

--- Simulation Experiment 3: Normal Subspace consists of constant location/scale/shape and 20 anomalies
-Run the scripts: (can be ran independently!)
Detection_Performance_HDR_E3
Detection_Performance_stray_E3
Detection_Performance_GAWS_E3

-Should see 3 csv files with pattern "_results_3.csv" under results folder. 
The files contain the fScore, excess_rank_abs performance metrics averaged over number of simulation runs.

-if interested in mean ranking per each anomalous time series then also look at files with pattern "_ranks_3.csv".

-using existing script arguments expect Detection_Performance_GAWS_E3 to take about 15-35 min to complete!

--- Simulation Experiment 4: GAWS Penalized Splines with Normal Subspace consists of constant location/scale/shape and 10 original anomalies
-Run the scripts:
Detection_Performance_HDR_E4
Detection_Performance_stray_E4
Detection_Performance_GAWS_E4

-Should see 3 csv files with pattern "_results_4.csv" under results folder. 
The files contain the fScore, excess_rank_abs performance metrics averaged over number of simulation runs.

-using existing script arguments expect Detection_Performance_GAWS_E4 to take > 2 hours  to complete!


--- Simulation Experiment 5: GAWS Penalized Splines with Normal Subspace consists of Level, Seasonality, Pulses, AR, Shift and 10 original anomalies
-Run the scripts:
Detection_Performance_HDR_E5
Detection_Performance_stray_E5
Detection_Performance_GAWS_E5

-Should see 3 csv files with pattern "_results_5.csv" under results folder. 
The files contain the fScore, excess_rank_abs performance metrics averaged over number of simulation runs.

-using existing script arguments expect Detection_Performance_GAWS_E5 to take >3 hours to complete!
