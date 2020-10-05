# SSBSE-FrDdE

The pre-print of our paper- "Using a Genetic Algorithm to Optimize Configurations in a Data driven Application" can be found at http://web.cs.iastate.edu/~mcohen/papers/ssbse20-preprint.pdf

The document 'Table description', contains the entity relationship diagram and the schema view of the major tables used for the study.

The csv files bear data for the MySql tables that were created and used for the study. The headers for all tables are provided. To replicate the tables in MySQL, run the queries provided below. Description of all table data (csv files):

1. null_hits.csv - These contain a list of all sequences (each identified by their unique sequence number) which found no hits/matches against the yeast database for a particular configuration sets (each identified by their unique configuration set number). Note that some sequences never found a hit for all 3000 configuration sets tested. There exist 19 such sequences in total.

2. bestF_Eq_Def.csv - This file gives us all the sequence numbers for which the default fitness is the best possible fitness score achievable amongst all 3,000 configurations tested per sequence. There exist 3,382 such cases/input sequences. For the remaining cases  out of 10,000 input sequences, there exist at least one 6,618 (or more) configuration which always fare better than the default. Headers for the file has been provided. For detailed information about the headers refer to the schema document.

3. config_dist.csv - This file contains each unique configuration no and their corresponding distance from the default configuration.

4. configuration.csv - This file contains the list of all 3000 possible configurations used in our experiment. the first column contains the configuration numbers while the consecutive columns bear the options for the following configurations: configno,dust,lcase_masking,soft_masking,ungapped,xdrop_gap,xdrop_gap_final,xdrop_ungap.

5. inputs.zip - The list of all 10,000 input sequences which were used for the experiment in BLASTn. Each file corresponds to a single sequence.

6. maxFitnessScorePerSequence.csv - This file contains the list of all sequence numbers and the corresponding maximum fitness score possible for each of the sequences.

7. yeast.GCF.zip - This file bears the NCBI databases used for the experiment. The database we used was Baker's yeast.

8. fitness.csv - This file contains a snapshot of the fitness table used for the study. The original fitness table has around 30 million records. The snapshot table has records for the first 10 input sequences and their corresponding 100 coconfiguration sets. It contains information about the hits, distance, average evalue, average percentage identity, median evalue, median percentage identity, w_distance, w_eval and the fitness score for the sequences and their corresponding configurations. 

9. blastn_output.csv - This file contains a snapshot of the blastn_output table used for the study. The original blastn_output table has over 30 million records. The snapshot table has records for the first 10 input sequences queried using the first 100 configuration sets in blastn. The original table contains information about the outcome of individual hits generated when blastn was ran for every single input sequence against all 3000 possible configuration sets.

10. AllBestF_perSequence.csv - This file contains the results of the best fitness scores per sequence along with their configuration numbers and their respective seven option's values.

#### Queries to create the above tables: 

1. configuration -
create table configuration (configNo int not null primary key, dust varchar(500) not null,lcase_masking varchar(500) not null,soft_masking varchar(500) not null,ungapped varchar(500) not null,xdrop_gap real not null,xdrop_gap_final real not null,xdrop_ungap real not null);

2. fitness - 
create table fitness(seqno int not null, configno int not null,hits int,distance int,averagepercid real(20,10),averageeval real(20,10), medianpercid real(20,10),medianeval real(20,10),w_dist real(20,10) w_eval real(20,10), fitnessScore real(20,10));
ALTER table fitness add primary key(seqno,configno);
ALTER table fitness add constraint fk_fitness_config foreign key (configno) references configuration(configno);

3. blastn_output - 
create table blastn_output(seqno int not null, configno int not null,hitno int not null,qseqid varchar(10000) not null, sseqid varchar(10000) not null,pident real(15,4) not null,length real not null,mismatch int not null,gapopen int not null,qstart int not null,qend int not null,sstart int not null,send int not null,evalue real(20,10) not null,bitscore real(20,10) not null,qhits varchar(10));
ALTER table fitness add primary key(seqno,configno,hitno);
ALTER table blastn_output add constraint fk_blastnOp_config foreign key (configno) references configuration(configno);

4. null_hits.csv - create table null_hits(seqno int not null, configno int not null);

5. maxFitnessScorePerSequence.csv - create table maxFitnessScorePerSequence(seqno int not null, fitnessScore real(20,10));

6. config_dist.csv - create table config_dist(configNo int not null, distance int not null);

7. bestF_Eq_Def.csv - create table bestF_Eq_Def(seqno int not null, configno int not null,distance int not null,medianpercid real(20,10) not null,medianeval real(20,10) not null,hits int not null, fitnessScore real(20,10) not null);

8. AllBestF_perSequence.csv - create table AllBestF_perSequence(seqno int not null,configno int not null,fitnessScore real(20,10),dust varchar(500) not null,lcase_masking varchar(500) not null,soft_masking varchar(500) not null,ungapped varchar(500) not null,xdrop_gap real not null,xdrop_gap_final real not null,xdrop_ungap real not null);

#### Load the data into the tables created:

1. LOAD DATA LOCAL INFILE 'configuration.csv' INTO TABLE configuration FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n';
2. LOAD DATA LOCAL INFILE 'fitness.csv' INTO TABLE fitness FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n';
3. LOAD DATA LOCAL INFILE 'blastn_output.csv' INTO TABLE blastn_output FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n';
4. LOAD DATA LOCAL INFILE 'null_hits.csv' INTO TABLE null_hits FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n';
5. LOAD DATA LOCAL INFILE 'maxFitnessScorePerSequence.csv' INTO TABLE maxFitnessScorePerSequence FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n';
6. LOAD DATA LOCAL INFILE 'config_dist.csv' INTO TABLE config_dist FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n';
7. LOAD DATA LOCAL INFILE 'bestF_Eq_Def.csv' INTO TABLE bestF_Eq_Def FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n';
8. LOAD DATA LOCAL INFILE 'AllBestF_perSequence.csv' INTO TABLE AllBestF_perSequence FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n';

#### Acknowledgments:

This work is supported in part by This work is supported in part by NSF Grant CCF-1901543 and by The Center for Bioenergy Innovation (CBI) which is supported by the Office of Biological and Environmental Research in the DOE Office of Science.

Any opinions, findings, and conclusions or recommendations expressed in this material are those of the author(s) and do not necessarily reflect the views of the National Science Foundation or the Department of Energy.
