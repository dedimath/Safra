# Safra

def myConcat(*cols):
    concat_columns = []
    print(str_list)
    for c in cols[:-1]:
        print(c)
        if c in str_list:
            concat_columns.append(F.lit('"'))
            concat_columns.append(F.coalesce(c, F.lit("")))
            concat_columns.append(F.lit('"'))
        else:
            concat_columns.append(F.coalesce(c, F.lit("")))
        concat_columns.append(F.lit("|"))  
    if cols[-1] in str_list:
        concat_columns.append(F.lit('"'))
        concat_columns.append(F.coalesce(cols[-1], F.lit("")))
        concat_columns.append(F.lit('"'))
    else:
        concat_columns.append(F.coalesce(c, F.lit("")))
    return F.concat(*concat_columns)


teste = df_vendas_trimestre_spark.withColumn(col_name, myConcat(*df_vendas_trimestre_spark.columns)).select(col_name)
