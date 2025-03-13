# Nextflow_Map
![alt text](Screenshot.png "Mapping complete")
we often face the challange of index path while mapping our fastq. In this we try to overcome this nextflow challenge of index path issue for a one paired reads P7741_R1.fastq.gz and P7741_R2.fastq.gz

<br>
Database: https://www.ebi.ac.uk/ena/browser/view/ERR3335404 <br>
Accession number: `ERR3335404` <br>
Reference Sequence: `Agy99`  <br>

The error in the pipeline_map.nf script occurred due to incorrect channel declarations, causing type mismatches between String and FileSystem objects.

⚠ Issues Identified: <br>
1️⃣ Channel.fromPath{params.index_dir}<br>

Issue: Used {} instead of (), leading to incorrect evaluation. <br>
Fix: Channel.fromPath(params.index_dir) <br>
2️⃣ Channel.of(params.ref) <br>

Issue: Channel.of() is designed for lists, but params.ref is a single value. <br>
Fix: Channel.value(params.ref) <br>
3️⃣ Channel.fromFilePairs{params.fastq} <br>

Issue: Used {} instead of (), preventing correct pairing of FASTQ files. <br>
Fix: Channel.fromFilePairs(params.fastq) <br>

✅ Key Fixes Implemented: <br>
✔ Corrected channel declarations for index, ref, and fastq inputs.
✔ Ensured file paths are properly recognized without type mismatches.
✔ Resolved java.lang.String cannot be cast to java.nio.file.FileSystem error.
<br>
Final Outcome: <br>
After these corrections, the Nextflow script successfully runs without type conflicts, ensuring proper execution of the mapping process.
