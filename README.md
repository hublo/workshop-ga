# Workshop Github Actions

## Overview of an action 



### Triggers

Manual trigger 

```bash
on:
  workflow_dispatch:

```

Basic trigger on PR
```bash
on:
  pull_request:
    # Sequence of patterns matched against refs/heads
    branches:    
      - main
```


Sending input to Actions 
```bash
on:
  workflow_dispatch:
    inputs:
      logLevel:
        description: 'Log level'
        required: true
        default: 'warning' 
        type: choice
        options:
        - info
        - warning
        - debug 
```

See triggers [documentations](https://docs.github.com/en/actions/using-workflows/triggering-a-workflow) for more 

:warning: :warning: :warning: :warning:
**NOW DO SOME STUFF**
:warning: :warning: :warning: :warning:

- Please clone this repository and then create your own branch `ws-myname` 
- Then modify the simple `my-first-action.yml` to be able to run it on every push on your specific branch only. 
- Add an input to be able to pass the version that you want  to trigger (a text input named version). 

:warning: :warning: :warning: :warning:

### Actions

Basic job definition 
```bash
jobs:
  my_first_job:
    name: My first job
  my_second_job:
    name: My second job
```


Job Dependencies 
```
jobs:
  job1:
  job2:
    needs: job1
  job3:
    needs: [job1, job2]
```

And now where the magic happens 

```
- uses: actions/setup-node@v2
  with:
    node-version: '14'
```

:warning: :warning: :warning: :warning:
**NOW DO SOME STUFF**
:warning: :warning: :warning: :warning:


- By reusing the workflow `my-first-action.yml` modify it to add two step, one for running a build and one for a run. 
- Check on a new github action that you can use to modify json file (JQ) and use it to update the package version version with the one you give as input. 
- Create two jobs, one for build, one for run with a dependency

If you have the time : 
- edit the `my-scheduled-action.yml` workflow to add a scheduled run on the other workflow 


#### Help
To be able to do this you will need to check this specific things : 
- Workflow triggering : 
```bash
    steps:
      - uses: ./.github/workflows/my-action
        with:
          username: ${{ inputs.username }}
```

Scheduled trigger : 
```bash
on:
schedule:
# * is a special character in YAML so you have to quote this string
- cron:  '30 5,17 * * *'
```

**NOTE:** Scheduled workflow are only trigger for main, you will need two things to make it works on your branch: 
- Trigger your workflow on  the main branch
- specificly checkout your branch at the beginning of the pipeline if you want to execute it. 

:warning: :warning: :warning: :warning:



