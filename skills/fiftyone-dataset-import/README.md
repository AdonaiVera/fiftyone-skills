# Dataset Import

Import any dataset into FiftyOne with automatic format detection. Supports local files, Hugging Face Hub, cloud storage, multimodal grouped data, and MCAP robotics/AV sensor recordings.

## Install

```bash
curl -sL skil.sh | sh -s -- voxel51/fiftyone-skills
```

When prompted, select **fiftyone-dataset-import** from the menu.

## Requirements

- [FiftyOne](https://docs.voxel51.com/getting_started/install.html)
- [FiftyOne MCP Server](https://github.com/voxel51/fiftyone-mcp-server) (optional, recommended for App control)

## Usage

Start the MCP server and ask your AI assistant:

```
"Import the COCO dataset from /path/to/data"
"Load the keremberke/license-plate-object-detection dataset from Hugging Face"
"Import this folder of images, there are cameras and LiDAR files grouped by scene"
"Import these MCAP recordings from /path/to/rosbags"
```

The skill scans your data, auto-detects the format and media types, and loads the dataset into FiftyOne. It handles images, videos, point clouds, MCAP multimodal recordings (robotics/AV sensor logs), COCO, YOLO, VOC, KITTI, and more without you specifying the format.

## Example

```bash
# Download sample COCO data to ~/fiftyone/coco-2017/validation
fiftyone zoo datasets download coco-2017 --split validation
```

Then ask your assistant:

```
"Import the COCO 2017 validation dataset from ~/fiftyone/coco-2017/validation and name it coco-2017-validation"
```

After the skill runs, verify in Python:

```python
import fiftyone as fo
dataset = fo.load_dataset("coco-2017-validation")
print(dataset)
```

Or ask your assistant to open it in the App:

```
"Launch the FiftyOne App with the coco-2017-validation dataset"
```

## See also

- [Dataset Import docs](https://docs.voxel51.com/user_guide/dataset_creation/index.html)
- [Hugging Face Hub integration](https://docs.voxel51.com/integrations/huggingface.html)
- [FiftyOne Multimodal (MCAP) guide](https://docs.voxel51.com/user_guide/multimodal.html)

This skill's directory also ships reference files the skill reads on demand rather than every
invocation: `SPECIALIZED-3D-FORMATS.md` (PandaSet, nuScenes, Waymo, Argoverse, KITTI 3D, Lyft L5,
A2D2), `USE-CASE-EXAMPLES.md` (copy-paste starting points), and for MCAP recordings specifically,
`MCAP-TROUBLESHOOTING.md` (why a tile isn't rendering), `MCAP-AUTHORING.md` (authoring MCAP from
raw sensor data, converting ROS bags, merging/patching), and `MCAP-DATASET-AND-VALIDATION.md`
(capability flags and validating an import before calling it done).
