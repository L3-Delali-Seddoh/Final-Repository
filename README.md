# Final-Repository

Lab 4 Code
•	mkdir ~/labs/lab4-myusername/pls1 –( Used to create a directory for my gene)
•	cd ~/labs/lab4-myusername/pls1- (Used to go to said directory)
•	iqtree -s ~/labs/lab3/pls1.homologs.al.fas -m VT+F+R10 –(Code to run an IQ tree)

•	nw_display pls1.homologs.al.fas.treefile  -(displays the IQ tree)

•	gotree draw png -w 1000 -i pls1.homologs.al.fas.treefile  -r -o  pls1.homologs.al.unrooted.png                                 (displays the unrooted tree)

•	gotree reroot midpoint -i pls1.homologs.al.fas.treefile -o pls1.homologs.al.mid.treefile        (Used to midpoint root the tree)

•	  nw_order -c n pls1.homologs.al.mid.treefile  | nw_display – (To view the rooted tree)

•	nw_order -c n hox.homologs.al.mid.treefile  |   nw_display  -w 1000 -b 'opacity:0' -s  >  hox.homologs.al.mid.svg -  (To draw the tree graphically)




Lab 5 Code
•	mkdir ~/labs/lab5-myusername/pls1 (to create a directory)

•	cp ~/labs/lab4-myusername/pls1/pls1.homologs.al.mid.treefile pls1.homologs.al.mid.treefile 
•	(to copy midpoint tree from lab4 folder)

•	java -jar ~/tools/Notung-3.0-beta/Notung-3.0-beta.jar -s ../speciesTreeBilateriaCnidaria.tre -g pls1.homologs.al.mid.treefile --reconcile --speciestag prefix --savepng –events  (to reconcile the gene tree)

•	python2.7 ~/tools/recPhyloXML/python/NOTUNGtoRecPhyloXML.py -g pls1.homologs.al.mid.treefile.reconciled --include.species  (to Generate a RecPhyloXML object to view the gene-within-species tree)

•	thirdkind -f hox.homologs.al.mid.treefile.reconciled.xml -o  pls1.homologs.al.mid.treefile.reconciled.svg (To create a gene-reconciliation-with species tree reconciliation using thirdkind)

•	java -jar ~/tools/Notung-3.0-beta/Notung-3.0-beta.jar -s ../speciesTreeBilateriaCnidaria.tre -g pls1.homologs.al.mid.treefile --root --speciestag prefix --savepng –events   ( to replace the --reconcile command with the --root flag to re-root the tree during using the reconciliation process.)




Lab6 Code

•	(To copy the alignment and tree files to the lab6 hox directory. )    cp ~/labs/lab4-myusername/pls1/pls1.homologs.al.fas ~/labs/lab6-myusername/hox/.
•	iqtree -s pls1.homologs.al.fas -nt AUTO -bb 1000 -m VT+F+R10 -t pls1.homologs.al.fas.treefile -pre pls1.bs -wbt

•	iqtree -t pls1.bs.ufboot -sup pls1.homologs.al.fas.treefile (to use the set of bootstrapped trees to add support values to our optimal tree)

•	gotree reroot midpoint -i pls1.bs.ufboot.suptree -o pls1.bs.mid.suptree
•	(to midpoint root the optimal tree)

•	nw_display -s  pls1.bs.mid.suptree -w 1000 -b 'opacity:0' >  pls1.bs.mid.suptree.svg
•	(To print out the tree to a graphics file with the bootstrap support)

•	cd ~/labs/lab6-myusername/pls1 (To go to directory)

•	sed 's/*//' ~/labs/lab3-myusername/pls1/pls1.homologs.fas > ~/labs/lab6-myusername/pls1/pls1.homologs.fas (to make a copy of our raw unaligned sequence)

•	wget -O ~/data/Pfam_LE.tar.gz ftp://ftp.ncbi.nih.gov/pub/mmdb/cdd/little_endian/Pfam_LE.tar.gz && tar xfvz ~/data/Pfam_LE.tar.gz  -C ~/data (To Download the Pfam database)

•	rpsblast -query ~/labs/lab3-myusername/pls1/pls1.homologs.fas -db /home/ec2-user/data/Pfam -out ~/labs/lab6-myusername/pls1/pls1.rps-blast.out  -outfmt "6 qseqid qlen qstart qend stitle"  (To  run RPS-BLAST)

•	awk 'BEGIN{FS="\t"} {print $1"\t"$2"\t"$3"@"$4"@"$5}' ~/labs/lab6-myusername/pls1/pls1.rps-blast.out | sed 's/,/_/g' | sed 's/ /_/g' | sed 's/__/_/g' | datamash -sW --group=1,2 collapse 3 | sed 's/,/\t/g' | sed 's/@/,/g' > ~/labs/lab6-myusername/pls1.rps-blast.evol.out (To reformat the output so that EvolView can use it)

•	cut -f 1 hox.rps-blast.out | sort | uniq -c (to Count the number of Pfam domains predicted for each protein)



