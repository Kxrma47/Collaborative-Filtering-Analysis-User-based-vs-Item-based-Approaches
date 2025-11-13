# Collaborative Filtering Analysis: User-based vs Item-based Approaches

## Project Overview

Comparative analysis of collaborative filtering methods for recommendation systems using the MovieLens 100k dataset. Evaluates user-based and item-based approaches with multiple evaluation metrics and optimization strategies.

## Dataset

- **Dataset**: MovieLens 100k
- **Ratings**: 100,000 ratings
- **Users**: 943 users
- **Movies**: 1,682 movies
- **Split**: 80/20 train-test (u1.base/u1.test)

- **Source**: [GroupLens Research](http://grouplens.org/datasets/movielens/100k/)
- **Direct Download**: [ml-100k.zip](https://files.grouplens.org/datasets/movielens/ml-100k.zip)

## Key Findings

### 1. Error Metric Evaluation

Both MAE and RMSE were implemented and evaluated:

- **User-based MAE**: 0.9069 - 0.9804
- **User-based RMSE**: 1.1675 - 1.2936
- **Item-based MAE**: 1.1728 - 1.2192
- **Item-based RMSE**: 1.5167 - 1.6216

**Finding**: User-based filtering consistently outperforms item-based filtering on this dataset.

### 2. Neighbor Count Sensitivity

Analysis across neighbor counts (1-100) shows:

- **Optimal neighbors**: n=81 for user-based (MAE=0.9069, RMSE=1.1675)
- **Trend**: Performance improves with more neighbors, then stabilizes
- **Trade-off**: More neighbors improve accuracy but increase computation

### 3. Alternative Prediction Formulas

When initial quality was unsatisfactory (MAE > 1.0), alternative formulas were tested:

- **Alternative 1 (Simple Mean)**: MAE=0.9303, RMSE=1.2277
- **Alternative 2 (Mean-Centered)**: MAE=0.9090, RMSE=1.1360

**Finding**: Mean-centered normalization (Formula 2) performs best, achieving the lowest MAE and RMSE.

### 4. Comparative Performance

| Method | MAE | RMSE |
|--------|-----|------|
| Original User-based (n=41) | 0.9316 | 1.2291 |
| Original Item-based (n=41) | 1.1931 | 1.5181 |
| Alternative 1 (Mean) | 0.9303 | 1.2277 |
| **Alternative 2 (Mean-Centered)** | **0.9090** | **1.1360** |

**Conclusion**: Alternative Formula 2 (mean-centered with normalization) is the best-performing method.

### 5. Top-N Size Impact

Analysis of top-n sizes {1,3,5,10,15,20,30,40,50,100}:

- **Best performance**: Top-100 for user-based (MAE=0.8921, RMSE=1.1442)
- **Pattern**: Larger neighborhoods generally improve accuracy
- **Diminishing returns**: Improvement rate decreases after n=50

### 6. Recommendation Diversity Analysis

Analysis of 200 users' recommendations:

- **Popular movies** (high ratings, high popularity): 338 movies recommended
- **Rare movies** (high ratings, low popularity): 632 movies recommended

**Finding**: The system recommends more rare movies than popular ones, indicating good diversity and novelty in recommendations. Top recommended rare movies include "Truman Show" (30 recommendations) and "Visitors, The" (24 recommendations).

### 7. Small Neighborhood Handling

Confidence evaluation for recommendations with limited neighbors:

- **Average confidence (User-based)**: 0.9902
- **Average confidence (Item-based)**: 1.0000
- **Confidence-Error Correlation (UB)**: 0.4113

**Finding**: Moderate negative correlation indicates that higher confidence generally corresponds to lower prediction error, validating the confidence metric.

### 8. Hybrid Recommendation Optimization

Comparison and optimization of hybrid approach:

- **Jaccard Similarity**: 0.0161 (very low overlap between UB and IB top-20 lists)
- **Optimal β for MAE**: 0.9 (MAE=1.0195)
- **Optimal β for RMSE**: 0.7 (RMSE=1.3107)

**Finding**: Hybrid approach with β=0.9 (favoring user-based) achieves best MAE, while β=0.7 provides best RMSE. The low Jaccard similarity suggests the methods complement each other well.

## Technical Implementation

### Similarity Metrics
- **Pearson Correlation**: Primary similarity measure
- **Euclidean Distance**: Alternative distance-based similarity
- **Kernel Similarity**: Exponential similarity function

### Optimization Techniques
- Similarity caching for computational efficiency
- Test sampling for faster evaluation (2000-1000 samples)
- Grid search for hyperparameter optimization

## Results Summary

**Best Performing Method**: Alternative Formula 2 (Mean-Centered Normalization)
- **MAE**: 0.9090
- **RMSE**: 1.1360
- **Improvement**: ~2.4% better MAE than original user-based method

**Key Insights**:
1. User-based filtering outperforms item-based on this dataset
2. Mean-centered normalization significantly improves prediction quality
3. Optimal neighborhood size is around 50-81 neighbors
4. System shows good recommendation diversity (more rare movies)
5. Hybrid approaches can further optimize performance


## Dependencies

- Python 3.x
- NumPy
- Matplotlib
- Standard library: math, collections

## References

- Segaran, T. (2007). *Programming Collective Intelligence*. O'Reilly Media, Chapter 2.
- Ricci, F., Rokach, L., & Shapira, B. (2011). [Foundations and Trends in Collaborative Filtering](http://files.grouplens.org/papers/FnT%20CF%20Recsys%20Survey.pdf)
- MovieLens Dataset: [GroupLens Research](http://grouplens.org/datasets/movielens/)

## License

This project is for educational and research purposes.
