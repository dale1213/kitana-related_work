# kitana-related_work
In this repo, we collect, build, and test the related work for Kitana

## Table of Contents

## Related Work
- [SEMA-Join](
    https://github.com/Yeye-He/Semantic-Join?tab=readme-ov-file
    ): A semantic-aware join algorithm for semantic related join operations. [Details](#sema-join), [Paper](https://github.com/Yeye-He/Semantic-Join?tab=readme-ov-file)


## SEMA-Join
### Overview
- The semantic-aware join algorithm converts the join problem into a optimization problem. It aims to maximize the aggregated semantic similarity of the join results. This similarity score can be calculated in two ways: row and column. 
- When talking about rows, it calculates the similarity of the rows in the join results. 
$$
PMI(r_i, s_j ) = \log \frac{p (r_i, s_j )}{p(r_i)p(s_j)}
$$
- For columns, it is a bit differnet. In the article, it uses PMI to calculate the similarity. Specifically, it calculates the probability of two pairs of value appears in the same dataset (but in two different columns). The PMI is defined as follows:
$$
PMI((r_i, s_j ),(r_k, s_l)) = \log \frac{p ((r_i, s_j ),(r_k, s_l))}{p(r_i, s_j )p(r_k, s_l)}
$$
- Then it uses the row PMI as the optimization function to maximize the similarity of the join results. Basically, the paper converts it to a quadratic programming problem:
$$
\max \sum_{\substack{r_i, r_k \in R, i \neq k \\ s_j, s_l \in S}} w_{ijkl} x_{ij} x_{kl}
$$
$$
\text{s.t.} \quad \forall i, \sum_{s_j \in S} x_{ij} \leq 1
$$
$$
x_{ij} \in \{0, 1\}
$$
- It then converts it to its duel problem and solves it by losening it to a linear programming problem (it rounds the solution to {0, 0.5, 1}).