### 修改的官方版本

官方openapi-genrator-4.1.3版本

### C#生成Python包的修改

#### 模板位置

```
./modules/openapi-generator/src/main/resources/python
```

#### 模板修改处

- configuration.mustache

  ```python
  #18-21
  # 增加了端口号和主机号设置
  # defalut port
  PORT = {{{apiPort}}}
  # defalut host by env RegServer
  HOST = "http://{}:{}".format(os.getenv("RegServer", "localhost"), PORT)
  ```

- model.mustache

  ```python
  # 删除isEnum标签所含的所有参数检查
  ```

  

### Java源码修改

#### 相关文件位置

- PythonClientCodegen

  ```
  ./modules/openapi-generator/src/main/java/org/openapitools/codegen/languages/PythonClientCodegen.java
  ```

- CodegenConstants

  ```
  ./modules/openapi-generator/src/main/java/org/openapitools/codegen/CodegenConstants.java
  ```

  

#### 源码修改处

- PythonClientCodegen.java

  ```java
  //增加命令行运行jar包可操作的自定义模板参数 apiPort
  //43
  protected String ApiPort;
  //182-184
  if (additionalProperties.containsKey(CodegenConstants.API_PORT)) {
      setApiPort((String)additionalProperties.get(CodegenConstants.API_PORT));
  }
  //205
  additionalProperties.put(CodegenConstants.API_PORT, ApiPort);
  //586
  public void setApiPort(String ApiPort) { this.ApiPort = ApiPort; }
  ```

- CodegenConstants.java

  ```java
  //增加了命令行操作相关模板参数应输入的键 apiPort
  //144-145
  public static final String API_PORT = "apiPort";
  public static final String API_POR_DESC = "port for api lib";
  ```