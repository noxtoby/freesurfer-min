## An example BIDS App (template repository)
Every BIDS App needs to follow a minimal set of command arguments common across
all of the Apps. This allows users and developers to easily use and integrate
BIDS Apps with their environment.

This is an minimalistic example BIDS App consisting of a Dockerfile and simple
entrypoint script (written in this case in Python) accepting the standard BIDS
Apps command line arguments. This repository can be used as a template for new BIDS Apps.

For more information about the specification of BIDS Apps see [here](https://docs.google.com/document/d/1E1Wi5ONvOVVnGhj21S1bmJJ4kyHFT7tkxnV3C23sjIE/edit#).

### Description
This is a placeholder for a shaort description explaining the user what your App is doing.

### Documentation
Provide a link to a documention of your pipeline.

### How to report errors
Provide instruction for users on how to get help and report errors.

### Acknowledgements
Describe how would you like users to acknoledge the use of your App in their papers (citation, a paragraph that should be copy pasted etc.)

### Usage
This App has the following comman line arguments:

		usage: run.py [-h]
		              [--participant_label PARTICIPANT_LABEL [PARTICIPANT_LABEL ...]]
		              bids_dir output_dir {participant,group}

		Example BIDS App entrypoint script.

		positional arguments:
		  bids_dir              The directory with the input dataset formatted
		                        according to the BIDS standard.
		  output_dir            The directory where the output files should be stored.
		                        If you are running group level analysis this folder
		                        should be prepopulated with the results of
		                        theparticipant level analysis.
		  {participant,group}   Level of the analysis that will be performed. Multiple
		                        participant level analyses can be run independently
		                        (in parallel).

		optional arguments:
		  -h, --help            show this help message and exit
		  --participant_label PARTICIPANT_LABEL [PARTICIPANT_LABEL ...]
		                        The label(s) of the participant(s) that should be
		                        analyzed. The label corresponds to
		                        sub-<participant_label> from the BIDS spec (so it does
		                        not include "sub-"). If this parameter is not provided
		                        all subjects should be analyzed. Multiple participants
		                        can be specified with a space separated list.

To run it in participant level mode (for one participant):

    docker run -i --rm \
		-v /Users/filo/data/ds005:/bids_dataset \
		-v /Users/filo/outputs:/outputs \
		bids/example \
		/bids_dataset /outputs participant --participant_label 01

After doing this for all subjects (potentially in parallel) the group level analysis
can be run:

    docker run -i --rm \
		-v /Users/filo/data/ds005:/bids_dataset \
		-v /Users/filo/outputs:/outputs \
		bids/example \
		/bids_dataset /outputs group

### Special considerations
Describe if your app has some special requirements. For example:

- Multiple map reduce steps (participant, group, participant2, group2 etc.)
- Unusual memory requirements
- etc.
