# SSBSE-FrDdE

The ER-diagram file contains the entity relationship diagram for the major tables that were used for the study.
The data sheet () contains information about the reports generated from the study and used for answering the research questions.

The csv files bear data for the MySql tables that were created and used for the study. The headers for all tables are provided. To replicate the tables in MySQL, run the queries provided below. Description of all table data (csv files):

1. null_hits.csv - These contain a list of all sequences (each identified by their unique sequence number) which found no hits/matches against the yeast database for a particular configuration sets (each identified by their unique configuration set number). Note that some sequences never found a hit for all 3000 configuration sets tested. There exist 19 such sequences in total.

2. bestF_Eq_Def.csv - This file gives us all the sequence numbers for which the default fitness is the best possible fitness score achievable amongst all 3,000 configurations tested per sequence. There exist 3,382 such cases/input sequences. For the remaining cases  out of 10,000 input sequences, there exist at least one 6,618 (or more) configuration which always fare better than the default. Headers for the file has been provided. For detailed information about the headers refer to the schema document.

3. config_dist.csv - This file contains each unique configuration no and their corresponding distance from the default configuration.

4. configuration.csv - This file contains the list of all 3000 possible configurations used in our experiment. the first column contains the configuration numbers while the consecutive columns bear the options for the following configurations: configno,dust,lcase_masking,soft_masking,ungapped,xdrop_gap,xdrop_gap_final,xdrop_ungap.

5. inputs.zip - The list of all 10,000 input sequences which were used for the experiment in BLASTn. Each file corresponds to a single sequence.

6. maxFitnessScorePerSequence.csv - This file contains the list of all sequence numbers and the corresponding maximum fitness score possible for each of the sequences.

7. null_hits.csv - These contain a list of all sequences (each identified by their unique sequence number) which found no hits/matches against the yeast database for a particular configuration sets (each identified by their unique configuration set number). Note that some sequences never found a hit for all 3000 configuration sets tested. There exist 19 such sequences in total.

8. yeast.GCF.zip - This file bears the NCBI databases used for the experiment. The database we used was Baker's yeast.

9. fitness.csv - This file contains a snapshot of the fitness table used for the study. (The original fitness table has over 10 million records). It contains information about the hits, distance, average evalue, average percentage identity, median evalue, median percentage identity, w_distance, w_eval and the fitness score for the first 10 sequences and their corresponding 100 configurations. 

10. blastn_output.csv - 

Queries to create the above tables: 

1. 
