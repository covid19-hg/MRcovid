---
title: "Mendelian Randomization Analysis"
author: "Dr. Shea Andrews"
date: "2021-02-19"
output:
  html_document:
    df_print: paged
    keep_md: true
    toc: true
    number_sections: false
    toc_depth: 4
    toc_float:
      collapsed: false
      smooth_scroll: false
params:
  rwd: NA
  exposure.code: NA
  Exposure: NA
  exposure.snps: NA
  outcome.code: NA
  Outcome: NA
  outcome.snps: NA
  proxy.snps: NA
  harmonized.dat: NA
  p.threshold: NA
  r2.threshold: NA
  kb.threshold: NA
  mrpresso_global: NA
  mrpresso_global_wo_outliers: NA
  power: NA
  out: NA
editor_options:
  chunk_output_type: console
---






## Instrumental Variables
**SNP Inclusion:** SNPS associated with at a p-value threshold of p < 5e-8 were included in this analysis.
<br>

**LD Clumping:** For standard two sample MR it is important to ensure that the instruments for the exposure are independent. LD clumping was performed in PLINK using the EUR samples from the 1000 Genomes Project to estimate LD between SNPs, and, amongst SNPs that have an LD above a given threshold, retain only the SNP with the lowest p-value. A clumping window of 10^{4}, r2 of 0.001 and significance level of 1 was used for the index and secondary SNPs.
<br>

**Proxy SNPs:** Where SNPs were not available in the outcome GWAS, the EUR thousand genomes was queried to identify potential proxy SNPs that are in linkage disequilibrium (r2 > 0.8) of the missing SNP.
<br>

### Exposure: Smoking Quantity
`#r exposure.blurb`
<br>

**Table 1:** Independent SNPs associated with Smoking Quantity
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["SNP"],"name":[1],"type":["chr"],"align":["left"]},{"label":["CHROM"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["POS"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["REF"],"name":[4],"type":["chr"],"align":["left"]},{"label":["ALT"],"name":[5],"type":["chr"],"align":["left"]},{"label":["AF"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["BETA"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["SE"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["Z"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["P"],"name":[10],"type":["dbl"],"align":["right"]},{"label":["N"],"name":[11],"type":["dbl"],"align":["right"]},{"label":["TRAIT"],"name":[12],"type":["chr"],"align":["left"]}],"data":[{"1":"rs2072659","2":"1","3":"154548521","4":"C","5":"G","6":"0.1050","7":"-0.0359","8":"0.00526","9":"-6.825095","10":"1.71e-12","11":"263954","12":"smkcpd"},{"1":"rs2084533","2":"3","3":"16872929","4":"C","5":"T","6":"0.3190","7":"0.0166","8":"0.00293","9":"5.665529","10":"1.22e-08","11":"263954","12":"smkcpd"},{"1":"rs7431710","2":"3","3":"48935583","4":"G","5":"A","6":"0.6440","7":"-0.0173","8":"0.00287","9":"-6.027875","10":"1.82e-09","11":"263954","12":"smkcpd"},{"1":"rs11725618","2":"4","3":"67053769","4":"T","5":"C","6":"0.2870","7":"0.0187","8":"0.00319","9":"5.862069","10":"4.67e-09","11":"263954","12":"smkcpd"},{"1":"rs787362","2":"4","3":"67904931","4":"T","5":"A","6":"0.4520","7":"0.0151","8":"0.00276","9":"5.471014","10":"4.50e-08","11":"263954","12":"smkcpd"},{"1":"rs806798","2":"6","3":"26214473","4":"T","5":"C","6":"0.5430","7":"-0.0155","8":"0.00279","9":"-5.555556","10":"2.48e-08","11":"263954","12":"smkcpd"},{"1":"rs215600","2":"7","3":"32333642","4":"G","5":"A","6":"0.6400","7":"-0.0246","8":"0.00287","9":"-8.571429","10":"1.10e-17","11":"263954","12":"smkcpd"},{"1":"rs73229090","2":"8","3":"27442127","4":"C","5":"A","6":"0.1130","7":"0.0282","8":"0.00447","9":"6.308725","10":"2.44e-10","11":"263954","12":"smkcpd"},{"1":"rs58379124","2":"8","3":"42579203","4":"T","5":"C","6":"0.7480","7":"0.0337","8":"0.00331","9":"10.181269","10":"9.00e-25","11":"263954","12":"smkcpd"},{"1":"rs790564","2":"8","3":"64604218","4":"A","5":"C","6":"0.7190","7":"-0.0205","8":"0.00310","9":"-6.612903","10":"3.97e-11","11":"263954","12":"smkcpd"},{"1":"rs3025383","2":"9","3":"136502369","4":"T","5":"C","6":"0.1800","7":"-0.0292","8":"0.00359","9":"-8.133705","10":"2.22e-16","11":"263954","12":"smkcpd"},{"1":"rs7951365","2":"11","3":"16377044","4":"T","5":"C","6":"0.3060","7":"0.0196","8":"0.00301","9":"6.511628","10":"6.63e-11","11":"263954","12":"smkcpd"},{"1":"rs75494138","2":"11","3":"46465361","4":"C","5":"T","6":"0.0618","7":"0.0295","8":"0.00523","9":"5.640535","10":"1.45e-08","11":"263954","12":"smkcpd"},{"1":"rs7928017","2":"11","3":"113448762","4":"C","5":"A","6":"0.4130","7":"-0.0165","8":"0.00280","9":"-5.892857","10":"3.14e-09","11":"263954","12":"smkcpd"},{"1":"rs632811","2":"15","3":"59155050","4":"A","5":"G","6":"0.3510","7":"-0.0190","8":"0.00328","9":"-5.792683","10":"1.03e-08","11":"263954","12":"smkcpd"},{"1":"rs8034191","2":"15","3":"78806023","4":"T","5":"C","6":"0.3280","7":"0.0906","8":"0.00292","9":"31.027397","10":"4.80e-211","11":"263954","12":"smkcpd"},{"1":"rs2386571","2":"16","3":"52074123","4":"A","5":"C","6":"0.5700","7":"-0.0159","8":"0.00278","9":"-5.719424","10":"1.03e-08","11":"263954","12":"smkcpd"},{"1":"rs4785587","2":"16","3":"89772619","4":"G","5":"A","6":"0.5110","7":"-0.0171","8":"0.00283","9":"-6.042403","10":"1.27e-09","11":"263954","12":"smkcpd"},{"1":"rs895330","2":"19","3":"4060707","4":"C","5":"G","6":"0.2060","7":"-0.0198","8":"0.00360","9":"-5.500000","10":"2.68e-08","11":"263954","12":"smkcpd"},{"1":"rs34406232","2":"19","3":"41305530","4":"C","5":"A","6":"0.0259","7":"-0.0739","8":"0.00833","9":"-8.871549","10":"1.33e-18","11":"263954","12":"smkcpd"},{"1":"rs56113850","2":"19","3":"41353107","4":"T","5":"C","6":"0.5680","7":"0.0560","8":"0.00291","9":"19.243986","10":"1.10e-81","11":"263954","12":"smkcpd"},{"1":"rs2424888","2":"20","3":"31047533","4":"G","5":"A","6":"0.4050","7":"0.0170","8":"0.00287","9":"5.923345","10":"2.76e-09","11":"263954","12":"smkcpd"},{"1":"rs2273500","2":"20","3":"61986949","4":"T","5":"C","6":"0.1590","7":"0.0347","8":"0.00398","9":"8.718593","10":"2.47e-18","11":"263954","12":"smkcpd"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

### Outcome: COVID: A2
`#r outcome.blurb`
<br>

**Table 2:** SNPs associated with Smoking Quantity avaliable in COVID: A2
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["SNP"],"name":[1],"type":["chr"],"align":["left"]},{"label":["CHROM"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["POS"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["REF"],"name":[4],"type":["chr"],"align":["left"]},{"label":["ALT"],"name":[5],"type":["chr"],"align":["left"]},{"label":["AF"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["BETA"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["SE"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["Z"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["P"],"name":[10],"type":["dbl"],"align":["right"]},{"label":["N"],"name":[11],"type":["dbl"],"align":["right"]},{"label":["TRAIT"],"name":[12],"type":["chr"],"align":["left"]}],"data":[{"1":"rs2072659","2":"1","3":"154548521","4":"C","5":"G","6":"0.10020","7":"-0.07015900","8":"0.059415","9":"-1.18082976","10":"0.237700","11":"1049400","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs2084533","2":"3","3":"16872929","4":"C","5":"T","6":"0.31630","7":"0.04202800","8":"0.034999","9":"1.20083000","10":"0.229800","11":"1049400","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs7431710","2":"3","3":"48935583","4":"G","5":"A","6":"0.64910","7":"-0.02588200","8":"0.027264","9":"-0.94931045","10":"0.342500","11":"1057104","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs11725618","2":"4","3":"67053769","4":"T","5":"C","6":"0.28530","7":"0.00140180","8":"0.036524","9":"0.03838024","10":"0.969400","11":"1049400","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs787362","2":"4","3":"67904931","4":"T","5":"A","6":"0.44650","7":"0.00400860","8":"0.032667","9":"0.12271099","10":"0.902300","11":"1048997","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs806798","2":"6","3":"26214473","4":"T","5":"C","6":"0.53370","7":"-0.04528500","8":"0.032921","9":"-1.37556575","10":"0.169000","11":"1048997","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs215600","2":"7","3":"32333642","4":"G","5":"A","6":"0.65800","7":"-0.06040600","8":"0.026698","9":"-2.26256648","10":"0.023670","11":"1059053","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs73229090","2":"8","3":"27442127","4":"C","5":"A","6":"0.11040","7":"0.03836700","8":"0.050523","9":"0.75939671","10":"0.447600","11":"1049400","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs58379124","2":"8","3":"42579203","4":"T","5":"C","6":"0.76170","7":"-0.00077344","8":"0.037510","9":"-0.02061957","10":"0.983500","11":"1049400","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs790564","2":"8","3":"64604218","4":"A","5":"C","6":"0.73200","7":"-0.03745700","8":"0.036562","9":"-1.02447897","10":"0.305600","11":"1048997","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs3025383","2":"9","3":"136502369","4":"T","5":"C","6":"0.18060","7":"0.05251900","8":"0.043030","9":"1.22052057","10":"0.222300","11":"1049400","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs7951365","2":"11","3":"16377044","4":"T","5":"C","6":"0.29880","7":"-0.01916200","8":"0.036306","9":"-0.52779155","10":"0.597600","11":"1049400","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs75494138","2":"11","3":"46465361","4":"C","5":"T","6":"0.06365","7":"-0.00960590","8":"0.051677","9":"-0.18588347","10":"0.852500","11":"1059456","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs7928017","2":"11","3":"113448762","4":"C","5":"A","6":"0.39890","7":"0.02354100","8":"0.025900","9":"0.90891892","10":"0.363400","11":"1059456","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs632811","2":"15","3":"59155050","4":"A","5":"G","6":"0.36070","7":"0.03857900","8":"0.035654","9":"1.08203848","10":"0.279200","11":"1049400","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs8034191","2":"15","3":"78806023","4":"T","5":"C","6":"0.34560","7":"-0.00053049","8":"0.026653","9":"-0.01990358","10":"0.984100","11":"1059456","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs2386571","2":"16","3":"52074123","4":"A","5":"C","6":"0.57530","7":"0.03744900","8":"0.033979","9":"1.10212190","10":"0.270400","11":"1049400","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs4785587","2":"16","3":"89772619","4":"G","5":"A","6":"0.52360","7":"0.07004700","8":"0.032829","9":"2.13369277","10":"0.032870","11":"1049400","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs895330","2":"19","3":"4060707","4":"C","5":"G","6":"0.18700","7":"-0.11184000","8":"0.041361","9":"-2.70399652","10":"0.006852","11":"1049400","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs34406232","2":"19","3":"41305530","4":"C","5":"A","6":"0.02610","7":"-0.07864200","8":"0.083872","9":"-0.93764308","10":"0.348400","11":"1059456","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs56113850","2":"19","3":"41353107","4":"T","5":"C","6":"0.56850","7":"-0.03959000","8":"0.034648","9":"-1.14263450","10":"0.253200","11":"1049400","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs2424888","2":"20","3":"31047533","4":"G","5":"A","6":"0.40300","7":"0.05158400","8":"0.035315","9":"1.46068243","10":"0.144100","11":"1048997","12":"COVID_A2__EUR_w/o_UKBB"},{"1":"rs2273500","2":"20","3":"61986949","4":"T","5":"C","6":"0.16470","7":"-0.01540900","8":"0.035099","9":"-0.43901536","10":"0.660600","11":"1059456","12":"COVID_A2__EUR_w/o_UKBB"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

**Table 3:** Proxy SNPs for COVID: A2
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["proxy.outcome"],"name":[1],"type":["lgl"],"align":["right"]},{"label":["target_snp"],"name":[2],"type":["lgl"],"align":["right"]},{"label":["proxy_snp"],"name":[3],"type":["lgl"],"align":["right"]},{"label":["ld.r2"],"name":[4],"type":["lgl"],"align":["right"]},{"label":["Dprime"],"name":[5],"type":["lgl"],"align":["right"]},{"label":["ref.proxy"],"name":[6],"type":["lgl"],"align":["right"]},{"label":["alt.proxy"],"name":[7],"type":["lgl"],"align":["right"]},{"label":["CHROM"],"name":[8],"type":["lgl"],"align":["right"]},{"label":["POS"],"name":[9],"type":["lgl"],"align":["right"]},{"label":["ALT.proxy"],"name":[10],"type":["lgl"],"align":["right"]},{"label":["REF.proxy"],"name":[11],"type":["lgl"],"align":["right"]},{"label":["AF"],"name":[12],"type":["lgl"],"align":["right"]},{"label":["BETA"],"name":[13],"type":["lgl"],"align":["right"]},{"label":["SE"],"name":[14],"type":["lgl"],"align":["right"]},{"label":["P"],"name":[15],"type":["lgl"],"align":["right"]},{"label":["N"],"name":[16],"type":["lgl"],"align":["right"]},{"label":["ref"],"name":[17],"type":["lgl"],"align":["right"]},{"label":["alt"],"name":[18],"type":["lgl"],"align":["right"]},{"label":["ALT"],"name":[19],"type":["lgl"],"align":["right"]},{"label":["REF"],"name":[20],"type":["lgl"],"align":["right"]},{"label":["PHASE"],"name":[21],"type":["lgl"],"align":["right"]}],"data":[{"1":"NA","2":"NA","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

## Data harmonization
Harmonize the exposure and outcome datasets so that the effect of a SNP on the exposure and the effect of that SNP on the outcome correspond to the same allele. The harmonise_data function from the TwoSampleMR package can be used to perform the harmonization step, by default it try's to infer the forward strand alleles using allele frequency information.
<br>

**Table 4:** Harmonized Smoking Quantity and COVID: A2 datasets
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["SNP"],"name":[1],"type":["chr"],"align":["left"]},{"label":["effect_allele.exposure"],"name":[2],"type":["chr"],"align":["left"]},{"label":["other_allele.exposure"],"name":[3],"type":["chr"],"align":["left"]},{"label":["effect_allele.outcome"],"name":[4],"type":["chr"],"align":["left"]},{"label":["other_allele.outcome"],"name":[5],"type":["chr"],"align":["left"]},{"label":["beta.exposure"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["beta.outcome"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["eaf.exposure"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["eaf.outcome"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["remove"],"name":[10],"type":["lgl"],"align":["right"]},{"label":["palindromic"],"name":[11],"type":["lgl"],"align":["right"]},{"label":["ambiguous"],"name":[12],"type":["lgl"],"align":["right"]},{"label":["id.outcome"],"name":[13],"type":["chr"],"align":["left"]},{"label":["chr.outcome"],"name":[14],"type":["dbl"],"align":["right"]},{"label":["pos.outcome"],"name":[15],"type":["dbl"],"align":["right"]},{"label":["se.outcome"],"name":[16],"type":["dbl"],"align":["right"]},{"label":["z.outcome"],"name":[17],"type":["dbl"],"align":["right"]},{"label":["pval.outcome"],"name":[18],"type":["dbl"],"align":["right"]},{"label":["samplesize.outcome"],"name":[19],"type":["dbl"],"align":["right"]},{"label":["outcome"],"name":[20],"type":["chr"],"align":["left"]},{"label":["mr_keep.outcome"],"name":[21],"type":["lgl"],"align":["right"]},{"label":["pval_origin.outcome"],"name":[22],"type":["chr"],"align":["left"]},{"label":["chr.exposure"],"name":[23],"type":["dbl"],"align":["right"]},{"label":["pos.exposure"],"name":[24],"type":["dbl"],"align":["right"]},{"label":["se.exposure"],"name":[25],"type":["dbl"],"align":["right"]},{"label":["z.exposure"],"name":[26],"type":["dbl"],"align":["right"]},{"label":["pval.exposure"],"name":[27],"type":["dbl"],"align":["right"]},{"label":["samplesize.exposure"],"name":[28],"type":["dbl"],"align":["right"]},{"label":["exposure"],"name":[29],"type":["chr"],"align":["left"]},{"label":["mr_keep.exposure"],"name":[30],"type":["lgl"],"align":["right"]},{"label":["pval_origin.exposure"],"name":[31],"type":["chr"],"align":["left"]},{"label":["id.exposure"],"name":[32],"type":["chr"],"align":["left"]},{"label":["action"],"name":[33],"type":["dbl"],"align":["right"]},{"label":["mr_keep"],"name":[34],"type":["lgl"],"align":["right"]},{"label":["pt"],"name":[35],"type":["dbl"],"align":["right"]},{"label":["pleitropy_keep"],"name":[36],"type":["lgl"],"align":["right"]},{"label":["mrpresso_RSSobs"],"name":[37],"type":["lgl"],"align":["right"]},{"label":["mrpresso_pval"],"name":[38],"type":["lgl"],"align":["right"]},{"label":["mrpresso_keep"],"name":[39],"type":["lgl"],"align":["right"]}],"data":[{"1":"rs11725618","2":"C","3":"T","4":"C","5":"T","6":"0.0187","7":"0.00140180","8":"0.2870","9":"0.28530","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"4","15":"67053769","16":"0.036524","17":"0.03838024","18":"0.969400","19":"1049400","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"4","24":"67053769","25":"0.00319","26":"5.862069","27":"4.67e-09","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs2072659","2":"G","3":"C","4":"G","5":"C","6":"-0.0359","7":"-0.07015900","8":"0.1050","9":"0.10020","10":"FALSE","11":"TRUE","12":"FALSE","13":"51GJaT","14":"1","15":"154548521","16":"0.059415","17":"-1.18082976","18":"0.237700","19":"1049400","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"1","24":"154548521","25":"0.00526","26":"-6.825095","27":"1.71e-12","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs2084533","2":"T","3":"C","4":"T","5":"C","6":"0.0166","7":"0.04202800","8":"0.3190","9":"0.31630","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"3","15":"16872929","16":"0.034999","17":"1.20083000","18":"0.229800","19":"1049400","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"3","24":"16872929","25":"0.00293","26":"5.665529","27":"1.22e-08","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs215600","2":"A","3":"G","4":"A","5":"G","6":"-0.0246","7":"-0.06040600","8":"0.6400","9":"0.65800","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"7","15":"32333642","16":"0.026698","17":"-2.26256648","18":"0.023670","19":"1059053","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"7","24":"32333642","25":"0.00287","26":"-8.571429","27":"1.10e-17","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs2273500","2":"C","3":"T","4":"C","5":"T","6":"0.0347","7":"-0.01540900","8":"0.1590","9":"0.16470","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"20","15":"61986949","16":"0.035099","17":"-0.43901536","18":"0.660600","19":"1059456","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"20","24":"61986949","25":"0.00398","26":"8.718593","27":"2.47e-18","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs2386571","2":"C","3":"A","4":"C","5":"A","6":"-0.0159","7":"0.03744900","8":"0.5700","9":"0.57530","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"16","15":"52074123","16":"0.033979","17":"1.10212190","18":"0.270400","19":"1049400","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"16","24":"52074123","25":"0.00278","26":"-5.719424","27":"1.03e-08","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs2424888","2":"A","3":"G","4":"A","5":"G","6":"0.0170","7":"0.05158400","8":"0.4050","9":"0.40300","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"20","15":"31047533","16":"0.035315","17":"1.46068243","18":"0.144100","19":"1048997","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"20","24":"31047533","25":"0.00287","26":"5.923345","27":"2.76e-09","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs3025383","2":"C","3":"T","4":"C","5":"T","6":"-0.0292","7":"0.05251900","8":"0.1800","9":"0.18060","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"9","15":"136502369","16":"0.043030","17":"1.22052057","18":"0.222300","19":"1049400","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"9","24":"136502369","25":"0.00359","26":"-8.133705","27":"2.22e-16","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs34406232","2":"A","3":"C","4":"A","5":"C","6":"-0.0739","7":"-0.07864200","8":"0.0259","9":"0.02610","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"19","15":"41305530","16":"0.083872","17":"-0.93764308","18":"0.348400","19":"1059456","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"19","24":"41305530","25":"0.00833","26":"-8.871549","27":"1.33e-18","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs4785587","2":"A","3":"G","4":"A","5":"G","6":"-0.0171","7":"0.07004700","8":"0.5110","9":"0.52360","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"16","15":"89772619","16":"0.032829","17":"2.13369277","18":"0.032870","19":"1049400","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"16","24":"89772619","25":"0.00283","26":"-6.042403","27":"1.27e-09","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs56113850","2":"C","3":"T","4":"C","5":"T","6":"0.0560","7":"-0.03959000","8":"0.5680","9":"0.56850","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"19","15":"41353107","16":"0.034648","17":"-1.14263450","18":"0.253200","19":"1049400","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"19","24":"41353107","25":"0.00291","26":"19.243986","27":"1.10e-81","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs58379124","2":"C","3":"T","4":"C","5":"T","6":"0.0337","7":"-0.00077344","8":"0.7480","9":"0.76170","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"8","15":"42579203","16":"0.037510","17":"-0.02061957","18":"0.983500","19":"1049400","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"8","24":"42579203","25":"0.00331","26":"10.181269","27":"9.00e-25","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs632811","2":"G","3":"A","4":"G","5":"A","6":"-0.0190","7":"0.03857900","8":"0.3510","9":"0.36070","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"15","15":"59155050","16":"0.035654","17":"1.08203848","18":"0.279200","19":"1049400","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"15","24":"59155050","25":"0.00328","26":"-5.792683","27":"1.03e-08","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs73229090","2":"A","3":"C","4":"A","5":"C","6":"0.0282","7":"0.03836700","8":"0.1130","9":"0.11040","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"8","15":"27442127","16":"0.050523","17":"0.75939671","18":"0.447600","19":"1049400","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"8","24":"27442127","25":"0.00447","26":"6.308725","27":"2.44e-10","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs7431710","2":"A","3":"G","4":"A","5":"G","6":"-0.0173","7":"-0.02588200","8":"0.6440","9":"0.64910","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"3","15":"48935583","16":"0.027264","17":"-0.94931045","18":"0.342500","19":"1057104","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"3","24":"48935583","25":"0.00287","26":"-6.027875","27":"1.82e-09","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs75494138","2":"T","3":"C","4":"T","5":"C","6":"0.0295","7":"-0.00960590","8":"0.0618","9":"0.06365","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"11","15":"46465361","16":"0.051677","17":"-0.18588347","18":"0.852500","19":"1059456","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"11","24":"46465361","25":"0.00523","26":"5.640535","27":"1.45e-08","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs787362","2":"A","3":"T","4":"A","5":"T","6":"0.0151","7":"0.00400860","8":"0.4520","9":"0.44650","10":"FALSE","11":"TRUE","12":"TRUE","13":"51GJaT","14":"4","15":"67904931","16":"0.032667","17":"0.12271099","18":"0.902300","19":"1048997","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"4","24":"67904931","25":"0.00276","26":"5.471014","27":"4.50e-08","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"FALSE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"NA"},{"1":"rs790564","2":"C","3":"A","4":"C","5":"A","6":"-0.0205","7":"-0.03745700","8":"0.7190","9":"0.73200","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"8","15":"64604218","16":"0.036562","17":"-1.02447897","18":"0.305600","19":"1048997","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"8","24":"64604218","25":"0.00310","26":"-6.612903","27":"3.97e-11","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs7928017","2":"A","3":"C","4":"A","5":"C","6":"-0.0165","7":"0.02354100","8":"0.4130","9":"0.39890","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"11","15":"113448762","16":"0.025900","17":"0.90891892","18":"0.363400","19":"1059456","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"11","24":"113448762","25":"0.00280","26":"-5.892857","27":"3.14e-09","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs7951365","2":"C","3":"T","4":"C","5":"T","6":"0.0196","7":"-0.01916200","8":"0.3060","9":"0.29880","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"11","15":"16377044","16":"0.036306","17":"-0.52779155","18":"0.597600","19":"1049400","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"11","24":"16377044","25":"0.00301","26":"6.511628","27":"6.63e-11","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs8034191","2":"C","3":"T","4":"C","5":"T","6":"0.0906","7":"-0.00053049","8":"0.3280","9":"0.34560","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"15","15":"78806023","16":"0.026653","17":"-0.01990358","18":"0.984100","19":"1059456","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"15","24":"78806023","25":"0.00292","26":"31.027397","27":"1.00e-200","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs806798","2":"C","3":"T","4":"C","5":"T","6":"-0.0155","7":"-0.04528500","8":"0.5430","9":"0.53370","10":"FALSE","11":"FALSE","12":"FALSE","13":"51GJaT","14":"6","15":"26214473","16":"0.032921","17":"-1.37556575","18":"0.169000","19":"1048997","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"6","24":"26214473","25":"0.00279","26":"-5.555556","27":"2.48e-08","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs895330","2":"G","3":"C","4":"G","5":"C","6":"-0.0198","7":"-0.11184000","8":"0.2060","9":"0.18700","10":"FALSE","11":"TRUE","12":"FALSE","13":"51GJaT","14":"19","15":"4060707","16":"0.041361","17":"-2.70399652","18":"0.006852","19":"1049400","20":"covidhgi2020A2v5alleurLeaveUKBB","21":"TRUE","22":"reported","23":"19","24":"4060707","25":"0.00360","26":"-5.500000","27":"2.68e-08","28":"263954","29":"Liu2019smkcpd","30":"TRUE","31":"reported","32":"fipWw2","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

SNPs that genome-wide significant in the outcome GWAS are likely pleitorpic and should be removed from analysis. Additionaly remove variants within the APOE locus by exclude variants 1MB either side of APOE e4 (rs429358 = 19:45411941, GRCh37.p13)
<br>


**Table 5:** SNPs that were genome-wide significant in the COVID: A2 GWAS
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["SNP"],"name":[1],"type":["chr"],"align":["left"]},{"label":["chr.outcome"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["pos.outcome"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["pval.exposure"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["pval.outcome"],"name":[5],"type":["dbl"],"align":["right"]}],"data":[],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>


## Instrument Strength
To ensure that the first assumption of MR is not violated (Non-zero effect assumption), the genetic variants selected should be robustly associated with the exposure. Weak instruments, where the variance in the exposure explained by the the instruments is a small portion of the total variance, may result in poor precission and accuracy of the causal effect estiamte. The strength of an instrument can be evaluated using the F statistic, if F is less than 10, this is an indication of weak instrument.


```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   .default = col_double(),
##   exposure = col_character(),
##   outcome = col_character(),
##   method = col_character(),
##   outliers_removed = col_logical(),
##   logistic = col_logical(),
##   beta = col_logical()
## )
## i Use `spec()` for the full column specifications.
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["outliers_removed"],"name":[1],"type":["lgl"],"align":["right"]},{"label":["pve.exposure"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["F"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["Alpha"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["NCP"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["Power"],"name":[6],"type":["dbl"],"align":["right"]}],"data":[{"1":"FALSE","2":"0.008433387","3":"102.0347","4":"0.05","5":"0.4074533","6":"0.09782802"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

The I2_GX statistic can be used to quantify the strength of the NOME violation for MR-Egger regression and should be used to evalute potential bias in the MR-Egger causal estimate, with values less then 90% indicating that causal estimated should interpreted with caution due to regression diluation.

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["outliers_removed"],"name":[1],"type":["lgl"],"align":["right"]},{"label":["Isq_gx"],"name":[2],"type":["dbl"],"align":["right"]}],"data":[{"1":"FALSE","2":"0.9729101"},{"1":"TRUE","2":"NA"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>


## MR Results
To obtain an overall estimate of causal effect, the SNP-exposure and SNP-outcome coefficients were combined in 1) a fixed-effects meta-analysis using an inverse-variance weighted approach (IVW); 2) a Weighted Median approach; 3) Weighted Mode approach and 4) Egger Regression.


[**IVW**](https://doi.org/10.1002/gepi.21758) is equivalent to a weighted regression of the SNP-outcome coefficients on the SNP-exposure coefficients with the intercept constrained to zero. This method assumes that all variants are valid instrumental variables based on the Mendelian randomization assumptions. The causal estimate of the IVW analysis expresses the causal increase in the outcome (or log odds of the outcome for a binary outcome) per unit change in the exposure. [**Weighted median MR**](https://doi.org/10.1002/gepi.21965) allows for 50% of the instrumental variables to be invalid. [**MR-Egger regression**](https://doi.org/10.1093/ije/dyw220) allows all the instrumental variables to be subject to direct effects (i.e. horizontal pleiotropy), with the intercept representing bias in the causal estimate due to pleiotropy and the slope representing the causal estimate. [**Weighted Mode**](https://doi.org/10.1093/ije/dyx102) gives consistent estimates as the sample size increases if a plurality (or weighted plurality) of the genetic variants are valid instruments.
<br>



Table 6 presents the MR causal estimates of genetically predicted Smoking Quantity on COVID: A2.
<br>

**Table 6** MR causaul estimates for Smoking Quantity on COVID: A2
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["chr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["chr"],"align":["left"]},{"label":["method"],"name":[5],"type":["chr"],"align":["left"]},{"label":["nsnp"],"name":[6],"type":["int"],"align":["right"]},{"label":["b"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["se"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[9],"type":["dbl"],"align":["right"]}],"data":[{"1":"fipWw2","2":"51GJaT","3":"covidhgi2020A2v5alleurLeaveUKBB","4":"Liu2019smkcpd","5":"Inverse variance weighted (fixed effects)","6":"22","7":"0.093330612","8":"0.2112967","9":"0.6587033"},{"1":"fipWw2","2":"51GJaT","3":"covidhgi2020A2v5alleurLeaveUKBB","4":"Liu2019smkcpd","5":"Weighted median","6":"22","7":"-0.009397694","8":"0.2557597","9":"0.9706889"},{"1":"fipWw2","2":"51GJaT","3":"covidhgi2020A2v5alleurLeaveUKBB","4":"Liu2019smkcpd","5":"Weighted mode","6":"22","7":"-0.095593396","8":"0.2481506","9":"0.7039461"},{"1":"fipWw2","2":"51GJaT","3":"covidhgi2020A2v5alleurLeaveUKBB","4":"Liu2019smkcpd","5":"MR Egger","6":"22","7":"-0.180847017","8":"0.4591016","9":"0.6978121"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

Figure 1 illustrates the SNP-specific associations with Smoking Quantity versus the association in COVID: A2 and the corresponding MR estimates.
<br>

<div class="figure" style="text-align: center">
<img src="/sc/arion/projects/LOAD/shea/Projects/MRcovid/results/MRcovideurwoukbb/Liu2019smkcpd/covidhgi2020A2v5alleurLeaveUKBB/Liu2019smkcpd_5e-8_covidhgi2020A2v5alleurLeaveUKBB_MR_Analaysis_files/figure-html/scatter_plot-1.png" alt="Fig. 1: Scatterplot of SNP effects for the association of the Exposure on the Outcome"  />
<p class="caption">Fig. 1: Scatterplot of SNP effects for the association of the Exposure on the Outcome</p>
</div>
<br>


## Pleiotropy
A Cochrans Q heterogeneity test can be used to formaly assesse for the presence of heterogenity (Table 7), with excessive heterogeneity indicating that there is a meaningful violation of at least one of the MR assumptions.
these assumptions..
<br>

**Table 7:** Heterogenity Tests
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["chr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["chr"],"align":["left"]},{"label":["method"],"name":[5],"type":["chr"],"align":["left"]},{"label":["Q"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["Q_df"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["Q_pval"],"name":[8],"type":["dbl"],"align":["right"]}],"data":[{"1":"fipWw2","2":"51GJaT","3":"covidhgi2020A2v5alleurLeaveUKBB","4":"Liu2019smkcpd","5":"MR Egger","6":"32.68085","7":"20","8":"0.03656224"},{"1":"fipWw2","2":"51GJaT","3":"covidhgi2020A2v5alleurLeaveUKBB","4":"Liu2019smkcpd","5":"Inverse variance weighted","6":"33.57213","7":"21","8":"0.04024564"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

Figure 2 shows a funnel plot displaying the MR estimates of individual genetic variants against their precession. Aysmmetry in the funnel plot may arrise due to some genetic variants having unusally strong effects on the outcome, which is indicative of directional pleiotropy.
<br>

<div class="figure" style="text-align: center">
<img src="/sc/arion/projects/LOAD/shea/Projects/MRcovid/results/MRcovideurwoukbb/Liu2019smkcpd/covidhgi2020A2v5alleurLeaveUKBB/Liu2019smkcpd_5e-8_covidhgi2020A2v5alleurLeaveUKBB_MR_Analaysis_files/figure-html/funnel_plot-1.png" alt="Fig. 2: Funnel plot of the MR causal estimates against their precession"  />
<p class="caption">Fig. 2: Funnel plot of the MR causal estimates against their precession</p>
</div>
<br>

Figure 3 shows a [Radial Plots](https://github.com/WSpiller/RadialMR) can be used to visualize influential data points with large contributions to Cochran's Q Statistic that may bias causal effect estimates.




```
## [1] "No significant Outliers"
```

<div class="figure" style="text-align: center">
<img src="/sc/arion/projects/LOAD/shea/Projects/MRcovid/results/MRcovideurwoukbb/Liu2019smkcpd/covidhgi2020A2v5alleurLeaveUKBB/Liu2019smkcpd_5e-8_covidhgi2020A2v5alleurLeaveUKBB_MR_Analaysis_files/figure-html/Radial_Plot-1.png" alt="Fig. 4: Radial Plot showing influential data points using Radial IVW"  />
<p class="caption">Fig. 4: Radial Plot showing influential data points using Radial IVW</p>
</div>
<br>

The intercept of the MR-Egger Regression model captures the average pleitropic affect across all genetic variants (Table 8).
<br>

**Table 8:** MR Egger test for directional pleitropy
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["chr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["chr"],"align":["left"]},{"label":["egger_intercept"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["se"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[7],"type":["dbl"],"align":["right"]}],"data":[{"1":"fipWw2","2":"51GJaT","3":"covidhgi2020A2v5alleurLeaveUKBB","4":"Liu2019smkcpd","5":"0.01206286","6":"0.01633334","7":"0.4687639"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

Pleiotropy was also assesed using Mendelian Randomization Pleiotropy RESidual Sum and Outlier [(MR-PRESSO)](https://doi.org/10.1038/s41588-018-0099-7), that allows for the evlation of evaluation of horizontal pleiotropy in a standared MR model (Table 9). MR-PRESSO performs a global test for detection of horizontal pleiotropy and correction of pleiotropy via outlier removal (Table 10).
<br>

**Table 9:** MR-PRESSO Global Test for pleitropy
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["chr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["chr"],"align":["left"]},{"label":["pt"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["outliers_removed"],"name":[6],"type":["lgl"],"align":["right"]},{"label":["n_outliers"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["RSSobs"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[9],"type":["dbl"],"align":["right"]}],"data":[{"1":"fipWw2","2":"51GJaT","3":"covidhgi2020A2v5alleurLeaveUKBB","4":"Liu2019smkcpd","5":"5e-08","6":"FALSE","7":"0","8":"35.53267","9":"0.0718"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>


**Table 10:** MR Estimates after MR-PRESSO outlier removal
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["chr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["chr"],"align":["left"]},{"label":["method"],"name":[5],"type":["chr"],"align":["left"]},{"label":["nsnp"],"name":[6],"type":["int"],"align":["right"]},{"label":["b"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["se"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[9],"type":["dbl"],"align":["right"]}],"data":[{"1":"fipWw2","2":"51GJaT","3":"covidhgi2020A2v5alleurLeaveUKBB","4":"Liu2019smkcpd","5":"Inverse variance weighted (fixed effects)","6":"22","7":"0.093330612","8":"0.2112967","9":"0.6587033"},{"1":"fipWw2","2":"51GJaT","3":"covidhgi2020A2v5alleurLeaveUKBB","4":"Liu2019smkcpd","5":"Weighted median","6":"22","7":"-0.009397694","8":"0.2711512","9":"0.9723520"},{"1":"fipWw2","2":"51GJaT","3":"covidhgi2020A2v5alleurLeaveUKBB","4":"Liu2019smkcpd","5":"Weighted mode","6":"22","7":"-0.095593396","8":"0.2551231","9":"0.7116444"},{"1":"fipWw2","2":"51GJaT","3":"covidhgi2020A2v5alleurLeaveUKBB","4":"Liu2019smkcpd","5":"MR Egger","6":"22","7":"-0.180847017","8":"0.4591016","9":"0.6978121"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

<div class="figure" style="text-align: center">
<img src="/sc/arion/projects/LOAD/shea/Projects/MRcovid/results/MRcovideurwoukbb/Liu2019smkcpd/covidhgi2020A2v5alleurLeaveUKBB/Liu2019smkcpd_5e-8_covidhgi2020A2v5alleurLeaveUKBB_MR_Analaysis_files/figure-html/scatter_plot_outlier-1.png" alt="Fig. 5: Scatterplot of SNP effects for the association of the Exposure on the Outcome after outlier removal"  />
<p class="caption">Fig. 5: Scatterplot of SNP effects for the association of the Exposure on the Outcome after outlier removal</p>
</div>
<br>

**Table 11:** Heterogenity Tests after outlier removal
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["chr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["chr"],"align":["left"]},{"label":["method"],"name":[5],"type":["chr"],"align":["left"]},{"label":["Q"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["Q_df"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["Q_pval"],"name":[8],"type":["dbl"],"align":["right"]}],"data":[{"1":"fipWw2","2":"51GJaT","3":"covidhgi2020A2v5alleurLeaveUKBB","4":"Liu2019smkcpd","5":"MR Egger","6":"32.68085","7":"20","8":"0.03656224"},{"1":"fipWw2","2":"51GJaT","3":"covidhgi2020A2v5alleurLeaveUKBB","4":"Liu2019smkcpd","5":"Inverse variance weighted","6":"33.57213","7":"21","8":"0.04024564"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

**Table 12:** MR Egger test for directional pleitropy after outlier removal
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["chr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["chr"],"align":["left"]},{"label":["egger_intercept"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["se"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[7],"type":["dbl"],"align":["right"]}],"data":[{"1":"fipWw2","2":"51GJaT","3":"covidhgi2020A2v5alleurLeaveUKBB","4":"Liu2019smkcpd","5":"0.01206286","6":"0.01633334","7":"0.4687639"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>
