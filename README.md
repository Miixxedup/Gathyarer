# GathYarer, a tool 'to gather' yara rules.
Gathyarer is a (very basic) tool to aid myself (and hopefully other) DFIR analists in the usage of Yara rules. It aims to collect all the .yar(a) rules from a directory, does some processing and generates a ready to go Yara ruleset.
The idea is simple: 
1. Clone multiple GitHubs / Find multiple Yara lists / Made multiple Yara rules spread everywhere on the system / a combination of all before
2. Run `gathyarer.py` to collect all the rules recursively from a starting directory
3. Use Yara to analyse your directory/disk/system/memory using only a single rules file generated from all other files.

## What does it (not) do?
For now, gathyarer does the following:

1. Builds the Gathyarer file structure from where Gathyarer is launched.
2. Collects all the `.yar` & `.yara` files it finds from a starting point.
3. Opens the original Yara rules files, does some processing(see below) and writes the results to a new file.
4. Adds the new entry to the `YARA-agg.yara` file and continues.

It (currently) does not:

1. Compare rules for similarity.
2. Fixes rules itself, it assumes all rules work.


## What does it process during copying ?

Currently it checks (and fixes) a couple of things:
- It creates a new name for each rule using a regex, to ensure unique names
- It checks for include only rule files and skips them.


## What does it do in the post-processing ? 
Currently nothing but I can image it might be useful to include it already


## Usage
Basic Usage

```bash
python3 gathyarer.py ../{a/directory/starting/point}

# If a folder was previously generated, overwrite it by answering with Y
[???] PREVIOUSLY GENERATED FOLDER result-agg FOUND, DELETE IT AND ITS CONTENTS?(Y/N): Y
```

```bash
python3 gathyarer.py -h
usage: gathyarer.py [-h] [-ts] [-d] p

positional arguments:
  p           Supply a file path to start from

optional arguments:
  -h, --help  show this help message and exit
  -ts         Appends timestamps during foldergeneration for foldernames and resulting .yara file
  -d          Returns debug information
```
