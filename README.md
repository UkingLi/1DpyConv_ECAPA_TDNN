
### Dependencies

Note: That is the setting based on my device, you can modify the torch and torchaudio version based on your device.

Start from building the environment
```
conda create -n ECAPA python=3.7.9 anaconda
conda activate ECAPA
pip install -r requirements.txt
```

Start from the existing environment
```
pip install -r requirements.txt
```

### Data preparation

Please follow the official code to perpare your VoxCeleb2 dataset from the 'Data preparation' part in [this repository](https://github.com/clovaai/voxceleb_trainer).

Dataset for training usage: 

1) VoxCeleb2 training set;

2) MUSAN dataset;

3) RIR dataset.

Dataset for evaluation: 

1) VoxCeleb1 test set for [Vox1_O](https://www.robots.ox.ac.uk/~vgg/data/voxceleb/meta/veri_test2.txt) 

2) VoxCeleb1 train set for [Vox1_E](https://www.robots.ox.ac.uk/~vgg/data/voxceleb/meta/list_test_all2.txt) and [Vox1_H](https://www.robots.ox.ac.uk/~vgg/data/voxceleb/meta/list_test_hard2.txt) (Optional)

### Training

Then you can change the data path in the `trainECAPAModel.py`. Train ECAPA-TDNN model end-to-end by using:

```
python trainECAPAModel.py --save_path exps/exp1 
```

Every `test_step` epoches, system will be evaluated in Vox1_O set and print the EER. 

The result will be saved in `exps/exp1/score.txt`. The model will saved in `exps/exp1/model`

In my case, I trained 80 epoches in one 3090 GPU. Each epoch takes 37 mins, the total training time is about 48 hours.

### Pretrained model

Our pretrained model performs `EER: 0.96` in Vox1_O set without AS-norm, you can check it by using: 

```
python trainECAPAModel.py --eval --initial_model exps/pretrain.model
```

With AS-norm, this system performs `EER: 0.86`. We will not update this code recently since no enough time for this work. I suggest you the following paper if you want to add AS-norm or other norm methods:

```
Matejka, Pavel, et al. "Analysis of Score Normalization in Multilingual Speaker Recognition." INTERSPEECH. 2017.
```

We also update the score.txt file in `exps/pretrain_score.txt`, it contains the training loss, training acc and EER in Vox1_O in each epoch for your reference.

***

### Acknowledge

We study many useful projects in our codeing process, which includes:

[clovaai/voxceleb_trainer](https://github.com/clovaai/voxceleb_trainer).

[lawlict/ECAPA-TDNN](https://github.com/lawlict/ECAPA-TDNN/blob/master/ecapa_tdnn.py).

[speechbrain/speechbrain](https://github.com/speechbrain/speechbrain/blob/96077e9a1afff89d3f5ff47cab4bca0202770e4f/speechbrain/lobes/models/ECAPA_TDNN.py)

[ranchlai/speaker-verification](https://github.com/ranchlai/speaker-verification)

Thanks for these authors to open source their code!


