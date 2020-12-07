# Good-Enough Compositional Data Augmentation – Jacob Andreas

## Introduction:
- With traditional models, it is straightforward to precisely characterize how that grammar will extrapolate beyond the examples in a given training set to out-of-distribution data.
- But with neural networks, it is possible but not very transparent and is beyond scale.
- The paper introduces a simple data augmentation protocol that provides a good compositional inductive bias for sequential models.
- Synthetic examples are created by taking real sequences and replacing the fragments in sequences which appear in similar environments. This operation is referred to as GECA (Good Enough Compositional Augmentation).
- The underlying idea is that if two fragments of training examples occur in some environment, then any environment where the first fragment appears is also a valid environment for the second fragment.    	

## Approach
- Authors aim at a notion of compositionality that is simpler and more general: a bias toward identifying recurring fragments seen at training time and re-using them in environments distinct from those in which they were first observed.
- Discover substitutable fragments (i.e. pairs of fragments that co-occur with a common fragment) and use them to generate new sequences by swapping fragments.
- The current work uses very simple criteria to decide if fragments are substitutable - fragments should occur in at least one lexical environment that is exactly the same. A lexical environment is the k-word window around each span of the fragment.
- Though the idea can be motivated by work in generative syntax and distributional semantics, it would not hold like a physical law when applied to the real data.
- The authors view this tradeoff as a balance between the shortage of training data vs relative frequency of mistake in the proposed data augmentation approach.

## Results
- The approach is evaluated on the SCAN dataset when the model is trained on the short sequence of English commands. Though the dataset augmentation helps the baseline models, it is not surprising given the nature of the SCAN dataset.
- The results suggest that GECA is most successful when it can increase similarity of word co-occurrence statistics in the training and test sets, and when the input dataset exhibits a high degree of recursion.

## Takeaways:
- Innovative and novel method for data augmentation.
- Focuses on improving syntactic robustness of the model (dataset, to be precise)
- No changes in model or architecture
- Rule based

## Cross References:
- https://arxiv.org/abs/1606.03622 : Data Recombination for Neural Semantic Parsing
- https://arxiv.org/abs/1709.01643 : Learning to Compose Domain-Specific Transformations for Data Augmentation
- https://arxiv.org/abs/1901.11196 : EDA: Easy Data Augmentation Techniques for Boosting Performance on Text Classification Tasks