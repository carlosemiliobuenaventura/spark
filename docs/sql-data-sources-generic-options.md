---
layout: global
title: Generic File Source Options
displayTitle: Generic File Source Options
license: |
  Licensed to the Apache Software Foundation (ASF) under one or more
  contributor license agreements.  See the NOTICE file distributed with
  this work for additional information regarding copyright ownership.
  The ASF licenses this file to You under the Apache License, Version 2.0
  (the "License"); you may not use this file except in compliance with
  the License.  You may obtain a copy of the License at
 
     http://www.apache.org/licenses/LICENSE-2.0
 
  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License.
---

* Table of contents
{:toc}

These generic options/configurations are effective only when using file-based sources: parquet, orc, avro, json, csv, text.

Please note that the hierarchy of directories used in examples below are:

{% highlight text %}

dir1/
 ├── dir2/
 │    └── file2.parquet (schema: <file: string>, content: "file2.parquet")
 └── file1.parquet (schema: <file, string>, content: "file1.parquet")
 └── file3.json (schema: <file, string>, content: "{'file':'corrupt.json'}")

{% endhighlight %}

### Ignore Corrupt Files

Spark allows you to use `spark.sql.files.ignoreCorruptFiles` to ignore corrupt files while reading data
from files. When set to true, the Spark jobs will continue to run when encountering corrupted files and
the contents that have been read will still be returned.

To ignore corrupt files while reading data files, you can use:

<div class="codetabs">
<div data-lang="scala"  markdown="1">
{% include_example ignore_corrupt_files scala/org/apache/spark/examples/sql/SQLDataSourceExample.scala %}
</div>

<div data-lang="java"  markdown="1">
{% include_example ignore_corrupt_files java/org/apache/spark/examples/sql/JavaSQLDataSourceExample.java %}
</div>

<div data-lang="python"  markdown="1">
{% include_example ignore_corrupt_files python/sql/datasource.py %}
</div>

<div data-lang="r"  markdown="1">
{% include_example ignore_corrupt_files r/RSparkSQLExample.R %}
</div>
</div>

### Ignore Missing Files

Spark allows you to use `spark.sql.files.ignoreMissingFiles` to ignore missing files while reading data
from files. Here, missing file really means the deleted file under directory after you construct the
`DataFrame`. When set to true, the Spark jobs will continue to run when encountering missing files and
the contents that have been read will still be returned.

### Path Global Filter

`pathGlobFilter` is used to only include files with file names matching the pattern.
The syntax follows <code>org.apache.hadoop.fs.GlobFilter</code>.
It does not change the behavior of partition discovery.

To load files with paths matching a given glob pattern while keeping the behavior of partition discovery,
you can use:

<div class="codetabs">
<div data-lang="scala"  markdown="1">
{% include_example load_with_path_glob_filter scala/org/apache/spark/examples/sql/SQLDataSourceExample.scala %}
</div>

<div data-lang="java"  markdown="1">
{% include_example load_with_path_glob_filter java/org/apache/spark/examples/sql/JavaSQLDataSourceExample.java %}
</div>

<div data-lang="python"  markdown="1">
{% include_example load_with_path_glob_filter python/sql/datasource.py %}
</div>

<div data-lang="r"  markdown="1">
{% include_example load_with_path_glob_filter r/RSparkSQLExample.R %}
</div>
</div>

### Recursive File Lookup
`recursiveFileLookup` is used to recursively load files and it disables partition inferring. Its default value is `false`.
If data source explicitly specifies the `partitionSpec` when `recursiveFileLookup` is true, exception will be thrown.

To load all files recursively, you can use:

<div class="codetabs">
<div data-lang="scala"  markdown="1">
{% include_example recursive_file_lookup scala/org/apache/spark/examples/sql/SQLDataSourceExample.scala %}
</div>

<div data-lang="java"  markdown="1">
{% include_example recursive_file_lookup java/org/apache/spark/examples/sql/JavaSQLDataSourceExample.java %}
</div>

<div data-lang="python"  markdown="1">
{% include_example recursive_file_lookup python/sql/datasource.py %}
</div>

<div data-lang="r"  markdown="1">
{% include_example recursive_file_lookup r/RSparkSQLExample.R %}
</div>
</div>