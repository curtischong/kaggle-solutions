Binary Cross Entropy loss
- typically used for binary classification problems
learn more about cross entropy loss at [[cross-entropy loss]]

related: [[BCEWithLogitsLoss]] (which is basically BCELoss but with a sigmoid applied to the logits first). You should use it instead in pytorch (cause it has stable gradients)