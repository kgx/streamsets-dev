# Local StreamSets development environment
## Dependencies
- Docker
- Docker Compose

## Environment Configuration
To get started, copy the example environment file (.env_example) to .env, 
and then you can customize it for your specific environment.

## Running The Services
```
docker-compose up -d
```

## Deploying Custom Extensions to SDC
Three host mount (bind) volumes are included to simplify deployment of custom 
dependencies to your local SDC instance.

| __Volume__ | __Purpose__ |
|-------------------------------------|------------------------------------------------------------------------|
| ./host_volumes/sdc1_user_libs | Custom stage libraries |
| ./host_volumes/sdc1_libs_extras | Custom JAR dependencies for built-in stage libraries |
| ./host_volumes/sdc1_libs_common_lib | JARs that should be available to all stages (e.g. custom EL functions) |

### Deploying custom JAR dependencies for built-in stage libraries
When deploying custom JARs to a specific stage, the files must be placed in a subdirectory 
that matches the directory name of the target stage library (e.g. streamsets-datacollector-jdbc-lib). 

For initial deployment, this is easily achieved by uploading the JAR to the target stage library 
using the built-in SDC Package Manager.  Then, for subsequent deployments,
you can simply overwrite the JAR in your local file system and restart the SDC container.