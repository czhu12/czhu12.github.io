---
layout: post
title: Explorations in Knowledge Distillation
---

Knowledge distillation is a common way to train compressed models by transferring the knowledge learned from a large model into a smaller model.

# Background / Motivations
A random example for why you may want to compress a model: in fields where privacy is important, it may be the case that we cannot stream patient data to the cloud where all our fancy GPU's live. This creates the need to train best model that can be downloaded and deployed to devices that run in a hospital?

The training process for knowledge distillation is basically as follows:

### Train a teacher network on labels
TODO

### Train a student network on logits from teacher + labels
TODO

# How well does it work?

I wanted to run some experiments on how well knowledge distillation acutally worked in practice for common image and language tasks. The original paper on distillation produced the following results in MNIST:

2 layer feed forward network / 1200 hidden dimension (large model)          | 67 test errors
2 layer feed forward network / 800 hidden dimension  (small model)          | 146 test errors
2 layer feed forward network / 800 hidden dimension  (large -> small model) | 74 test errors

But I wanted to answer some additional questions like:
1. How much smaller can the student model be than the teacher model?
2. Is knowledge distillation more effective on different tasks? (For instance, image classification vs language modeling)
3. How do different hyperparameters perform in different settings?

Since MNIST is known to be a fairly weak baseline, and I wanted to explore datasets in the medical space anyways, I thought maybe this would be a good chance to play around with a couple datasets.
- [APTOS 2019 Blindness Detection Dataset](https://www.kaggle.com/c/aptos2019-blindness-detection/data) (Image classification)

We'll also be using PyTorch and PyTorch lightning to build and train the models.

PyTorch Lightning is an amazing library that will let us modularize our code so we can separate the bits that are common in basically all image classification tasks and the bits that are specific to image distillation tasks.

Lets start by building a generic `ImageClassificationModel` base class

```
class ImageClassificationModel(pl.LightningModule):

    def __init__(self, encoder, classes=10):
        super().__init__()
        out_features = list(encoder.children())[-1].out_features
        self.net = nn.Sequential(encoder, nn.Linear(out_features, classes))

    def forward(self, x):
        # in lightning, forward defines the prediction/inference actions
        predictions = self.net(x)
        return predictions

    def training_step(self, batch, batch_idx):
        # training_step defined the train loop. It is independent of forward
        x, y = batch
        prediction = self.net(x)
        loss = F.cross_entropy(prediction, y)
        self.log('train_loss', loss)
        return loss

    def validation_step(self, batch, batch_idx):
        x, y = batch
        output = self.net(x)
        loss = F.cross_entropy(output, y)
        preds = torch.argmax(output, dim=1)
        acc = accuracy(preds, y)

        # Calling self.log will surface up scalars for you in TensorBoard
        self.log('val_loss', loss, prog_bar=True)
        self.log('val_acc', acc, prog_bar=True)
        return loss

    def configure_optimizers(self):
        optimizer = optim.Adam(self.net.parameters(), lr=0.02)
        return optimizer
```

This basically sets up our dataset the same way any image classification task would 