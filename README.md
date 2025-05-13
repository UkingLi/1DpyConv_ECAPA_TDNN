
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



### Training

Then you can change the data path in the `trainECAPAModel.py`. Train ECAPA-TDNN model end-to-end by using:

```
python trainECAPAModel.py --save_path exps/exp1 
```

Every `test_step` epoches, system will be evaluated in Vox1_O set and print the EER. 

The result will be saved in `exps/exp1/score.txt`. The model will saved in `exps/exp1/model`

In my case, I trained 80 epoches in one 3090 GPU. Each epoch takes 37 mins, the total training time is about 48 hours.



### Acknowledge

We study many useful projects in our codeing process, which includes:

[clovaai/voxceleb_trainer](https://github.com/clovaai/voxceleb_trainer).

[lawlict/ECAPA-TDNN](https://github.com/lawlict/ECAPA-TDNN/blob/master/ecapa_tdnn.py).

[speechbrain/speechbrain](https://github.com/speechbrain/speechbrain/blob/96077e9a1afff89d3f5ff47cab4bca0202770e4f/speechbrain/lobes/models/ECAPA_TDNN.py)

[ranchlai/speaker-verification](https://github.com/ranchlai/speaker-verification)

Thanks for these authors to open source their code!


