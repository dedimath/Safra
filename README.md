# Safra
str_list = [col[0] for col in df_vendas_trimestre_spark.dtypes if col[1] in ['string','timestamp','date']]
