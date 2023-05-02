# Life Event Dialog (LED)

Dataset for [LED: A Dataset for Life Event Extraction from Dialogs](http://arxiv.org/abs/2304.08327).
In this paper, we present Life Event Dialog, a dataset containing fine-grained life event annotations on conversational data from [DailyDialog dataset](http://yanran.li/dailydialog.html). 


## Structure

Each line is a jsonl object of a conversation with the following format:

- `DailyDialog_id`: The dialogue id to map to the original dialogue in DialyDialog dataset.
- `dialog_id`: A unique identifier for each dialogue in LifeEventDialog\_[train/valid/test].jsonl
- `events`: A list of `Events` in each turn.
- `coreferences`: A list of clusters, each cluster is a list of tokens index. Note that the 1st cluster must be the cluster of speaker 1 (S1) and the 2nd must be of speaker 2 (S2). The cluster of S1/S2 might be an empty cluster if no events happen to S1/S2.


Each `Event` consists of the following schema:

```
"event_type": {
    'explicit': Bool, # 1: explicit, 0: implicit
    'Verb': {
        'tokens': Str,
        'tokens_id': Str, # Format: f'{StartID}-{EndID}'
    },
    'Class': Str,
    'Frame': Str,
}
"participant": {
    'subject': EntityDict,
    'object': EntityDict,
},
"event_status": { 
    'polarity': Bool, # 1: positive, 0: negative
    'modality': Bool, # 1: actual, 0: hypothetical
    'time': Str or Dict, # ['BEFORE', 'NOW', 'AFTER', 'CONTINUOUSLY', or an EntityDict refers to time in the dialogue
```

where 
```
EntityDict = {
    "entity_id": Int, # which is also the index of cluster in the "coreferences" field
    "tokens": Str,
    "tokens_id": Str, # Foramt: f'{StartID}' or f'{StartID}-{EndID}', e.g. '0' or '0-1'
}
```

## License
This dataset is licensed under the [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-nc-sa/4.0/) (CC BY-NC-SA 4.0.). 

This means you are free to use and share the dataset for non-commercial purposes, as long as you give appropriate credit to the original creators and share any adaptations of the dataset under the same license.


## Citation
If you use this dataset in your research, please cite our paper:
```
@inproceedings{chen-etal-2023-led,
    title = "{LED}: A Dataset for Life Event Extraction from Dialogs",
    author = "Chen, Yi-Pei  and
      Yen, An-Zi  and
      Huang, Hen-Hsen  and
      Nakayama, Hideki  and
      Chen, Hsin-Hsi",
    booktitle = "Findings of the Association for Computational Linguistics: EACL 2023",
    month = may,
    year = "2023",
    address = "Dubrovnik, Croatia",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2023.findings-eacl.29",
    pages = "384--398",
}
```
