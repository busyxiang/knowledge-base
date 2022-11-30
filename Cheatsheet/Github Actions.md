# Manual running a workflow
```yml
name: Example

on:
	# ...triggers
	workflow_dispatch:

# ...rest
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
## Check step fails
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