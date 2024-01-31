05_divMigrate
================

R script for DivMigrate analysis of P. turqueti samples from the Scotia
Sea (+ South Weddell Sea):

``` r
library(diveRsity)

#Create genpop file using PGDSpider, with the thin1000_maf005_obshet05.vcf from 01.SNP_filtering.Rmd
#Make sure to remove locations with n=1

res_sco <- divMigrate("./Scotia_SWS_5188_genpop.txt", plot_network = TRUE, 
                      boots = 10000, para = TRUE, stat = "Nm")
save.image(file="./divmigrate/sco_divmigrate.RData")
res_sco_matrix<- res_sco$nmRelMig
write.csv(res_sco_matrix, "./divmigrate/divmigrate_Scotia_SWS_for_plotting.csv")
```

Ran the above R script on HPC

``` bash
cd $PBS_O_WORKDIR
source /etc/profile.d/modules.sh
module load R

singularity run /fast/tmp/containers/R-4.1.2u1.sif Rscript Scotia_SWS_divmigrate.R
```
