# MetFrag Hands-on

**Topic:** Using MetFrag for compound identification with MS/MS data and additional information.

A online training presentation is available [here](https://ipb-halle.github.io/MetFragTraining/).

---

In this hands-on session you will learn how to use MetFrag to annotate MS/MS spectra as a first 
step to identify a molecular structure given MS and MS/MS information. Furthermore, we will use
additional experimental and meta data to support a putative identification.

---

## MetFrag webservice workflow

In this example we have extracted a feature from a water (river) sample from a LC-MS/MS measurement
with a precursor m/z&nbsp;230.1162 at retention time 10.1&nbsp;minutes. The data is acquired on a
LTQ Orbitrap XL with a high mass accuracy (&lt;5ppm) in positive ion mode. The adduct type of the 
selected precursor ion is known as \[M+H\]⁺.

Please download the prepared data:

* MS1: <a href="handson_data/ms1_mz230.1162_rt10.1.txt" download>ms1_mz230.1162_rt10.1.txt</a>
* MS2: <a href="handson_data/ms2_mz230.1162_rt10.1.txt" download>ms2_mz230.1162_rt10.1.txt</a>

---

## *Step 1 - Run initial MetFrag processing*

#### 1 a) Retrieve Candidates from database
- visit the MetFragWeb tool in your browser 
<a href="https://msbi.ipb-halle.de/MetFrag" target="_blank">https://msbi.ipb-halle.de/MetFrag</a>
- define database settings to retrieve candidates given the MS1 information:
	1. use the precursor m/z value and type to calculate the neutral monoisotopic mass
	2. check mass accuracy
	3. select PubChemLite in the "Local Databases" section as compound database
- start a candidate retrieval by clicking "Retrieve Candidates"

---

<video controls preload> 
    <source src="media/cast1.webm"></source> 
    <div>
         <img src="media/image1.png" alt="Retrieve Candidates" />
    </div>
</video>

<a href="https://msbi.ipb-halle.de/MetFrag/landing.xhtml?FragmentPeakMatchAbsoluteMassDeviation=0.001&FragmentPeakMatchRelativeMassDeviation=5&DatabaseSearchRelativeMassDeviation=5&PeakList=57.06984_29;61.97913_88;68.02435_999;71.0604_228;79.00582_486;90.01058_17;96.05565_432;104.00108_999;110.04612_66;128.05657_6;132.03232_422;138.0775_129;146.02289_393;172.0386_4;174.05425_999;230.11679_999&IonizedPrecursorMass=230.1162&MetFragDatabaseType=PubChem" target="_blank">Go to live demo</a>

---

- MetFrag searches candidates matching the information given by the "Database settings" (here: Neutral Mass and 5 ppm deviation)
- after the retrieval you can download the candidate list as CSV or XLS to get a first overview about the retrieved data set

---

#### 1 b) Process candidates by performing *in silico* fragmentation and matching to MS/MS data

- use the "Fragmentation settings" tab to add the given MS2 peak list
- you can visualize the peak list by clicking on the "Show Spectrum" button
- keep the settings for the *in silico* fragmentation and start the processing by clicking "Process Candidates"

---

<video controls preload>
    <source src="media/cast2.webm"></source>
    <div>
         <img src="media/image3.png" alt="MS2 peak list" />
         <br>
         <img src="media/image4.png" alt="MS2 peak list" />
    </div>
</video>

---

- MetFrag now generates fragments for each candidate up to the specified tree depth
- the fragments are mapped to the MS/MS peak list (based on mass) which is used to calculate a score for each candidate
- after the processing is finished you see the ranked candidates list in the "Results" tab
- here you have different possibilities:
    - you can filter candidates by explained peaks
    - investigate explained fragments and calculated scores for each candidate
    - download ranked candidate list as CSV or XLS file

---

<video controls preload>
    <source src="media/cast3.webm"></source>
    <div>
         <img src="media/image6.png" alt="Results" />
    </div>
</video>

---

*Questions:*

Q1: How many different molecular formulas are present?

Q2: What do you think is the correct molecular formula? 

Q3: What else could you do to verify the molecular formula besides using the given MetFrag results?

--

Visit http://www.envipat.eawag.ch/index.php and verify your molecular formula.

---

## *Step 2 - Run MetFrag processing using molecular formula*

#### 2 a) Retrieve Candidates from database

- use the same settings as in 1 a) but add the molecular formula
- also select "Include references" when using PubChem

---

<img src="media/image7.png" alt="Retrieve Candidates with formula" />

<a href="https://msbi.ipb-halle.de/MetFrag/landing.xhtml?FragmentPeakMatchAbsoluteMassDeviation=0.001&FragmentPeakMatchRelativeMassDeviation=5&DatabaseSearchRelativeMassDeviation=5&PeakList=57.06984_29;61.97913_88;68.02435_999;71.0604_228;79.00582_486;90.01058_17;96.05565_432;104.00108_999;110.04612_66;128.05657_6;132.03232_422;138.0775_129;146.02289_393;172.0386_4;174.05425_999;230.11679_999&MetFragDatabaseType=PubChem&NeutralPrecursorMolecularFormula=C9H16ClN5" target="_blank">Go to live demo</a>

---

#### 2 b) Process candidates by performing *in silico* fragmentation and matching to MS/MS data

- use the same settings as in 1 b) and process the candidates

---

*Questions:*

Q4: Looking at the results, what has changed compared to using the monoisotopic mass as candidate filter?

Q5: Is the molecular formula helpful here?

---

## *Step 3 - Run MetFrag adding additional experimental information*

#### 3 a) Add the retention time data model to the MetFragWeb tool

- adding additional information available from the experimental context is often helpful to verify a putative identification
- we want to add retention time as additional experimental information

---

- MetFrag includes a retention time model
- linear correlation of *n*-octanol/water partition coefficient([*logP*](https://en.wikipedia.org/wiki/Partition_coefficient)) and retention time
- candidate *logP* is predicted by XLogP3(retrieved from PubChem) or calculated by CDK's XLogP
- <a href="handson_data/retentiontime_model/rt_XlogP.csv" download>rt_XlogP.csv</a> contains a data set of measured rt and [*XLogP3*](https://www.ncbi.nlm.nih.gov/pubmed/17985865) values of 254 Eawag standards:
<img src="media/image8.png" alt="rt model" />

---

- upload the data set to the MetFragWeb tool in the "Candidate Filter & Score Settings" tab using the "Retention Time" panel on the right side (direct download: <a href="https://raw.githubusercontent.com/ipb-halle/MetFragTraining/master/handson_data/retentiontime_model/rt_XlogP.csv" download>rt_XlogP.csv</a>)

<img src="media/image9.png" alt="rt model setup" />

---

- after the file upload set the retention time of the precursor and select XLogP3 as partition coefficient which is used for correlation
- this results in an additional scoring term in the scoring function of MetFrag

---

#### 3 b) Process candidates by performing *in silico* fragmentation and matching to MS/MS data

-   use the same settings as in 2 b) and process the candidates

<img src="media/image10.png" alt="rt model results" />

---

*Questions:*

Q6: What has changed compared to the previous run?

Q7: Use the weight sliders in the "Results" tab. Does it change anything?

Q8: Is the retention time information helpful here?

---

## *Step 4 - Run MetFrag adding additional meta information*

#### 4 a) Add the additional scoring terms

- meta information can help to verify putative identifications depending on the experimental context
- however, you need to be careful when using this information which is not related to your acquired data
- in the "Candidate Filter & Score Settings" tab select the additional "Database Scoring Terms"
    - PubChemNumberPubMedReferences
    - PubChemNumberPatents

---

<img src="media/image11.png" alt="meta information setup" />

---

#### 4 b) Process candidates by performing *in silico* fragmentation and matching to MS/MS data

- use the same settings as in 3 b) and process the candidates

<img src="media/image12.png" alt="meta information result" />

---

*Questions:*

Q9: What has changed compared to the previous run?

Q10: Would the number of references and patents have helped for a metabolomics experiment?

Q11: Investigate the high intensity fragments of the first ranked candidate. Are they plausible compared to fragment structures of other candidates?

---

<img src="media/image13.png" alt="view fragments" />

---

## *Step 5 - Search in spectral libraries*

#### 5 a) Investigate MS/MS peaks in MassBank

- visit MassBank EU (<a href="https://massbank.eu" target="_blank">https://massbank.eu</a>)
- select the "Peak Search" and add the most intense explained peaks

---

<img src="media/image14.png" alt="massbank" />

- hitting "Search" to find spectra with matching peaks in the database

---

*Questions:*

Q12: Investigate the results and compare them to your MetFrag result list. Any conclusions?

---

## *Step 6 - Combine Spectra library search and MetFrag*

#### 6 a) Enable spectral similarity in MetFrag

-   in the "Candidate Filter & Score Settings" tab enable "Spectral Similarity"
-   MetFrag will now query the MS/MS peak list against a spectral library mirror to search for similar spectra of known compounds

---

<img src="media/image15.png" alt="spectral similarity setup" />

---

#### 6 b) Process candidates by performing *in silico* fragmentation and matching to MS/MS data

-   use the same settings as in 4 b) and process the candidates

<img src="media/image16.png" alt="spectral similarity results" />

---

**Questions:**

Q13: Discard the meta information scores to just use the results based on experimental data. Any conclusions?

---

## Exercise

- visit the CASMI contest site (<a href="http://www.casmi-contest.org/2017/challenges_1-45.shtml" target="_blank">http://www.casmi-contest.org/2017/challenges_1-45.shtml</a>)
- try to identify some of the compounds
- check your results <a href="http://www.casmi-contest.org/2017/solutions.shtml" target="_blank">here</a>

---

## Advanced exercise: using MetFrag on command line

- MetFrag can be used on command line to process batches of annotation tasks -- its called MetFragCLI
- parameter files for MetFragCLI can be created by web interface
- get your copy of MetFragCLI from <br>
<a href="http://ipb-halle.github.io/MetFrag/" target="_blank">http://ipb-halle.github.io/MetFrag/</a>
- setup one example calculation to retrieve a set of valid parameter

---

<img src="media/image17.png" alt="get parameter file" />

---

#### Prepare one directory with the required files for each annotation task
<!-- .slide: style="text-align: left;"> -->  

<pre><code class="bash">
~/course$ ls *
MetFrag2.4.2-CL.jar  MetFragWeb_Parameters.zip

data:
challenge-001-msms.txt  challenge-003-msms.txt  challenge-005-msms.txt  challenge-007-msms.txt  challenge-009-msms.txt
challenge-001-ms.txt    challenge-003-ms.txt    challenge-005-ms.txt    challenge-007-ms.txt    challenge-009-ms.txt
challenge-002-msms.txt  challenge-004-msms.txt  challenge-006-msms.txt  challenge-008-msms.txt
challenge-002-ms.txt    challenge-004-ms.txt    challenge-006-ms.txt    challenge-008-ms.txt

MetFragWeb_Parameters:
MetFragWeb_Parameters.cfg  MetFragWeb_Peaklist.txt  README.txt
</code></pre>


---

#### Prepare one directory with the required files for each annotation task

- slightly adjust MetFragWeb_Parameters.cfg to use ionized precursor mass
- works well in conjunction with "PrecursorIonMode" option

<!-- .slide: style="text-align: left;"> -->
<pre><code class="bash">
# 1 for M+H and -1 for M-H
PrecursorIonMode = 1 
FragmentPeakMatchRelativeMassDeviation = 5.0
SampleName = MetFragWeb_Sample
MetFragCandidateWriter = XLS
DatabaseSearchRelativeMassDeviation = 5.0
FragmentPeakMatchAbsoluteMassDeviation = 0.001
MetFragDatabaseType = PubChem
ResultsPath = .
#NeutralPrecursorMass = 272.068624
IonizedPrecursorMass = 272.068624
MetFragScoreTypes = FragmenterScore
MetFragScoreWeights = 1.0
MetFragPreProcessingCandidateFilter = UnconnectedCompoundFilter,IsotopeFilter
IsPositiveIonMode = true
MaximumTreeDepth = 2
NumberThreads = 1
UseSmiles = true
PeakListPath = MetFragWeb_Peaklist.txt
</code></pre>

---

#### Prepare one directory with the required files for each annotation task

- create the directories and populate with files

<!-- .slide: style="text-align: left;"> -->
<pre><code class="bash">
for x in `seq -f %03g 1 9`; do
 mkdir challenge-${x};
 cp data/challenge-${x}* challenge-${x};
 cp MetFragWeb_Parameters/MetFragWeb_Parameters.cfg challenge-${x};
 ln -s challenge-${x}-msms.txt challenge-${x}/MetFragWeb_Peaklist.txt;
done
</code></pre>

---

#### Prepare one directory with the required files for each annotation task

- inject precursor mass

<!-- .slide: style="text-align: left;"> -->
<pre><code class="bash">
for x in `seq -f %03g 1 9`; do
 mass=`head -n1 challenge-${x}/challenge-${x}-ms.txt | cut -f1`;
 sed -i 's|IonizedPrecursorMass =.*|IonizedPrecursorMass ='${mass}'|g' challenge-${x}/MetFragWeb_Parameters.cfg
done
</code></pre>

---

#### Run all MetFrag processes

<!-- .slide: style="text-align: left;"> -->
<pre><code class="bash">
for x in `seq -f %03g 1 9`; do
 cd challenge-$x;
 java -jar ../MetFrag2.4.2-CL.jar MetFragWeb_Parameters.cfg
 cd ..;
done
</code></pre>

--- 
