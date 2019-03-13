# Gradle

## Accessing Buildscript ClassPath

```groovy
 project.buildscript.configurations.classpath
```

Reference: https://discuss.gradle.org/t/accessing-the-buildscript-classpath/5297/2

### Create a project in groovy test	
```groovy
Project project = ProjectBuilder.builder().build()
```
- https://docs.gradle.org/current/userguide/custom_plugins.html

### Write an input stream to file	

```groovy    
FileUtils.copyInputStreamToFile(initialStream, targetFile);
```
- https://www.baeldung.com/convert-input-stream-to-a-file

### Deserialize Generic	
```groovy
ObjectMapper mapper = new ObjectMapper();
JavaType type = mapper.getTypeFactory().constructParametrizedType(Data.class, Data.class, Parameter.class);
Data<Parameter> dataParam = mapper.readValue(jsonString,type)
```

- https://stackoverflow.com/questions/11664894/jackson-deserialize-using-generic-class


### Gradle Lines	

```groovy
multiline.eachLine { line, count ->
    if (count == 0) {
        println "line $count: $line"  // Output: line 0: Groovy is closely related to Java,
    }
}
```

- http://mrhaki.blogspot.com/2009/11/groovy-goodness-working-with-lines-in.html

### Check task pipeline	
```sh
./gradlew clean build publish -m
```
- http://mrhaki.blogspot.com/2014/11/gradle-goodness-check-task-dependencies.html

### Jackson Ignore Unknown Properties	

```groovy
new ObjectMapper()
  .configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false)
```

- https://www.baeldung.com/jackson-deserialize-json-unknown-properties

### Gradle Unzip File	
- https://docs.gradle.org/current/userguide/working_with_files.html#sec:unpacking_archives_example

```groovy
task unpackFiles(type: Copy) {
    from zipTree("src/resources/thirdPartyResources.zip")
    into "${buildDir}/resources"
}
```

### String Split with All Delimiters	

```groovy
s.trim().split("[\\W]+") 
```

- https://stackoverflow.com/questions/5993779/use-string-split-with-multiple-delimiters

### Groovy ConvertAll	

```groovy
List<Integer> testCaseNumbers = new ArrayList<>();
report.testDetails.each {TestDetail t ->
    t.testCaseNumbers.addAll(t.testCaseNumbers)
}


List<RallyTestCase> response = rallyProvider.getTestCases(testCaseNumbers.collect{x->x.toString()})


//converts [1,2,3] -> ["1","2","3"]
```


### Run Specific Build	

```sh
gradlew -b <filenam> task
```
### Stop gradle build upon test fail	

```groovy
test.afterTest { TestDescriptor td, TestResult tr ->
    if (tr.resultType == ResultType.FAILURE) {
        throw new Exception("$td failed")
    } 
} 
```

- https://stackoverflow.com/questions/41786063/stop-gradle-build-when-a-unit-test-fails

### Setup on System out	

```java
    private PrintStream sysOut;
    private final ByteArrayOutputStream outContent = new ByteArrayOutputStream();


    @Before
    public void setUpStreams() {
        sysOut = System.out;
        PrintStream contentOutputStream = new PrintStream(outContent)
        System.setOut( new PrintStream( new TeeOutputStream(sysOut, contentOutputStream)));

    }

    @After
    public void revertStreams() {
        System.setOut(sysOut);
    }


    @Test
  
    void test_(){


        ...

        Assert.assertTrue(outContent.toString().contains("<Message>"));


    }
```

### Json Parsing

```groovy
new JsonSlurper().parseText(jsonAsText)
```

### Pass parameters to Gradle Script

```sh
./gradlew myTask -PmyArg=hello
```

which can be used as 
```groovy
println "$project.myArg"
```

See https://stackoverflow.com/a/48370451/474377
