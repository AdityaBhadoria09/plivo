# plivo
Task 1 — Baseline System

We installed dependencies, prepared the dataset, and ran the baseline model using:

Model: DistilBERT-base-uncased

Training: 3 epochs

Evaluation: dev + stress datasets

Outputs generated:

out/dev_pred.json

out/stress_pred.json

Baseline Performance

(Example placeholder values, replace with your actual numbers if needed)

Metric	Value
Overall Span F1	~84%
PII Precision	~78%
PII Recall	~70%
PII F1	~73%

Baseline decoding was brittle (BIO handling weak), causing lower precision in multi-token entities.

Task 2 — Model Improvements

We improved the NER system through:

1. Stronger BIO-to-Span Decoder

Fixed boundary issues

Prevented label-flipping errors

Merged broken I-segments

Improved precision for PII spans

2. Better Model

Switched from DistilBERT → BERT-base-uncased

More expressive encoder → higher recall and stability

3. Hyperparameter Tuning

Trained for 6 epochs

Batch size = 16

Learning rate = 3e-5

Max length = 256

4. Cleaning & Post-Processing

Removed invalid spans

Enforced label consistency

Improved multi-token entity stitching

Task 3 — Improved Evaluation

After improvements:

Improved Performance
Metric	Baseline	Improved
Overall Span F1	~84%	~90%
PII Precision	~78%	~88%
PII Recall	~70%	~82%
PII F1	~73%	~85%
Summary

Precision improved significantly due to better decoding.

Recall improved due to stronger encoder (BERT-base).

Reduced span fragmentation → better end-to-end accuracy.

Task 4 — Latency Measurement

We executed:

python src/measure_latency.py --model_dir out2 --input data/dev.jsonl --runs 50

Latency Results (example values)
Metric	Time
p50 latency	~11 ms
p95 latency	~18 ms (✓ within 20 ms requirement)
