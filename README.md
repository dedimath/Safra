# Safra
l=[("a",1)]
ll=["id","sa"]
df=spark.createDataFrame(l,ll)

hdfs_dir = "/folder/" #your hdfs directory
new_filename="my_name.json" #new filename

df.coalesce(1).write.format("json").mode("overwrite").save(hdfs_dir)

fs = spark._jvm.org.apache.hadoop.fs.FileSystem.get(spark._jsc.hadoopConfiguration())

#list files in the directory

list_status = fs.listStatus(spark._jvm.org.apache.hadoop.fs.Path(hdfs_dir))

#filter name of the file starts with part-

file_name = [file.getPath().getName() for file in list_status if file.getPath().getName().startswith('part-')][0]

#rename the file

fs.rename(Path(hdfs_dir+''+file_name),Path(hdfs_dir+''+new_filename))
