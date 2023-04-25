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








vcs
RUN cd / && git clon
FROM alpine/git AS e https://github.com/DevProjectsForDevOps/StudentCoursesRestAPI.git && \
 pwd && ls /StudentCoursesRestAPI


FROM python:3.8.3-alpine As Builder
  LABEL author="raji" organization="qt" project="learning"
 COPY --from=vcs /StudentCoursesRestAPI /StudentCoursesRestAPI
   ARG DIRECTORY=StudentCourses
  RUN cd / StudentCoursesRestAPI cp requirements.txt /StudentCourses
   ADD . ${DIRECTORY}
  EXPOSE 8080
  WORKDIR StudentCoursesRestAPI
 RUN pip install --upgrade pip
  RUN pip install -r requirements.txt
  ENTRYPOINT ["python", "app.py"]
