pipeline {
   agent any

   environment {
 
     SERVICE_NAME = "fleetman-webapp"
     ECR_URI = "738942673819.dkr.ecr.us-east-2.amazonaws.com/fleetman-webapp"
     REPOSITORY_TAG ="${ECR_URI}:${BUILD_ID}"
   }

   stages {
      
      stage('Build') {
         steps {
            sh 'echo No build required for Webapp.'
         }
      }

      stage('Build and Push Image') {
         steps {
           sh 'aws ecr --region us-east-2 | docker login -u AWS -p eyJwYXlsb2FkIjoic2N6b2RHNE8vckhjSDQ2Y0tnRmxKWlY2dWVPTm9aZCtRN2I2V1VYSFhBczRBSktrYkRHTkN6Y3lHdWFvUlkrY1JEWjJ0VUFMeEJNQWJNajNhWmk3d1RiNXdiSUVKOUFUUHN1K3Z0NkJ0ZUczbmZiWktwM050NC9CakVvUU0zVVQ2RmZnYndCWTBYNitJWFBUcTZWdmNZQWNSQk9kaDdlQUFyOVZGUzBpWk1CZzRyc3hpNEVqQ3JzWkgyNjVRMmJCYmluRm15b1FHSUc1bnRpejNaYmR6aVptTGZBbWNKSnZ2MkcvSGtZWWxqN3Y1T3hzS1VhVnBhOExWaHNZYXU1VEFJR21DOTBoWUtpVTVVaEJCQTQvS1VXS3pmZjJRd3ZBaG8waU9tazNVa05kazVYYUFMUUxGMm1jUTFpRndRYVFvTEZlZlJLVFRFRTh5L2QxYnBTeUM1Ykpmdi9xb2xSdE1Uc2VNVFc0bDRPampuNkJFYTFtRC83WDlkSWdrV3FFT2o0N25OUnhLZWdtTlo1S29EbXdxNDJLZXozT1hJYy8xQll4bEVEVUVrSkFFSUx5QW05dElhUVB4OUcyRC8xbXRmWk1UNzNPQ3F3YnVDcXI0TjNkWEZ3S0NKOFZtYno3c042c3FpQUc4dEMvMituS2ZRM0J6aGswZnd4QnlLbk53c25oS05WWGlhM1p6V29zc0ViQy9YeHlSbDdsenhrQlh1TmNKL3NiNGcrenBpUGJnc2Y4Zzlkc2V1cTV6VmlrcWxwaHM4UmFoM3FrL3Y2bElYNks4L29LZHZGL0ZrNUl6WTdZcW9IRlFKVzA2bW15TEg2MmdLTEtvUnFQdk13REQyekVYUURNeGJvWDJFdmJDWktGSnZRdWVCVDRHNXBmVWRSZGVWZk1WSTd4cVlRemJNVWZMK0dzTXlmN1RjQjJVR1I0d0RDNmtIaTZza0dEd0FjRjBITXFYS0g1UjFYaE1ZNnJHRjhWd1B0Ry9vYWFXVmtGclltaHkxS0tjVExoWkgvOTFDOUMvNWpoSzlrMGp6MkZ3R1J2Z3FoSHFad2xsekFDdWY1cUFod0kwcHk1aDFpdkRpKzFHMUNtZ2NGeGo2dWJxK2tMWDAwSUpsaGdlbTB0cmpJNTIwUkdwNm9NZERxTExQY3FqSkY3RFNtUlVCMVdiR2JtcVNpcmQzTW5DaG9FTW5hcDNvQXgzaDJIbEpLU2hXMkVKUERyZERlSnB2enliWDJBL3pxRUF4c1FsZkpNcHBWZ2Y2Z1RhUnpvSGlFYUxsTHF4NnltOTROSWhBdGdwekorbVo1L1JxTDI1YUdpTlozTitONldidlE4UkUwYTVsNEdyM0xSbmQrM3RFdWk1a3paVzBOMjNJL0tkQT09IiwiZGF0YWtleSI6IkFRRUJBSGpCNy9pZ3dNZzROUHdhdXJ4U0lZeDRIZm54dUdjLzQ4YkR3dndEcE5ZV1pnQUFBSDR3ZkFZSktvWklodmNOQVFjR29HOHdiUUlCQURCb0Jna3Foa2lHOXcwQkJ3RXdIZ1lKWUlaSUFXVURCQUV1TUJFRURMbXhPTHlTM3B3Q2RkWUdoUUlCRUlBN29UcnJLOGJoVCtVZ1pyYVJxUDBoaVE3WVIvRUxSMktYenEzT3NreENCeVc4OG9lZDlaNmVQTTJ1SXRMU1l0NXZkd0RHVVluMlNCK254d2M9IiwidmVyc2lvbiI6IjIiLCJ0eXBlIjoiREFUQV9LRVkiLCJleHBpcmF0aW9uIjoxNjUyOTEzNDMwfQ== 738942673819.dkr.ecr.us-east-2.amazonaws.com/fleetman-webapp'
           sh 'docker image build -t ${REPOSITORY_TAG} .'
           sh 'docker push ${REPOSITORY_TAG}'
         }
      }

      stage('Deploy to Cluster') {
          steps {
            sh 'envsubst < /var/lib/jenkins/workspace/fleetman-webapp/jenkins-cluster-admin-config | ${WORKSPACE}/deploy.yaml | /usr/local/bin/kubectl apply -f -'
          }
      }
   }
}
