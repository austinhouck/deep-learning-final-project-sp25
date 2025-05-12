# Cornell Deep Learning Final Project - Spring 2025

## Introduction
This repo re-implements the watermarking described in the paper A Watermark for Large Language Models by Kirchenbauer and Geiping. The authors propose a method for detecting LLM-generated text through watermarking and z-scores to detect the watermark. The proposed watermarking is simple, compute-efficient, reproducable, and requires no knowledge of the model architecture. This was our work for the CS4782 final project.

## Chosen Result
We aim to reproduce the case studies presented in Table 1 of the paper, as well as the z-score vs. sequence length graphs for various $\gamma$ and $\delta$ values that are shown below. Together, these results highlight the fundamental challenge of balancing text quality against watermark robustness and show how parameter choices impact this trade-off.

![Paper results](/results/paper_results.png)

## GitHub Contents
This repo has the following structure:
- `code`: Includes the souce notebook file of our re-implementation.
- `data`: Includes the subset of data used to generate the case studies Table from the paper.
- `poster`: Includes the poster of the project.
- `report`: Includes the written report of the project.
- `results`: Includes the results generated in our re-implementation, as well as the paper results.

## Re-implementation Details
We implement two watermarking schemes: hard red-list and soft red-list watermarking. Both watermarking schemes randomly divide the next word's logits into a red and green list using the previous token as the seed. Hard red-list watermarking bans the use red tokens, while soft red-list watermarking adds $\delta$ to the logits in the green list. The green list size is based on $\gamma$.

We used the `c4` dataset and the `OPT-1.3B` model during our experiments. One challenge we faced was the model seemed to repeat itself at times, but we believe this is due to the small size of the model.

## Reproduction Steps
To run the code, we reccommend uploading `code/notebook.ipynb` to Google Colab and using the free T4 GPU. Running the code without a GPU will take a long time.

After uploading the file to Google Colab, run each cell in order to reproduce results.

Following libraries are used in the notebook. `code/notebook.ipynb` includes an install cell to install necessary requirements on Google Colab:
- `datasets`
- `torch`
- `transformers`
- `functools`
- `json`
- `math`
- `matplotlib`
- `numpy`

## Results/Insights
Our re-implementation closely replicates the results from the paper. Graphs below show how $\gamma$ and $\delta$ parameters impact the hard and soft watermarking implemented in our project:

![](/results/hard_watermark_gamma_sweep.png)
![](/results/soft_watermark_gamma_sweep.png)
![](/results/soft_watermark_delta_sweep.png)

These results show that with a longer sequence length, it is easier to detect a watermark. Aditionally, decreasing $\gamma$\ and increasing $\delta$ improves watermark detectability, at the cost of impacting text quality.

## Conclusion
In the context of the paper and the broader area of watermarking, our analysis shows that watermark detectability depends on sequence length and word choice. Priming the LLM to use specific words, either through restriction or by increasing logit scores, embeds a watermark in the output, but this comes at the cost of not allowing the LLM to choose the word it deems best, which results in worse text quality.

## References

1. J. Kirchenbauer, J. Geiping, Y. Wen, J. Katz, I. Miers, and T. Goldstein,
   *A Watermark for Large Language Models*, 2024.
   [Online] Available: https://arxiv.org/abs/2301.10226

2. J. Dodge, M. Sap, A. Marasovic, W. Agnew, G. Ilharco, D. Groeneveld, and M. Gardner,
   *Documenting the English Colossal Clean Crawled Corpus*, CoRR, vol. abs/2104.08758, 2021.
   [Online] Available: https://arxiv.org/abs/2104.08758

3. S. Zhang, S. Roller, N. Goyal, M. Artetxe, M. Chen, S. Chen, C. Dewan, M. Diab, X. Li, X. V. Lin,
   T. Mihaylov, M. Ott, S. Shleifer, K. Shuster, D. Simig, P. S. Koura, A. Sridhar, T. Wang, and L. Zettlemoyer,
   *OPT: Open Pre-trained Transformer Language Models*, 2022.
   [Online] Available: https://arxiv.org/abs/2205.01068
## Acknowledgements
This project was completed as a part of the coursework for CS4782 at Cornell University. We would like to thank the course instructors and course staff for their guidance throughout the semester.
