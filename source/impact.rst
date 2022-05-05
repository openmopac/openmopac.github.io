Scientific Impact
=================

Summarize our approach to measuring the scientific impact of MOPAC.

Eventually, include statistics on the rate of MOPAC downloads.

Graph of MOPAC journal references as a function of time.

.. image:: /impact/plot.pdf
   :alt: A plot of MOPAC references in the scientific literature versus time, rising steadily from 1984
         to a peak in 1996 just over 1000 per year, and gradually declining to around 600 per year in the present day.

..
  We use Google Scholar with the simple, inclusive search term of only "MOPAC" and randomly sample these results
  to estimate the probability that a result is a valid scientific publication referring to MOPAC. This methodology
  incurs an unbiased statistical error, and the leading bias is that this probability is not constant with time
  even though we assume it to be so (& we can't account for double-counting & other non-uniformity).
  We are excluding preprints, technical reports, and theses from this analysis, focusing on published papers & proceedings.
  The estimated probability is 0.72 +/- 0.03 from 200 samples in the interval 1984-2020,
  sampled uniformly over years and sampled uniformly over papers published within each year.
  This sampling scheme was chosen because Google Scholar only provides detailed information for the first 1000 search results,
  and MOPAC is cited frequently enough that multi-year searches exceed this cap.
  NOTE: for more recent searches, we use the search string 'MOPAC OR "MOPAC2007" OR "MOPAC2009" OR "MOPAC2012" OR "MOPAC2016"'
        because Google Scholar can't parse "MOPAC" as being part of these other, more recent synonymous software names

An actively updated list of new papers making reference to MOPAC.

Note the methodology for calculating these metrics in the page source.

..
  The .bib files for the post-2020 impact lists are annotated (annote block) with keywords to help with usage statistics:
  cite-code = paper cites the MOPAC code in some way (QCPE, journal, manual, or website)
  cite-model = paper cites the semiempirical model that they use
  developer = paper about development of a feature in MOPAC or tightly coupled with MOPAC
  drc = used dynamical reaction coordinate method
  dubious = paper claiming to use MOPAC for something it isn't capable of doing [e.g. DFT calculations]
  foreign = paper is written in a foreign language
  gui = MOPAC was used through a GUI,
        = chem3d [Cambridge Soft, defunct product]
        = chemdes [http://www.scbdd.com/chemdes/]
        = codessa [http://www.semichem.com/codessa/default.php] (dubious: this is a GUI for AMPAC, not MOPAC)
        = drudit [https://www.drudit.com/]
        = gabedit [http://gabedit.sourceforge.net]
        = insight [https://www.3ds.com/products-services/biovia/products/data-science/biovia-insight/]
        = jmol [http://jmol.sourceforge.net/]
        = lumpac [https://lumpac.pro.br]
        = maestro [https://www.schrodinger.com/products/maestro]
        = mercury [https://www.ccdc.cam.ac.uk/solutions/csd-core/components/mercury/]
        = moe [https://www.chemcomp.com/index.htm]
        = molclus [http://www.keinsci.com/research/molclus.html]
        = scigress [https://www.fqs.pl/en/chemistry/products/scigress]
        = spartan [https://www.wavefun.com/products/spartan.html]
        = sybylx [https://www.g6g-softwaredirectory.com/bio/proteomics/structure-modeling/20710-Tripos-SYBYL-X-Suite.php]
        = tmolex [https://www.3ds.com/products-services/biovia/products/molecular-modeling-simulation/solvation-chemistry/turbomoler/]
        = winmostar [https://winmostar.com/en/]
  mozyme = paper states that MOZYME was used
  no-access = the full text of the paper couldn't be accessed to determine an annotation at the time of data collection,
              but a Google Scholar search indicated that MOPAC was mentioned (false-positive rate on chemistry-related papers is <1%)
  no-calc = MOPAC is mentioned in the paper, but no MOPAC calculations are reported
  qsar = MOPAC was part of a QSAR study
  supp-only = the full text of the paper couldn't be accessed, but the supplementary material was accessible

2021
----

.. bibliography:: impact/impact.bib
   :list: enumerated
   :filter: year % "2021"
