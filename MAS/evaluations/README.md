<h1>Training RESISC45 Models</h1>

`cd model_training`

set `--gpu x` where x is the gpu number (0 for a single gpu machine).

<h3>Resnet101 training</h3>

`python3 trainer.py --arch resnet101 --path-to-data ../../resisc45 --num-classes 45 --save_name resisc_45_resnet101.pth.tar --batch-size 200 --epochs 100
Acc@1 96.889 Acc@5 99.651`

<h3>Unmodified VIT16 training</h3>

`python3 trainer.py --arch vit_b_16 --path-to-data ../../resisc45 --num-classes 45 --save_name resisc_45_vit_b_16.pth.tar --batch-size 200 --epochs 100
Acc@1 89.069 Acc@5 98.476`

<h3>VIT16 training for the VIT attribution methods</h3>

`python3 trainer.py --arch vit_b_16_normal --path-to-data ../../resisc45 --num-classes 45 --save_name resisc_45_vit_b_16_normal.pth.tar --batch-size 200 --epochs 100
Acc@1 94 Acc@5 99`

<h1>EVALUATION ON ALL MODELS</h1>

`cd MAS/evaluations`

All results save to a sub folder of MAS called "test_results". 
Results for different models have their own folder: "R101" or "VIT16".

<h3>Testing sensitivity (Table 1)</h3>

```
python3 ImageNetSensitivityTest.py --model R101 --image_count 1000 --noise_type constant --dataset_path ../../../ImageNet --dataset_name ImageNet
python3 ImageNetSensitivityTest.py --model VIT16 --image_count 1000 --noise_type constant --dataset_path ../../../ImageNet --dataset_name ImageNet
python3 ImageNetSensitivityTest.py --model R101 --image_count 1000 --noise_type noised --dataset_path ../../../ImageNet --dataset_name ImageNet
python3 ImageNetSensitivityTest.py --model VIT16 --image_count 1000 --noise_type noised --dataset_path ../../../ImageNet --dataset_name ImageNet

python3 resisc45SensitivityTest.py --model R101 --image_count 1000 --noise_type constant --dataset_path ../../../resisc45 --dataset_name resisc45
python3 resisc45SensitivityTest.py --model VIT16 --image_count 1000 --noise_type constant --dataset_path ../../../resisc45 --dataset_name resisc45
python3 resisc45SensitivityTest.py --model R101 --image_count 1000 --noise_type noised --dataset_path ../../../resisc45 --dataset_name resisc45
python3 resisc45SensitivityTest.py --model VIT16 --image_count 1000 --noise_type noised --dataset_path ../../../resisc45 --dataset_name resisc45
```

Use `MAS/sensitivity_test_grapher.ipynb` to visualize the curves and measure the sensitivity, two examples are provided.


<h3>Testing consistency (Table 2 and Table 4)</h3>

```
python3 ImageNetConsistencyTest.py --model R101 --image_count 5000 --dataset_path ../../../ImageNet --dataset_name ImageNet
python3 ImageNetConsistencyTest.py --model VIT16 --image_count 5000 --dataset_path ../../../ImageNet --dataset_name ImageNet

python3 resisc45ConsistencyTest.py --model R101 --image_count 5000 --dataset_path ../../../resisc45 --dataset_name resisc45
python3 resisc45ConsistencyTest.py --model VIT16 --image_count 5000 --dataset_path ../../../resisc45 --dataset_name resisc45
```

<h3>Test baseline invariance (Table 3)</h3>

```
python3 ImageNetBaselineTest.py --model R101 --image_count 5000 --dataset_path ../../../ImageNet --dataset_name ImageNet
python3 ImageNetBaselineTest.py --model VIT16 --image_count 5000 --dataset_path ../../../ImageNet --dataset_name ImageNet

python3 resisc45BaselineTest.py --model R101 --image_count 5000 --dataset_path ../../../resisc45 --dataset_name resisc45
python3 resisc45BaselineTest.py --model VIT16 --image_count 5000 --dataset_path ../../../resisc45 --dataset_name resisc45
```

<h3>Qualitative ordering results (Figure 5 and Figures 16 - 25)</h3>

`python3 compareOrderings.py --image_count 100 --imagenet ../../../ImageNet`