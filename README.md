What This Guide Covers
-------------------------
This guide will help you integrate SourceNinja into your Maven work-flow. This only needs to be done once.

What is the SourceNinja module
---------------------------
The SourceNinja maven plugin can be included in your build and release work-flow to allow seamless integration with SourceNinja. The SourceNinja plugin will send all of your artifacts and versions to SourceNinja to begin managing your open source libraries.

Getting Started
---------------
1. Create a [SourceNinja](http://sourceninja.com) account.

2. Log into SourceNinja and create a product. The product you create will be paired with your application.

3. After you create a product, you will be directed to a page asking what language your application is running. Select `Java` from the menu on the left side.

4. You will be presented with two values, you'll need these two values later.

  	Example:

		SOURCENINJA_PRODUCT_ID="477fcfa7-765a-4b91-b6a5-2ebe4c4f9d58"
		SOURCENINJA_TOKEN="50a336d92da8ddea1ae0a6c0d06a172"

5. Add the [SourceNinja plugin](https://github.com/SourceNinja/sourceninja-maven) to your Maven project. You can do this by adding the following lines to your `pom.xml`.

    ```xml
    <plugins>
      <plugin>
	  	<groupId>com.sourceninja</groupId>
	  	<artifactId>sourceninja-maven-plugin</artifactId>
        <version>0.1.5</version>
		<configuration>
		  <id>${env.PRODUCT_ID}</id>
		  <token>${env.PRODUCT_TOKEN}</token>
		</configuration>
      </plugin>
    </plugins>
   ```

6. Set the values of <id> and <token> in the configuration block of the XML from the previous step using the values obtained in step 4. You can choose to store these values as environment variables as demonstrated above, or you can embed them as string literals.

7. At this point the module is configured. Dependency data is sent to SourceNinja by triggering the ```send``` goal. This goal needs to be triggered after your dependencies are resolved, typically after the compile or test phase.

   ```mvn com.sourceninja:sourceninja-maven-plugin:0.1.5:send```

8. If you want your open source usage sent to SourceNinja when your artifacts are built, you can configure maven to trigger the plugin during the package phase. For example the configuration below will send data to SourceNinja every time the build is packaged.

    ```xml
    <plugins>
      <plugin>
	  	<groupId>com.sourceninja</groupId>
	  	<artifactId>sourceninja-maven-plugin</artifactId>
        <version>0.1.5</version>
		<configuration>
		  <id>${env.PRODUCT_ID}</id>
		  <token>${env.PRODUCT_TOKEN}</token>
		</configuration>
		<executions>
		  <execution>
			<id>package</id>
			<phase>package</phase>
			<goals>
			  <goal>send</goal>
			</goals>
		  </execution>
		</executions>
      </plugin>
    </plugins>
    ```

Support
-------
Feel free to email us at support at sourceninja dot com if you have any questions or issues.