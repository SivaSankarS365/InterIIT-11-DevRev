# Inter IIT 11.0 Tech Meet
# Expert Answers in a Flash: Improving Domain-Specific QA

This project, awarded a gold medal out of 19 participating IITs, presents an innovative solution for domain-specific question answering (DSQA). Our method, **Retrieve Twice, Rank, and Answer (R2RA)**, emphasizes both efficiency and performance, making it suitable for real-time deployment.

## Code Structure

### Models
- **reader.py**: Handles the extraction and understanding of answers from the text.
- **retriever.py**: Manages the retrieval of relevant documents.
- **retrievers**:
  - **dpr.py**: Implements Dense Passage Retrieval (DPR) for capturing semantic information.
  - **sparse.py**: Utilizes sparse retrieval techniques for efficient lexical matching.
  - **colbert.py**: Applies ColBERT for fine-grained interaction and similarity scoring.
  - **voting.py**: Implements a voting strategy for combining results from different retrievers.
  - **crossencoder.py**: Uses cross-encoders for detailed scoring and ranking of documents.

## Installation

To get started, clone the repository and run the setup script:

```bash
git clone https://github.com/SivaSankarS365/InterIIT-11-DevRev
bash setup.sh
```

## Retrieval Strategy

Our approach integrates both Dense Passage Retrieval (DPR) and Sparse retrieval models with a sophisticated voting strategy:

1. **Hybrid Retrieval**:
   - Combines dense and sparse embeddings to leverage both semantic and lexical information.
   - Utilizes ColBERT embeddings for fine-grained similarity, improving retrieval accuracy.

2. **Voting Mechanism**:
   - Min-max scales individual retriever scores.
   - Applies weighted averaging to synthesize scores from multiple models.
   - Selectively uses cross-encoders when scores are close to refine results.

## Re-Ranking

The re-ranking system is trained on self-generated data to further enhance accuracy:

1. **Automatic Question Generation**:
   - Identifies noun chunks using POS tagging and NER.
   - Uses a T5 model to generate relevant questions based on these noun chunks.
   - Generates approximately 130 questions per paragraph to assist in retrieval.

2. **Cross-Encoder Fine-Tuning**:
   - Optionally re-ranks retrieved passages using a cross-encoder.
   - Fine-tunes the cross-encoder using SDAFT (Self Distill And FineTune) to adapt to specific themes while preserving pre-trained knowledge.

## Performance and Efficiency

Our method balances performance with efficiency, as demonstrated by the following features:

- **Top-1 Accuracy**: Improved by using a hybrid retrieval approach with voting.
- **Top-5 Accuracy**: Achieves perfect scores with our ensemble strategy.
- **F1 Score**: Enhanced by combining the best retrievers with effective QA readers.

### Latency Optimization

- **Inference Speed**: Utilizes ONNX for faster model inference and parallelizes processing across multiple threads.
- **Caching**: Uses joblib for caching to reduce load times and improve overall efficiency.

## Results

Our pipeline shows significant improvements in both accuracy and efficiency:

- **Retriever Performance**: Achieves top-1 accuracy of 0.854 with voting ensemble and appended questions.
- **Re-Ranker Performance**: Fine-tuned cross-encoder improves top-1 accuracy to 0.871.
- **QA Reader Performance**: TinyRoberta achieves an F1 score of 0.817.

## Conclusion

The **R2RA** pipeline integrates advanced retrieval, re-ranking, and answer extraction techniques to deliver a highly efficient and accurate DSQA system. Our novel approach ensures robust performance while maintaining computational efficiency, making it ideal for real-time applications.