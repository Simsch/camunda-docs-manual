---

title: 'Configuring Spin Integration'
category: 'Process Data Formats (XML, JSON, Custom)'

---

In order to use Spin with a process engine, the relevant Spin libraries have to be on the engine's classpath. Furthermore, the process engine plugin provided by Spin has to be registered with the engine. When using a pre-built camunda distribution, Spin is already integrated.

There exist two types of Spin artifacts:

* `camunda-spin-core`: a jar that contains only the core Spin classes. In addition to `camunda-spin-core`, single data format artifacts like `camunda-spin-dataformat-json-jackson` and `camunda-spin-dataformat-xml-dom` exist that provide the JSON and XML functionality. These dependencies should be used when the default data formats have to be reconfigured or when custom data formats are used.
* `camunda-spin-all`: a single jar without dependencies that contains the Spin core, the built-in XML and JSON data formats and the engine integration plugin. `camunda-spin-all` is included in the pre-built-distributions. 

### Maven coordinates

#### `camunda-spin-core`

`camunda-spin-core` contains Spin's core classes that every data format implementation requires. In addition, XML and JSON data formats can be included with the dependencies `camunda-spin-dataformat-json-jackson` and `camunda-spin-dataformat-xml-dom`. These artifacts will transitively pull in their their dependencies, like Jackson in the case of the JSON data format. For integration with the engine, the artifact `camunda-spin-engine-plugin` is needed. The Maven coordinates are as follows:

```xml
<dependency>
  <groupId>org.camunda.spin</groupId>
  <artifactId>camunda-spin-core</artifactId>
  <version>1.0.0-Final</version>
</dependency>
```

```xml
<dependency>
  <groupId>org.camunda.spin</groupId>
  <artifactId>camunda-spin-dataformat-json-jackson</artifactId>
  <version>1.0.0-Final</version>
</dependency>
```

```xml
<dependency>
  <groupId>org.camunda.spin</groupId>
  <artifactId>camunda-spin-dataformat-xml-dom</artifactId>
  <version>1.0.0-Final</version>
</dependency>
```

```xml
<dependency>
  <groupId>org.camunda.spin</groupId>
  <artifactId>camunda-spin-engine-plugin</artifactId>
  <version>1.0.0-Final</version>
</dependency>
```

#### `camunda-spin-all`

This artifact contains the Spin classes, the XML and JSON dataformats as well as their dependencies. To avoid conflicts with other versions of these dependencies, Spin's dependencies are relocated to different packages. `camunda-spin-all` has the following Maven coordinates:

```xml
<dependency>
  <groupId>org.camunda.spin</groupId>
  <artifactId>camunda-spin-all</artifactId>
  <version>1.0.0-Final</version>
</dependency>
```

### Configuring the Spin Process Engine Plugin

`camunda-spin-engine-plugin` contains a class called `org.camunda.spin.plugin.SpinProcessEnginePlugin` that can be registered with a process engine using the [plugin mechanism](ref:/guides/user-guide/#process-engine-process-engine-plugins). For example, a `bpm-platform.xml` file with the plugin enabled would look as follows:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<bpm-platform xmlns="http://www.camunda.org/schema/1.0/BpmPlatform"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://www.camunda.org/schema/1.0/BpmPlatform http://www.camunda.org/schema/1.0/BpmPlatform ">

  ...
  
  <process-engine name="default">
    ...

    <plugins>
      <plugin>
        <class>org.camunda.spin.plugin.SpinProcessEnginePlugin</class>
      </plugin>
    </plugins>
    
    ...
  </process-engine>

</bpm-platform>
```

<div class="alert alert-info">
  <strong>Note:</strong>
  <p>When using a pre-built distribution of camunda BPM, the plugin is already pre-configured.</p>
</div>