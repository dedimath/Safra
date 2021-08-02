# Safra

DATA_ASSOC_PIX: campo presente no arquivo INFO_ADD_AGZERO, Gabriel ainda está analisando a regra.
 Resposta: 
 O campo DATA_ASSOC_PIX pode ser recuperado pelo join entre a BCDTUCD.ID_USR + o seguinte sub select
 para facilitar montei o select: 
 
   select ASSOC_PIX.DATA_ASSOC as DATA_ASSOC_PIX,
     FROM BCD.BCDTUCD CAD
left join ( 
     SELECT DISTINCT A.*,CAD.ID_USR,CAD.ID_CPF_DOC
 FROM ( 
 select cd_pto_vda as agencia 
,cta_corrente  as CONTA
,dt_abertura
  from DB_CORPORATIVO.CONTA.CORRENTEATUAl
 WHERE CD_PTO_VDA IN ('9784','28400')  
) A
INNER JOIN  BCD.BCDTCDL PWD ON A.AGENCIA = PWD.CD_AG AND A.CONTA = PWD.ID_NUM_CC
INNER JOIN  BCD.BCDTUCD CAD ON PWD.ID_USR = CAD.ID_USR
            ) cta ON CAD.ID_USR = CTA.ID_USR
 left join (
        SELECT distinct aa.AGENCIA,aa.CONTA, aa.DATA_ASSOC  
FROM [DB_CRM].[DBO].TB_PWBI_ASSOC_PIX (nolock) aa
inner join( SELECT distinct case when AGENCIA = '0097' then '09784'
when AGENCIA = '0284' then '28400'
end as AGENCIA
,CONTA 
FROM [DB_CRM].[DBO].[TBCRM_CADASTRO_PIX] (nolock)
WHERE STATUS = 'ATIVA'
) bb
on aa.agencia = bb.agencia and aa.conta = bb.conta
WHERE aa.agencia in ('09784','28400') 
and CLI_ASSOC = 1
           ) ASSOC_PIX ON (CTA.AGENCIA = ASSOC_PIX.AGENCIA  AND CTA.CONTA = ASSOC_PIX.CONTA )

