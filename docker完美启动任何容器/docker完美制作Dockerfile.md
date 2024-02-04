```dockerfile
from openjava:8
EXPOSE 8080
ADD demo-0.0.1-SNAPSHOT.jar app.jar
run bash -c 'touch /app.jar'
ENTRYPOINT ["java","-jar","/app.jar"]
```

