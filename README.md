## Implementation of an end-to-end AWS DevSecOps CI/CD pipeline with open-source SCA, SAST, and DAST tools

In today's fast-paced software development landscape, organizations are constantly seeking ways to accelerate the delivery of reliable and secure applications. DevSecOps, an approach that combines development, security, and operations, has emerged as a solution to integrate security practices seamlessly into the software development lifecycle. One crucial aspect of implementing DevSecOps is the establishment of a robust CI/CD pipeline. In this blog, we will explore the implementation of an end-to-end AWS DevSecOps CI/CD pipeline, leveraging open-source Software Composition Analysis (SCA), Static Application Security Testing (SAST), and Dynamic Application Security Testing (DAST) tools.





Security Termrs 



Tools















# Step: 2 -  Adding Security to AWS Pipepline
   
   1. Integrate SonarCloud with AWS CodeCommit and CodeBuild ( SAST Scan )
        Create SonarCloud account
        Set up AWS Secret manager and store Sonarcloud Tokens


            Update buildspec.yml file
                  env:
                secrets-manager:
                  TOKEN: firstSecret:tokenForSonar
            phases:
              build:
                commands:
                  - mvn verify sonar:sonar -Dsonar.projectKey=javaprojectaws -Dsonar.organization=javaprojectaws -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=$TOKEN 
                  - sleep 5
                  - |- 
                    quality_status=$(curl -s -u $TOKEN: https://sonarcloud.io/api/qualitygates/project_status?projectKey=javaprojectaws | jq -r '.projectStatus.status')
                    echo "SonarCloud analysistatus is $quality_status"; 
                    if [ $quality_status = "ERROR" ] ; then exit 1;fi
              
      
![image](https://github.com/iamdeborah-Q/AWS-Cloud-DevSecOps-Project/assets/122198373/60c7de3f-36e3-4a2d-8024-cd7f948278e8)
![image](https://github.com/iamdeborah-Q/AWS-Cloud-DevSecOps-Project/assets/122198373/532dccb9-35a6-4da3-9812-af2174deb91e)
![image](https://github.com/iamdeborah-Q/AWS-Cloud-DevSecOps-Project/assets/122198373/e4cceb89-9961-4411-aeb9-1533d3275624)






   2. Integrate Snyk with AWS CodeCommit and CodeBuild (SCA Scan)

     Run Software Compostion Analysis using Snyk



      ![image](https://github.com/iamdeborah-Q/AWS-Cloud-DevSecOps-Project/assets/122198373/29cd404f-70f4-49fe-a56e-11282213dd2f)



  3. Integrate OWASP ZAP with AWS CodeCommit and CodeBuild (DAST Scan)
     Run Dynamic Application Securit Testing using OWASP ZAP
     Create Amazon S3 Bucket for Artifacts

     ![image](https://github.com/iamdeborah-Q/AWS-Cloud-DevSecOps-Project/assets/122198373/ba51f61f-ac35-4b5f-8f42-85a4b64d0504)



      


# Step: 3 - End-to-End DevSecOps Pipepline
  Write a code to intergrate security into AWS Code pipeline

  ![image](https://github.com/iamdeborah-Q/AWS-Cloud-DevSecOps-Project/assets/122198373/d6c8ad13-fd3b-410a-877a-4105188e3fa1)





# Step : 4 - Create JIRA Account to Report Security Issues 


![image](https://github.com/iamdeborah-Q/AWS-Cloud-DevSecOps-Project/assets/122198373/86967eac-06fa-4622-9a62-36a625567b5b)

 Below consist of all analysis on JIRA

 ![image](https://github.com/iamdeborah-Q/AWS-Cloud-DevSecOps-Project/assets/122198373/056f426a-517c-45bf-b544-4df3843ab663)




## AWS Security Compliance 

Implement AWS Security Hub withion our infracture
  set up AWS Config and enable confliance rule


![image](https://github.com/iamdeborah-Q/AWS-Cloud-DevSecOps-Project/assets/122198373/6b97c732-45c7-466a-93e9-bc5c49e790ac)


AWS Inspector 

Activate 
intergrate EC2 

        1) Create an EC2 instance and enable port http:80 in the security group
        2) SSM agent should be installed on EC2 instance 
        3) SSM agent should be running on EC2 instance
