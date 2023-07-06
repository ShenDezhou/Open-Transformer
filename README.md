# Training A Transformer Model

```python
python main.py \
    optim.name={adafactor,adamwscale} \
    optim.lr_scheduler={legacy,cosine}
```

We recommend adding `model.compile=true` flag for pre-training, if you are able to install PyTorch 2.0.
