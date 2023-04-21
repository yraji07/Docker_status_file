### Create a Multistage dockerfile 
-----------------------------------

create a ec2 machine 

` sudo apt update `

` curl -fsSL https://get.docker.com -o get-docker.sh `

` sudo sh get-docker.sh `

` sudo usermod -aG docker ubuntu `

` exit `

` re-login `
 
` docker info `

` vi Dockerfile `



FROM ubuntu:22.04 As builder
RUN apt update && apt install unzip -y
ADD https://github.com/nopSolutions/nopCommerce/releases/download/release-4.40.2/nopCommerce_4.40.2_NoSource_linux_x64.zip /nop/nopCommerce_4.40.2_NoSource_linux_x64.zip
RUN cd nop && unzip nopCommerce_4.40.2_NoSource_linux_x64.zip && rm nopCommerce_4.40.2_NoSource_linux_x64.zip


FROM mcr.microsoft.com/dotnet/sdk:7.0
LABEL author="raji" organization="qt" project="learning"
COPY --from=builder /nop /nop-bin
WORKDIR /nop-bin
EXPOSE 5000
CMD [ "dotnet", "Nop.Web.dll", "--urls", "http://0.0.0.0:5000" ]

`docker image build -t nop .  `

![preview](images/build%20image.png)

` docker image ls `
` docker container run --name nop -d -p 32000:5000 nop `
![preview](images/container.png) 

` docker container ls `
` docker image tag nop raji07/rajeshwari-nopcommerce `
` docker image ls `
` docker login `

![preview](images/loginpage.png)

give docker hub username = raji07     
password - ******* 

` docker push -a raji07/rajeshwari-nopcommerce ` 

Now give aws configure 
![preview](images/img2&cli.png)
     
![preview](images/nop.png)
![preview](images/Screenshot%202023-04-21%20170158.png)


![preview](images/ecr%20error%20.png)
