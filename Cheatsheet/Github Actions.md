# Trigger
## Manual running a workflow
```yml
name: Example

on:
 # ...triggers
 workflow_dispatch:

# ...rest
```
## Trigger by another workflow
```yml
name: Trigger by another workflow

on:
	workflow_run:
		workflows: [Workflow A, Workflow B]
		types:
			- completed
```
# Get data from another job
```yaml
jobs:
  job1:
    runs-on: ubuntu-latest
    outputs:
      output1: ${{ steps.step1.outputs.test }}
      output2: ${{ steps.step2.outputs.test }}
    steps:
      - id: step1
        run: echo "test=hello" >> $GITHUB_OUTPUT
      - id: step2
        run: echo "test=world" >> $GITHUB_OUTPUT
  job2:
    needs: job1
    runs-on: ubuntu-latest
    steps:
      - run: echo ${{needs.job1.outputs.output1}} ${{needs.job1.outputs.output2}}
```
# Check step fails
```yml
jobs:
 job1:
  - name: 'Step that fails'
    id: 'step_fail'
    # ...run something that might fails
    
    - name: 'Run if step fails',
    if: ${{ failure() && steps.step_fail.conclusion == 'failure' }}
    # ...run something when the step fails
```
# Artifact
This is normally used to separate build step and deployment step
```yml
jobs:
 build:
  steps:
   # ...run steps that you need to create a build
   
   - name: Archive build artifacts
     uses: actions/upload-artifact@v3
     with:
      name: ${{github.ref_name}}-artifact
      path: dist
      retention-days: 1
      
 deploy:
  needs: build
  permission:
   id-token: write
   contents: read
  steps:
   - name: Download ${{github.ref_name}} artifact
     uses: actions/download-artifact@v3
     with:
      name: ${{github.ref_name}}-artifact
      path: dist		
```
# Composite Action (Reusable Action)
Path: `.github/actions/hello-world-composite-action/action.yml`
```yaml
name: 'Hello World'
description: 'Greet someone'
inputs:
  who-to-greet:  # id of input
    description: 'Who to greet'
    required: true
    default: 'World'
outputs:
  random-number:
    description: "Random number"
    value: ${{ steps.random-number-generator.outputs.random-number }}
runs:
  using: "composite"
  steps:
    - name: Set Greeting
      run: echo "Hello $INPUT_WHO_TO_GREET."
      shell: bash
      env:
        INPUT_WHO_TO_GREET: ${{ inputs.who-to-greet }}

    - name: Random Number Generator
      id: random-number-generator
      run: echo "random-number=$(echo $RANDOM)" >> $GITHUB_OUTPUT
      shell: bash

    - name: Set GitHub Path
      run: echo "$GITHUB_ACTION_PATH" >> $GITHUB_PATH
      shell: bash
      env:
        GITHUB_ACTION_PATH: ${{ github.action_path }}

    - name: Run goodbye.sh
      run: goodbye.sh
      shell: bash

```

Using the composite action
```yaml
on: [push]

jobs:
  hello_world_job:
    runs-on: ubuntu-latest
    name: A job to say hello
    steps:
      - uses: actions/checkout@v4
      - id: foo
        uses: ./.github/actions/hello-world-composite-action
        with:
          who-to-greet: 'Mona the Octocat'
      - run: echo random-number "$RANDOM_NUMBER"
        shell: bash
        env:
          RANDOM_NUMBER: ${{ steps.foo.outputs.random-number }}
```
# Performance Optimizations
- [cache](https://github.com/actions/cache)
- [matrix strategies](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/running-variations-of-jobs-in-a-workflow)
# Github Actions Package
- [Create or Update Comment](https://github.com/marketplace/actions/create-or-update-comment#create-or-update-comment)
- [Release Drafter](https://github.com/marketplace/actions/release-drafter)