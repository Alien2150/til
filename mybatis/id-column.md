I recently faced an issue where i was not getting back the proper amount of sql-results in a query when using "ResultMap"

Here's how to "force" it:

```
CREATE TABLE test(
  id: int, 
  foo: varchar
);

INSERT INTO test(id, value) VALUES
  (1, 'test'),
  (2, 'test');
```

My Kotlin data-class looks like this:
```
data class Test(id: Int, foo: String)
```

When using a result mapper in MyBatis:

```
<select id="getTests" resultMap="testMap">
  select * from tests
</select>

<resultMap id="testMap" type="com.test.Test" autoMapping="true">
</resultMap>
```

This might end up in 1 row but not 2. This is fixable by adding id to the resultMap:

```
<resultMap id="testMap" type="com.test.Test" autoMapping="true">
  <id column="id" property="id"/>
</resultMap>
```
