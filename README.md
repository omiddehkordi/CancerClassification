data.csv was too large to commit

Healthcare Capstone Write-Up
1) Clustermap would be better after PCA, because it is difficult to get any insights from a clustermap representing a little over 20k genes.
2) Hypothesis Testing
  a) T-test -> One cancer type vs all in terms of gene expression
    i) Result: There were significant differences between each cancer type and the rest
  b) F-test/ANOVA -> Test overall differences between cancer types in gene expression
    i) Result: There were significant overall differences between cancer types
3) Dimensionality Reduction (train_test_split before for good practice)
  a) PCA
    i) Did 25 components as an arbitrary number
    ii) Did PCA for dataset and transposed dataset in order to use it for clustering all samples and all genes
  b) LDA and t-SNE
    i) Did 2 components
  c) Ended up using PCA data for Clustering and Classification algorithms because it is more efficient than t-SNE and it doesn’t need class labels like LDA
4) Clustering
  a) I used the pca data for the normal data set to cluster for all samples
    i) Results: Both the Hierarchical Clustering and KMeans clustering performed well and clustered the samples into similar Cancer Groupings as the labeled data. The KMeans Scatter Plot shows some overlap among 3 of the groups. The Mean Shift Clustering didn’t provide as much of an insight, because it took too long to cluster.
  b) The transposed pca data was used for clustering all the genes
    i) Results: The column added to the transposed genes dataset shows the grouping for each gene
5) Classification Algorithms
  a) Neural Network
    i) I used a Label Encoder for the Class Column for the training and test data for the Neural Network
    ii) I used a different train_test_split, because Deep Neural Networks don’t require feature selection, because it is done in its layers
    iii) The algorithm performed well with about .98 accuracy for training data and 1.0 accuracy for validation data. The accuracy values seem high which might be a result of not enough data per sample class or due to overfitting problems
  b) Random Forest
    i) I used the pca data for random forest and the algorithm performed relatively well with around a .88 accuracy which slightly improved on some iterations when using the feature selection algorithms, but not by much. This indicates PCA did a relatively good job in reducing the dimensions. However, the algorithm couldn’t identify COAD samples which might be due to it having the least samples available for training and testing. Feature Selection didn’t seem to help with this
  c) Multiclass SVM (SVC)
    i) I used the same data as for the Random Forest Classifier and the algorithm performed very well with 1.0 accuracy which is most likely due to there not being enough test data.
  d) T-test one vs all and F-test
    i) All the F-test values show that there are significant differences among the genetic components resulting from PCA and Feature Selection
    ii) The T-test values differ
      (1) Random Forest Forward Selection T-test -> All components except the last 3 have significant differences
      (2) Random Forest Backward Elimination T-test -> Half the components have significant differences and the other half don’t
      (3) Multi-class SVM Forward Selection T-test -> All components except the last 2 have significant differences

Final Notes: All the classification algorithms perform fairly well, but due to the amount of data available it can’t be said how well they would perform with vast test data. The Dimension Reduction functions helped a lot in making the Random Forest and SVM algorithms more accurate. The cluster algorithms were fairly accurate in the clusters they made in terms of each sample being clustered with the corresponding Cancer type.
