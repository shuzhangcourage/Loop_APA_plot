# Loop_APA_plot
the loop plot depend on the juicertools APA function. Please install juicetool before use it.
Actually, this scripts just normalize the value from juicetool APA function, because from APA we get total interactions not average, and total is not good to compare.

# APA
java -Djava.awt.headless=true -Xmx32000m -jar juicer_tools_1.13.02.jar apa  -c 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,X -r 10000 -k KR -q 3 \
-w 6 -n 15 -u  inter_30.hic loop.bedpe outfold

from APA function you will get a file called APA.txt, we need this one. This file count the matrix to plot.

# normalize a bit 
python 01_tidy_APAvalue.py APA.txt APA.average number_of_loops_after_filter

usually -n parameter from APA means how many bins are excepted from using. eg, 15 means 15*binsize=150000, so it filters under 150kb loops
and the number_of_loops_after_filter is the number of loops be counted. 
This step just calculate average signal. You also get a maximum from this step, if you want to compare different samples, 
add a maximum in your heatmap will help make signal at same level!

python 02_tidy_APA_heatmap.py APA.average outfile.heatmap maximum_from_01_step

./03_heatmap.R --input outfile.heatmap --output out.pdf
