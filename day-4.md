# Essential Scala for CDP
## Spark Overview
- The many worlds of Spark APIs
  - RDD
  - Dataset and DataFrame
  - Spark SQL

- DataFrames are descriptions
  - Some methods are actions
  
  
## Spark Model
- Cluster manager & executors
- `SparkSession` to read and write data


## Loading Data
- Pain and suffering have come into your life
- Loading CSV
  val df = spark.read
    .option("header", "true")
    .option("inferSchema", "true")
    .csv("../essential-spark/data/cats.csv")
- Use Parquet


## Basic Operations
- show
- count
- printSchema
- distinct


## DataFrame API
- DataFrame is Dataset[Row]
- See Dataset for many methods
- sql.functions for additional methods


## Filtering
- `org.apache.spark.sql`
- Column expressions
  - `col("name")` or `$"name"`
  - `df("name")` to name a column on a `DataFrame`
  - Various operations to transform or compare against other columns
  ```scala
    $("col_name") > 100
  ```
- `filter` or `where` to retain rows matching a column expression
- `select` retain columns matching a column expression.
  - Note this can involve transforming a column at the same time
- `withColumn` to add or replace an existing column
    
    
## Aggregation
- df.agg(column)
- Use the functions in `functions`, or methods on `Column`


## GroupBy
- Apply aggregations to groups determined by column expressions


## TODO
- Data generation
- Timing and performance optimization
- How does BigInt work?
- Vectorization
