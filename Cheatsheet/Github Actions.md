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
This is normally used for CI/CD build
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