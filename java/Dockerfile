{{#image}}
  FROM {{{.}}}
{{/image}}

{{^image}}
  FROM maven:3-jdk-11-slim
{{/image}}

WORKDIR /usr/src/app

COPY . ./

{{#patch}}
  {{{.}}}
{{/patch}}

{{#build}}
  RUN {{{.}}}
{{/build}}

{{^build}}
  RUN mvn clean package -q
{{/build}}


FROM openjdk:11-jre-slim

{{#fixes}}
  RUN {{{.}}}
{{/fixes}}

WORKDIR /usr/src/app


{{#files}}
COPY --from=0 /usr/src/app/{{{.}}} {{{.}}}
{{/files}}


WORKDIR /usr/src/app
{{#files}}
COPY --from=0 /usr/src/app/{{{.}}} {{{.}}}
{{/files}}

{{#before_command}}
  RUN {{{.}}}
{{/before_command}}

{{#command}}
  CMD {{{.}}}
{{/command}}
