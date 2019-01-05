# TasNet: Time-domain Audio Separation Network
A PyTorch implementation of "TasNet: Time-domain Audio Separation Network for Real-time, single-channel speech separation", published in ICASSP2018, by Yi Luo and Nima Mesgarani.

## Install
- PyTorch 0.4.1+
- Python3 (Recommend Anaconda)
- `pip install -r requirements.txt`
- If you need to convert wjs0 to wav format and generate mixture files, `cd tools; make`

## Usage
See `egs/wsj0/run.sh` for example. Remember to modify related wsj0 data path and `stage`.
- Stage 0: Convert sphere format to wav format and generate mixture (optional)
- Stage 1: Generating json files including wav path and duration
- Stage 2: Training
- Stage 3: Evaluate separation performance
- Stage 4: Separate speech using TasNet

If you want to visualize your loss, you can use `visdom` to do that:
- Open a new terminal in your remote server (recommend tmux) and run `$ visdom`
- Open a new terminal and run `$ run.sh --visdom 1 --visdom_id "<any-string>"` or `$ train.py ... --visdom 1 --vidsdom_id "<any-string>"`
- Open your browser and type `<your-remote-server-ip>:8097`, egs, `127.0.0.1:8097`
- In visdom website, chose `<any-string>` in `Environment` to see your loss

## Experimental Results
| Method | Causal | SDRi | SI-SNRi | Config |
| :----: | :----: | :-----: | :--: | :----: |
| TasNet-BLSTM (Paper) | No | 11.1 | 10.8 | |
| TasNet-BLSTM (Mine) | No | 11.84 | 11.54 | L40 N500 hidden500 layer4 lr1e-3 epoch100 batch size10 |
| TasNet-BLSTM (Mine) | No | 11.77 | 11.46 | Above + L2 1e-4|
| TasNet-BLSTM (Mine) | No | 13.07 | 12.78 | Above + L2 1e-5|

## TODO
- [ ] Layer normlization described in paper
- [ ] LSTM skip connection
- [ ] Curriculum learning
