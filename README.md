What is Docker ?

A Docker container is a tool that makes it very easy to deploy and run an application using containers. 
A container allows a developer to create an all-in-one package of the developed application with all its dependencies. 
For example, a Java application requires Java libraries, and when we deploy it on any system or VM, we need to install Java first. But, in a container, everything is kept together and shipped as one package, such as in a Docker container.

Step 1:

Intalation:

We have installation for every os, we have give bellow url for window to install the docker desktop.
https://docs.docker.com/docker-for-windows/install


Step 2:

Create an application using Spring boot 
   - Install STS (Spring Tool Suit)
     
  a) Create Spring boot application
    
    *Contraller*
               @SpringBootApplication
               @RestController
               public class DockerWithSpringBootApplication {

                  @RequestMapping("/")
                    public String home() {
                      return "Hello Docker World";
                    }

                  public static void main(String[] args) {
                     SpringApplication.run(DockerWithSpringBootApplication.class, args);
                  }

               }

   
  b) generate the jar using maven
      - right click to pom.xml file 
      - run As - Maven Build
      - after that popup will show and inside popup you need to add following instructins
         a) Goals :  clean compile install
         b) Check the skip Test checkbox
         c) Select the specific jre (I prefer 8)
      - Jar file will be generate in Target folder.
  
  c) create the dockerFile 
       docker file wil contain following information.
       
            FROM openjdk:8-jdk-alpine
            RUN addgroup -S spring && adduser -S spring -G spring
            USER spring:spring
            ARG JAR_FILE=target/*.jar
            COPY ${JAR_FILE} app.jar
            ENTRYPOINT ["java","-jar","/app.jar"]
            
    d) run the spring boot application
        i) check the installed versions it should be same in which we geneerate the jar file using maven.
             java -version
             
        ii) go to the drive where jar is exist
        iii) open the comman prompt and run the following comman
            java -jar nameOfJar.jar
            
                         
    e) run the dockerFile using docker with following Commands
    
      --build the docker image
      docker build -t naemOfDockerimage(small caps) .
      
      --create the new container with port binding and start/run
      docker run -8080:8080 nameofimage

      --check the running images
      docker ps

      --stop the running specific image
      docker container stop nameofimage

      --check all container including running and not running
      doker ps -a

      --start /run the existing container
      docker container start idOfContainer

 	
 


