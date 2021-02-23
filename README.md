# GPT-NeoX

This repository records [EleutherAI](www.eleuther.ai)'s work-in-progress for training large scale GPU language models. Our current framework is based on NVIDIA's [Megatron Language Model](https://github.com/NVIDIA/Megatron-LM) and has been augmented with techniques from [DeepSpeed](https://www.deepspeed.ai) as well as some novel optimizations. 

If you are looking for our TPU codebase, see [GPT-Neo](https://github.com/EleutherAI/gpt-neo).

## Getting Started

TO DO

## Training

TO DO

## Datasets

TO

## EleutherAI cluster

### Using a cluster

If you already have a EleutherAI cluster setup for you, test to see if the cluster is working:
    
1. Copy data from cold storage to the shared mount: `cp -R /mnt/ssd-0/megatron-3d/data /mnt/ssd-cluster/data`
2. Example run `bash examples/ds_pretrain_gpt2_medium_pipe.sh`
    
### Cluster features

Setup:

* Use the "main node" as the entry point. This is the node with index 0
* All nodes have read/write access to a shared mount at `/mnt/ssd-cluster`. The default location for data for GPT-NEOX is set to `/mnt/ssd-cluster/data`
* All nodes have read access to a cold storage mount. This is where preprocessed data is kept `/mnt/ssd-0`
* A copy of the gpt-neox repo is cloned to `~/gpt-neox`

Tools (cd to `~/gpt-neox`):

* To kill a run: `bash tools/killall.sh`
* To copy a file to all nodes `bash tools/sync.sh $FILE`
* To copy a directory to all nodes `bash tools/syncdir.sh $DIR`
* To run a `git pull` command on all nodes `pdsh -w ^/job/hosts 'cd gpt-neox; git pull'`

Utils:
* `htop`: process monitor, CPU and memory utilisation
* `gpustat`: GPU utilisation
* `tmux`: use this so that when you disconnect you don't kill your run

### Setting up a cluster

Requires necessary permissions. To set-up a cluster for yourself:

1. `bash kubernetes/deploy_cluster.sh main 2` to deploy a 2 node cluster and clone the main branch of this repo to each node

To set-up a cluster for someone else (named `NAME`) without cluster permissions:

1. `bash kubernetes/deploy_cluster.sh main 2 NAME`
2. `bash kubernetes/public_cluster.sh NAME`

## Licensing

This repository hosts code that is part of EleutherAI's GPT-NeoX project. Copyright 2021 Stella Biderman, Sid Black, Josh Levy-Kramer, and Shivanshu Purohit.

    GPT-NeoX is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program. If not, see <https://www.gnu.org/licenses/>.

This repository is based off code written by NVIDIA that is licensed under the Apache License, Version 2.0. In accordance with the Apache License, all files that are modifications of code originally written by NIVIDIA maintain a NVIDIA copyright header. All files that do not contain such a header are original to EleutherAI. When the NVIDIA code has been modified from its original version, that fact is noted in the copyright header. All derivative works of this repository must preserve these headers under the terms of the Apache License.

For full terms, see the `LICENSE` file. If you have any questions, comments, or concerns about licensing please email us at contact@eleuther.ai.
