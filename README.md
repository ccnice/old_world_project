# old_world_project
Lycaeides (Plebejus) Holarctic GBS data
basic project outline:
1. assemble and call variants for all OW samples + N. American samples for autosome phylogenomics
2. assemble and call variants for non-argus OW samples + N. American samples - autsomes 
3. assemble and call variants for non-argus OW samples + N. American samples - Z chromosome - calculate and compare coverage for autosomes vs Z to figure out females for the old world samples
4. entropy, angsd for diversity

| Group | Location | State | Code | n |
|-------|----------|-------|------|---|
| old world| Europe /  Asia|  | various | 367 (79 P. argus)|
| Karner | Fort McCoy | WI | fmc | 23 |
| Karner | Saratoga Springs | NY | ssn | 19 |
| Anna | Leek Springs | CA | lks | 20 |
| Anna | Yuba Gap| CA | ybg | 19 |
| Idas | Cottonwood Divide| WA | cwd | 25 |
| Idas | Strawberry Mts.| OR | stb | 17 |
| Nabokovi | Railroad| MN | rrm | 23 |
| Nabokovi | Sawbill| MN | sbm | 10 |
| Ricei | Big Lake| OR | big | 18 |
| Ricei | Chinook Pass| WA | chp | 24 |
| Jackson Hybrids | Blacktail Butte| WY | btb | 20 (subset of 44 total) |
| Jackson Hybrids | Bull Creek| WY | bcr | 20 (subset of 39 total) |
| Whites/Sierra Hybrids | Carson Pass| CA | csp | 20 (subset of 48 total) |
| Whites/Sierra Hybrids | County Line Hill| CA | clh | 20 (subset of 40 total) |
| Warners Hybrids | Buck Mt.| CA | bkm | 20 (subset of 35 total) |
| Warners Hybrids | Eagle Pk.| CA | egp | 20 (subset of 35 total) |
| Melissa Rockies | Lander| WY | lan | 23 |
| Melissa Rockies | Yellow Pine CG| WY | ywp | 16 |
| Melissa East | Brandon| SD | bsd | 18 |
| Melissa East | Montague| CA | mtu | 20 (all from 2017, not 2007) |
| Melissa West | Verdi Crystal Peak Park| NV | vcp | 20 (subset, first 20 from 2018, of 72 total) |
| Melissa West | Deer Mountain Rd.| NV | der | 20 (subset of 25 total) |
| Idas Alaska | Nolan Rd.| AK | nol | 8 |
| Idas Alaska | Spruce Barley| AK | sbw | 20 |
| Idas Alaska | Tok| AK | tok | 14 |
| Idas Alaska | Tolvana Creek| AK | tol | 8 |
| `Total` | |  | | `852` (773 w/o P. argus)|

19xii21

Assembly using bwa mem to dovetail_pacbio Lycaeides reference

```
> table(substr(dat$V1,1,3))

alk alq arg arm aze azo bcr bie big bka bkm bsd btb bul byj cdv cer cga chp cji 
  1   1   2  10   1   5  20   1  18   3  20  18  20   2   1  17   1   2  24  10 
clh cma cpq csp cwd cze der dja dvu edc egp elb elz erb erm fcg fcl fmc fvi fvy 
 20   7   1  20  25   2  20   1   2   1  20   8   1   5  11  10   1  23   1   1 
gen gru gsk gua hod ias ica iip ilm imo ira iro ise jas jav jpa kal kam kha khm 
  4   1   1   1   1   5   1   1   1   1   2   1   3   1   1   1   3   1   4   1 
kii kit kpc kpn kpr kpu kra ktm kun lan lau ldv lks lpi lss lzk men mnk mtu muk 
  1  13   1   1   1   1   1   9   3  23  20  10  20   1   9   7  12   1  20  10 
nie nkk nol npi ops ore oro par pdb pdr pds pmt pzo rad rpa rrm sbm sbt sbw sck 
  4  10   8   1   1   6   1  10   5   1  10   1   1   1  22  23  10   2  20   2 
shl sod spb spi srd ssn stb tas tkk tok tol uka upi ups upy vcp vel ybg ywp 
  1   1   4  10   2  19  17  10  10  14   8   1   1   1   2  20   1  19  16 

```
```
11.24
chris@anna:/Volumes/storage_a1/Parsed_reads_storage/all_the_fastqs$ perl runbwa_mem_forks_list_pacbio_OW.pl FINAL_OWlist.txt &
[1] 207046
```
DONE 23.42

####### 20xii21
```
11.00
chris@anna:/Volumes/storage_a1/Parsed_reads_storage/all_the_fastqs$ perl runbwa_mem_forks_Z_list_pacbio_OW.pl FINAL_OWlist.txt &
[1] 244722
```
DONE 16.25
moved to data_a3

############ 21xii21
8.59
```
chris@anna:/Volumes/data_a3/oldWorld/varCall/autosomes$ perl /Volumes/programs/scripts/sam2bam.pl *.sam &
[1] 287845
```
DONE 11.38
```
rm *.sam
```
14.38 
```
chris@anna:/Volumes/data_a3/oldWorld/varCall/Zchromosome$ perl /Volumes/programs/scripts/sam2bam.pl *.sam &
[1] 297192
```
DONE 16.56
###### 22xi21
Variant calling

9.53
```
chris@anna:/Volumes/data_a3/oldWorld/varCall/autosomes$ bcftools mpileup -d 8000 -o out1.bcf -O b -I -f /Volumes/data_a1/melissaGenomes/pacbio_dovetail_reference/autosomes_unassigned_Lmel_dovetailPacBio_genome.fasta aln*sorted.bam &
[1] 308611
```

9.57
```
chris@anna:/Volumes/data_a3/oldWorld/varCall/Zchromosome$ bcftools mpileup -d 8000 -o out1.bcf -O b -I -f /Volumes/data_a1/melissaGenomes/pacbio_dovetail_reference/scaff1631_Z_pacbio.fasta aln*sorted.bam &
[1] 308787
```
