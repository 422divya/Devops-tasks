**CI/CD pipeline in AWS**

# CodeCommit:

1- Created AWS CodeCommit repository on AWS.
2- Created IAM user to use with codecommit, attached the codecommit policy so that user access codecommit, created https git credentials for user.
3- Then cloned the CodeCommit repository in the local machine by giving the credentials genertaed for https.
4- Created file in local and commited it using git.
5- Then pushed the changed to the remote repository i.e on AWS codecommit repository.

~~~~~~~~~~~~~~~~~~~~~~~~~
IAM user HTTPS credentials to authenticate codecommit locally.
divya-at-434309355563
GWZoyZ8uUrkKtbEkaCwDmBHOcIh9ml2Nr/CVN5xdZK4=
~~~~~~~~~~~~~~~~~~~~~~~~~

# CodeBuild
