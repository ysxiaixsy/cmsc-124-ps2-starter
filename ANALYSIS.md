# Vector and Scalar Evaluation

Both functions keeps the names and turns the raw scores given to them into adjusted scores, which replaces missing scores with 0 and doubles other scores. Then cleans the scores capped at 20. 

`clean_scores_vector()` implements this score transformation on all scores at once, similar to P14 in the case predictions. Each line acts on the scores. For instance, in the given sample scores, `c(Ada = 8, Grace = NA_real_, Linus = 12, Barbara = 4)`, the scores double because of this line `clean_vout <- scores*2`, making it: Ada = 16, Grace = NA, Linus = 24, Barbara = 8. `clean_vout[is.na(scores)] <- 0` line replaces the missing values with 0, so Grace's score will be `0` instead of `NA`. Then, `clean_vout [clean_vout > 20] <- 20` caps the scores at 20, anything that is greater than 20 is replaced by 20, making Linus' score becomes 20 at maximum. Names are still attached because the doubling and subassignment only change the values. Hence, the result in the end of the adjusted scores is:

Ada   Grace   Linus   Barbara
16      0       20       8

`clean_scores_scalar()` ...

Keeping vector evaluation implementation in an R program is faster compared to the scalar evaluation, as it acts on the scores all at once, unlike in scalar that loops through the number of items one-by-one.