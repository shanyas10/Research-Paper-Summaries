Following are the contributions made by the authors in the paper:
	• MacroBase, an analytics engine and architecture for analyzing fast data streams that is the first to combine streaming outlier detection and streaming data explanation.
	• The Adaptable Damped Reservoir, the first exponentially damped reservoir sample to operate over arbitrary windows, which MacroBase leverages in online classifier training.
	• An optimization for improving the efficiency of combined detection and explanation by exploiting cardinality imbalance between classes in streams.
	• The Amortized Maintenance Counter, a new heavy-hitters sketch that allows fast updates by amortizing sketch pruning across multiple observations of the same item.

Core Concepts: 
To prioritize attention, MacroBase executes streaming analytics operators that help filter and aggregate the stream. To do so, it combines two classes of operators:
	• Classification: Classification operators examine individual data points and label them according to user-specified classes(e.g. normal and outliers)
	• Explanation: Explanation operators group and aggregate multiple data points.(e.g. describe commonalities as well as differences.

Pipeline:
	• Ingestion
	• Feature Transformation: By default, MDP (Macrobase Default Pipeline) uses Median Absolute Deviation (MAD) for univariate data and MCD otherwise.
	• Classification: By default, Percentile Classifier is used. It calculates the 99th percentile as the threshold and classifies everything above it as an outlier.
	• Explanation: MacroBase’s default pipeline returns explanations in the form of attribute-value combinations (e.g., device ID 5052) that are common among outlier points but uncommon among inlier points.
	• Presentation: MacroBase’s default presentation mode is a static report rendered via a REST API or GUI.
	• Extensibility: MacroBase’s pipeline architecture lends itself to three major means of extensibility. First, users can add new domain specific feature transformations to the start of a pipeline without modifying the rest of the pipeline. Second, users can input rules and/or labels to MacroBase to perform supervised classification. Third, users can write their own feature transformation, classification, and explanation operators, as well as new pipelines.

	
MDP Classification: 
	• MacroBase’s classification operators label input data points, and, by default, identify data points that exhibit deviant behavior. 

	• Z- Score is not robust to outliers. A single outlier can skew the mean and standard deviation by a high amount.
	• So Macrobase's MDP Pipeline leverages robust statistical estimation
	• The MAD measures the median of the absolute distance from each point in the sample to the sample median. Since the median itself is resistant to outliers, each outlying data point has limited impact on the MAD score of all other points in the sample.
	• For multivariate data, the Minimum Covariance Determinant(MCD) provides similar robust estimates for location and spread

MDP Streaming Execution:
	• Adaptable Damped Reservoir: ADR is a novel adaptation of reservoir sampling over streams
	• The key difference from traditional reservoir sampling is that the ADR operates over arbitrary window sizes, allowing greater flexibility than existing damped samplers.
	• In contrast with existing approaches that decay on a per-tuple basis, the ADR separates the insertion process from the decay decision, allowing both time-based and tuple-based decay policies.
	• MacroBase currently supports two decay policies: time-based decay, which decays the reservoir at a pre-specified rate measured according to real time, and batch-based decay, which decays the reservoir at a pre-specified rate measured by arbitrarily-sized batches of data points

Evaluation:
	• MacroBase is accurate: on controlled, synthetic data, under changes in stream behavior and over real-world workloads from the literature and in production
	• MacroBase can process up to 2M points per second per query on a range of real-world datasets.
	• MacroBase’s cardinality-aware explanation strategy produces meaningful speedups.
	• MacroBase’s use of AMC is up to 500x faster than existing sketches on production data.
	• MacroBase’s architecture is extensible, which we illustrate via three case studies.
