# U2Seg Enhanced Demo - COMP7404 Group 11

Enhanced demonstration tools for **U2Seg: Unsupervised Universal Image Segmentation** with ground truth comparison capabilities and comprehensive visualization features.

## Team Introduction

This repository has been enhanced by **COMP7404 Group 11** from the University of Hong Kong. We've added comprehensive demo capabilities, ground truth comparison tools, and improved visualization features to make U2Seg more accessible for research and educational purposes.

**Team Members:**
- **Group 11** - COMP7404 Advanced Machine Learning
- **Institution:** University of Hong Kong
- **Course:** COMP7404 - Advanced Topics in Machine Learning

## Our Contributions

- ✨ **Enhanced demo script** with ground truth comparison (`u2seg_demo_with_gt.py`)
- 📊 **Side-by-side visualization** of predictions vs. ground truth
- 🎥 **Video processing capabilities** with real-time preview
- 📖 **Improved documentation** and usage examples
- 🔧 **Extended evaluation tools** for better analysis

## Installation

### Quick Installation
```bash
# Clone the repository
git clone https://github.com/your-repo/U2Seg.git
cd U2Seg

# Install the package
pip install .
```

### Requirements
- Python 3.8+
- PyTorch 1.8+
- OpenCV
- NumPy
- Matplotlib
- pycocotools

## Quick Start

### 1. Download Pre-trained Model
Download the model checkpoint and place it in the `ckpts/` folder:
```bash
mkdir -p ckpts
# Download from: https://drive.google.com/drive/folders/186GBbIhEW7W0eidGOGRTmTyM_HedSOQh
# Place as: ckpts/cocotrain_800_0089999.pth
```

### 2. Basic Demo (No Ground Truth)
```bash
# Test on demo images
python demo/u2seg_demo_with_gt.py \
    --config-file configs/COCO-PanopticSegmentation/u2seg_eval_800.yaml \
    --input "demo/images/*.jpg" \
    --output results/demo \
    --max-images 5
```

### 3. Enhanced Demo with Ground Truth Comparison

#### Setup COCO Data (One-time)
```bash
# Download COCO validation images (~1GB)
wget http://images.cocodataset.org/zips/val2017.zip
unzip val2017.zip

# Download COCO annotations (~25MB)
mkdir -p coco/annotations
wget http://images.cocodataset.org/annotations/annotations_trainval2017.zip
unzip annotations_trainval2017.zip -d coco/
```

#### Run Ground Truth Comparison
```bash
python demo/u2seg_demo_with_gt.py \
    --config-file configs/COCO-PanopticSegmentation/u2seg_eval_800.yaml \
    --input "val2017/val2017/*.jpg" \
    --output results_with_gt \
    --show-ground-truth \
    --ground-truth-file ./coco/annotations/instances_val2017.json \
    --max-images 10
```

## Usage Examples

### Process Your Own Images
```bash
python demo/u2seg_demo_with_gt.py \
    --input "path/to/your/images/*.jpg" \
    --output results/custom \
    --max-images 20
```

### Process More Images
```bash
# Process 50 images instead of default 5
python demo/u2seg_demo_with_gt.py \
    --input "val2017/val2017/*.jpg" \
    --show-ground-truth \
    --max-images 50 \
    --output results/batch_50
```

### Video Processing
```bash
python demo/u2seg_demo_with_gt.py \
    --mode videos \
    --video-dir ./videos \
    --output results/videos \
    --show-fps \
    --preview
```

## Command Line Options

| Parameter | Description | Default |
|-----------|-------------|---------|
| `--input` | Input images (glob pattern or specific files) | `./demo/images/*.jpg` |
| `--output` | Output directory | `./results_with_gt` |
| `--show-ground-truth` | Enable GT comparison (COCO images only) | `False` |
| `--max-images` | Maximum number of images to process | `5` |
| `--confidence-threshold` | Minimum confidence for predictions | `0.5` |
| `--mode` | `images`, `videos`, or `both` | `images` |
| `--show-fps` | Show FPS on video frames | `False` |
| `--preview` | Real-time video preview | `False` |

## Output Files

For each processed image, the enhanced demo generates:

1. **`comparison_*.jpg`** - Side-by-side view:
   - Original image
   - U2Seg predictions  
   - Ground truth (if available)

2. **`pred_*.jpg`** - Predictions only

3. **`gt_*.jpg`** - Ground truth only (if available)

## Examples

### Basic Usage
```bash
# Quick test with demo images
python demo/u2seg_demo_with_gt.py
```

### Specific Images with Ground Truth
```bash
python demo/u2seg_demo_with_gt.py \
    --input val2017/val2017/000000006040.jpg val2017/val2017/000000397133.jpg \
    --show-ground-truth \
    --output results/specific
```

### Batch Processing
```bash
# Process 100 COCO validation images
python demo/u2seg_demo_with_gt.py \
    --input "val2017/val2017/*.jpg" \
    --show-ground-truth \
    --max-images 100 \
    --output results/coco_100
```

## Troubleshooting

### Common Issues

**"The input path(s) was not found"**
- Check your image paths: `ls val2017/val2017/*.jpg | head -5`
- Use quotes around glob patterns: `"val2017/val2017/*.jpg"`

**"Ground truth file not found"**
- Download COCO annotations as shown in setup
- Check file exists: `ls ./coco/annotations/instances_val2017.json`

**Only processing 5 images**
- Add `--max-images N` to process more images
- Default limit prevents overwhelming output

## Windows Users

Use PowerShell and backslashes or quoted forward slashes:
```powershell
python demo/u2seg_demo_with_gt.py --input "val2017\val2017\*.jpg" --max-images 10
```

## Original Paper

> **Unsupervised Universal Image Segmentation**  
> Dantong Niu, Xudong Wang, Xinyang Han, Long Lian, Roei Herzig, Trevor Darrell  
> CVPR 2024  
> [Paper](https://arxiv.org/abs/2312.17243) | [Project Page](https://u2seg.github.io/)

## License

This enhanced version maintains the original U2Seg license terms. See LICENSE file for details.

## Support

For questions about our enhanced demo tools:
- Open an issue in this repository
- The enhanced features are designed to be self-explanatory with clear error messages

For questions about the original U2Seg method, refer to the original authors.
