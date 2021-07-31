# masterzero-hw-hpo-nni
Trying to use nni hyper parameter search tool.
## Dataset 
- MNIST
## Search Space
```json
{
    "batch_size": {"_type":"choice", "_value": [16, 32, 64, 128]},
    "hidden_size":{"_type":"choice","_value":[128, 256, 512, 1024]},
    "lr":{"_type":"choice","_value":[0.0001, 0.001, 0.01, 0.1]},
    "momentum":{"_type":"uniform","_value":[0, 1]}
}
```
## NNI Config
- If you use only one gpu in GUI system, trainingService.use_active_gpu must be set true.
```yml
# This is the minimal config file for an NNI experiment.
# Use "nnictl create --config config.yml" to launch this experiment.
# Afterwards, you can check "config_detailed.yml" for more explanation.

searchSpaceFile: search_space.json
trialCommand: python mnist.py  # NOTE: change "python3" to "python" if you are using Windows
trialGpuNumber: 1
trialConcurrency: 2
tuner:
  name: TPE
  classArgs:
    optimize_mode: maximize
trainingService:
  platform: local
  use_active_gpu: True
```

## Run `run.bat` in windows
```bash
nnictl create --config config.yml
```

## Stop
```bash
nnictl stop
```

## Reference
- [nni/examples/trials/mnist-pytorch/](https://github.com/microsoft/nni/tree/84507248ccec1fa329da91f930bf8704449c9707/examples/trials/mnist-pytorch)
- [Write a Trial Run on NNI](https://nni.readthedocs.io/en/stable/TrialExample/Trials.html#more-examples)
- [MnistExamples](https://nni.readthedocs.io/en/stable/TrialExample/MnistExamples.html)
- [TPE, Random Search, Anneal Tuners on NNI](https://nni.readthedocs.io/en/stable/Tuner/HyperoptTuner.html)