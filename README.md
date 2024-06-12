This is a built pipeline with github actions

We need to know how to create a webstatic with S3
https://medium.com/@nneyenu/automation-how-to-deploy-your-static-website-to-s3-using-github-actions-642267301359

1) Create a user and grant policies
   On the AWS console go to the IAM service and Choose Users. Then create a User
   ![image](https://github.com/resgem585/deploy-github-actions/assets/105258020/37761a29-1f90-4b75-ad79-63e8842bd375)

   Type the name of the user – Grant Programmatic access after creation
   ![image](https://github.com/resgem585/deploy-github-actions/assets/105258020/a211c193-d3e3-487f-bbac-b83b04fecd5c)

   Attach policies directly and select AmazonS3FullAccess
   ![image](https://github.com/resgem585/deploy-github-actions/assets/105258020/14b80bc4-0f39-4857-b240-6a3a11d2c9a8)
   ![image](https://github.com/resgem585/deploy-github-actions/assets/105258020/e7200b18-5c02-42ac-a267-6d5b5be52a58)

   Go next and create User

   After create user add Key with outside resources of aws.

   ![image](https://github.com/resgem585/deploy-github-actions/assets/105258020/9682140b-0018-4301-8933-bfb2220acb62)

2) Go to the repository and click on settings

   ![image](https://github.com/resgem585/deploy-github-actions/assets/105258020/630f3908-6f21-48f4-bdae-740c406ce891)

   On the left hand choose Secrets then Actions
   ![image](https://github.com/resgem585/deploy-github-actions/assets/105258020/b4caa0b7-aba5-4e93-8187-044b3dd98096)

   Click on New repository secret and add your ACCESS KEY. Repeat the action for SECRET KEY.

   ![image](https://github.com/resgem585/deploy-github-actions/assets/105258020/5cf31490-157c-4217-b9e8-b71e0ab9c06a)

   It shoud looks after creation

   ![image](https://github.com/resgem585/deploy-github-actions/assets/105258020/670e30ce-54b7-4a3d-b654-9d6f8a5c6367)


3) Create a workflow

   Navigate to your repository containing the app you wish to deploy and select the Actions tab.
   •	Click on set up workflow yourself

   ![image](https://github.com/resgem585/deploy-github-actions/assets/105258020/221561f7-1649-4d58-8e4d-091edc885acd)

   insert this script into your workspace

   name: Upload Website

on:
  push:
    branches:
    - main

jobs:
  deploy-site:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: jakejarvis/s3-sync-action@master
        with:
          args: --delete
        env:
          AWS_S3_BUCKET: myrodolfo-site
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          SOURCE_DIR: ./main

Click on commit to save the workflow

4) Run your Pipeline
    Navigate to Actions to see your pipeline in action

   ![image](https://github.com/resgem585/deploy-github-actions/assets/105258020/749d3217-573c-4a64-a733-f26fd427dda7)

   It should looks

   ![image](https://github.com/resgem585/deploy-github-actions/assets/105258020/faf46ba9-1304-4468-9b4f-55b5064a6595)

5) Now make your changes in your IDE and push to verify the workflow

   ![image](https://github.com/resgem585/deploy-github-actions/assets/105258020/ef9d2b89-1be8-4437-bfed-2f71a9a810ad)


6) Finally verify the changes
   ![image](https://github.com/resgem585/deploy-github-actions/assets/105258020/05fba741-f273-4001-b603-f21d2514ebe2)







   



