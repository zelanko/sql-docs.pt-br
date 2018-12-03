---
title: Tipos definidos pelo usuário CLR grandes (OLE DB) | Microsoft Docs
description: Tipos definidos pelo usuário CLR grandes (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types [OLE DB]
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: b5c071a36cebacc8ce0dea5c1633bf3f92b28599
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52409603"
---
# <a name="large-clr-user-defined-types-ole-db"></a>Tipos definidos pelo usuário CLR grandes (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este tópico aborda as alterações feitas no OLE DB no OLE DB Driver for SQL Server para dar suporte aos UDTs (tipos definidos pelo usuário) CLR (Common Language Runtime) grandes.  
  
 Para obter mais informações sobre o suporte para UDTs CLR grandes no Driver do OLE DB para SQL Server, consulte [Large CLR User-Defined tipos](../../oledb/features/large-clr-user-defined-types.md). Para obter um exemplo, consulte [UDTs CLR grandes de uso &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-large-clr-udts-ole-db.md).  
  
## <a name="data-format"></a>Formato de Dados  
 O OLE DB Driver for SQL Server usa ~0 para representar o tamanho de valores de tamanho ilimitado para tipos de objeto grande (LOB). ~ 0 também representa o tamanho de UDTs CLR maiores que 8.000 bytes.  
  
 A seguinte tabela mostra o mapeamento de tipo de dados em parâmetros e conjuntos de linhas:  
  
|Tipo de dados do SQL Server|Tipo de dados OLE DB|Layout de memória|Valor|  
|--------------------------|----------------------|-------------------|-----------|  
|CLR UDT|DBTYPE_UDT|BYTE[](matriz de bytes\)|132 (oledb.h)|  
  
 Os valores UDT são representados como matrizes de bytes. Há suporte para conversões de cadeias hexadecimais e para cadeias hexadecimais. Os valores literais são representados como cadeias de caracteres hexadecimais com um prefixo "0x". Uma cadeia de caracteres hexadecimal é a representação textual de dados binários na base 16. Um exemplo é uma conversão do tipo de servidor **varbinary(10)** em DBTYPE_STR, que resulta em uma representação hexadecimal de 20 caracteres, em que cada par de caracteres representa um único byte.  
  
## <a name="parameter-properties"></a>Propriedades de parâmetro  
 O conjunto de propriedades DBPROPSET_SQLSERVERPARAMETER dá suporte a UDTs através do OLE DB. Para obter mais informações, confira [Usando tipos definidos pelo usuário](../../oledb/features/using-user-defined-types.md).  
  
## <a name="column-properties"></a>Propriedades de coluna  
 O conjunto de propriedades DBPROPSET_SQLSERVERCOLUMN dá suporte à criação de tabelas através do OLE DB. Para obter mais informações, confira [Usando tipos definidos pelo usuário](../../oledb/features/using-user-defined-types.md).  
  
## <a name="data-type-mapping-in-itabledefinitioncreatetable"></a>Mapeamento de tipo de dados em ITableDefinition::CreateTable  
 As seguintes informações são usadas em estruturas **DBCOLUMNDESC** usadas por ITableDefinition::CreateTable quando as colunas UDT são obrigatórias:  
  
|Tipo de dados OLE DB (*wType*)|*pwszTypeName*|Tipo de dados do SQL Server|*rgPropertySets*|  
|----------------------------------|--------------------|--------------------------|----------------------|  
|DBTYPE_UDT|Ignored|UDT|Deve incluir um conjunto de propriedades DBPROPSET_SQLSERVERCOLUMN.|  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 As informações retornadas na estrutura DBPARAMINFO por meio de **prgParamInfo** são as seguintes:  
  
|Tipo de parâmetro|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags* se DBPARAMFLAGS_ISLONG|  
|--------------------|-------------|-------------------|------------------|--------------|------------------------------------|  
|DBTYPE_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|"DBTYPE_UDT"|*n*|não definido|não definido|clear|  
|DBTYPE_UDT<br /><br /> (comprimento maior que 8.000 bytes)|"DBTYPE_UDT"|~ 0|não definido|não definido|set|  
  
## <a name="icommandwithparameterssetparameterinfo"></a>ICommandWithParameters::SetParameterInfo  
 As informações fornecidas na estrutura DBPARAMBINDINFO devem estar de acordo com o seguinte:  
  
|Tipo de parâmetro|*pwszDataSourceType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags* se DBPARAMFLAGS_ISLONG|  
|--------------------|--------------------------|-------------------|------------------|--------------|------------------------------------|  
|DBTYPE_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|DBTYPE_UDT|*n*|ignorado|ignorado|Deve ser definido se o parâmetro for passado usando DBTYPE_IUNKNOWN.|  
|DBTYPE_UDT<br /><br /> (comprimento maior que 8.000 bytes)|DBTYPE_UDT|~ 0|ignorado|ignorado|ignorado|  
  
## <a name="isscommandwithparameters"></a>ISSCommandWithParameters  
 Os aplicativos usam **ISSCommandWithParameters** para obter e definir as propriedades de parâmetro definidas na seção Propriedades de parâmetro.  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 As colunas são retornadas da seguinte maneira:  
  
|Tipo de coluna|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE|DBCOLUMN_FLAGS_ISLONG|DBCOLUMNS_ISSEARCHABLE|DBCOLUMN_OCTETLENGTH|  
|-----------------|--------------------|--------------------------|-------------------------|---------------------|-----------------------------|-----------------------------|---------------------------|  
|DBTYPE_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|DBTYPE_UDT|*n*|NULL|NULL|Liberada|DB_ALL_EXCEPT_LIKE|n|  
|DBTYPE_UDT<br /><br /> (comprimento maior que 8.000 bytes)|DBTYPE_UDT|~ 0|NULL|NULL|Defina|DB_ALL_EXCEPT_LIKE|0|  
  
 As seguintes colunas também são definidas para UDTs:  
  
|Identificador de coluna|Tipo|Descrição|  
|-----------------------|----------|-----------------|  
|DBCOLUMN_UDT_CATALOGNAME|DBTYPE_WSTR|Para colunas de UDT, o nome do catálogo onde o UDT foi definido.|  
|DBCOLUMN_UDT_SCHEMANAME|DBTYPE_WSTR|Para colunas de UDT, o nome do esquema onde o UDT foi definido.|  
|DBCOLUMN_UDT_NAME|DBTYPE_WSTR|Para colunas de UDT, o nome de uma única parte do UDT.|  
|DBCOLUMN_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Para colunas de UDT, o nome de tipo completo do UDT. O nome totalmente qualificado do tipo de assembly permite que você crie uma instância de um objeto daquele tipo usando o método Type.GetType.|  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 As informações retornadas na estrutura DBCOLUMNINFO são as seguintes:  
  
|Tipo de parâmetro|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBCOLUMNFLAGS_ISLONG|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------|  
|DBTYPE_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|DBTYPE_UDT|*n*|~ 0|~ 0|Liberada|  
|DBTYPE_UDT<br /><br /> (comprimento maior que 8.000 bytes)|DBTYPE_UDT|~ 0|~ 0|~ 0|Defina|  
  
## <a name="columns-rowset-schema-rowsets"></a>Conjunto de linhas COLUMNS (conjuntos de linhas de esquema)  
 Os seguintes valores de coluna são retornados para tipos UDT:  
  
|Tipo de coluna|DATA_TYPE|COLUMN_FLAGS, DBCOLUMFLAGS_ISLONG|CHARACTER_OCTET_LENGTH|  
|-----------------|----------------|-----------------------------------------|------------------------------|  
|DBTYPE_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|DBTYPE_UDT|Liberada|*n*|  
|DBTYPE_UDT<br /><br /> (comprimento maior que 8.000 bytes)|DBTYPE_UDT|Defina|0|  
  
 As seguintes colunas adicionais são definidas para UDTs:  
  
|Identificador de coluna|Tipo|Descrição|  
|-----------------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Para colunas de UDT, o nome do catálogo onde o UDT foi definido.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Para colunas de UDT, o nome do esquema onde o UDT foi definido.|  
|SS_UDT_NAME|DBTYPE_WSTR|Para colunas de UDT, o nome de uma única parte do UDT.|  
|SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Para colunas de UDT, este é o nome de tipo completo do UDT. O nome totalmente qualificado do tipo de assembly permite que você crie uma instância de um objeto daquele tipo usando o método Type.GetType.|  
  
 Relativo ao conjunto de linhas PROCEDURE_PARAMETERS, DATA_TYPE contém os mesmos valores que o conjunto de linhas de esquema COLUMNS e TYPE_NAME contém o UDT. As mesmas colunas adicionais também são definidas.  
  
 Os tipos definidos pelo usuário não aparecerão no conjunto de linhas de esquema PROVIDER_TYPES.  
  
## <a name="bindings-and-conversions"></a>Associações e conversões  
  
|Tipo de dados de associação|UDT para servidor|Não UDT para servidor|UDT de servidor|Não UDT de servidor|  
|----------------------|-------------------|------------------------|---------------------|--------------------------|  
|DBTYPE_UDT|Compatível (5)|Erro (1)|Compatível (5)|Erro (4)|  
|DBTYPE_BYTES|Compatível (5)|N/A|Compatível (5)|N/A|  
|DBTYPE_WSTR|Com suporte (2), (5)|N/A|Com suporte (3), (5), (6)|N/A|  
|DBTYPE_BSTR|Com suporte (2), (5)|N/A|Compatível (3), (5)|N/A|  
|DBTYPE_STR|Com suporte (2), (5)|N/A|Compatível (3), (5)|N/A|  
|DBTYPE_IUNKNOWN|Compatível (6)|N/A|Compatível (6)|N/A|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|Com suporte (5)|N/A|Compatível (3), (5)|N/A|  
|DBTYPE_VARIANT (VT_BSTR)|Com suporte (2), (5)|N/A|N/A|N/A|  
  
### <a name="key-to-symbols"></a>Legenda dos símbolos  
  
|Símbolo|Significado|  
|------------|-------------|  
|1|Se um tipo de servidor diferente de DBTYPE_UDT for especificado com **ICommandWithParameters::SetParameterInfo** e o tipo de acessador for DBTYPE_UDT, ocorrerá um erro quando a instrução for executada.  O erro será DB_E_ERRORSOCCURRED e o status do parâmetro será DBSTATUS_E_BADACCESSOR.<br /><br /> É um erro especificar um parâmetro de tipo UDT para um parâmetro de servidor que não seja UDT.|  
|2|Os dados são convertidos de cadeia de caracteres hexadecimal em dados binários.|  
|3|Os dados são convertidos de dados binários em cadeia de caracteres hexadecimal.|  
|4|A validação pode ser feita usando **CreateAccessor** ou **GetNextRows**. O erro é DB_E_ERRORSOCCURRED. O status de associação é definido como DBBINDSTATUS_UNSUPPORTEDCONVERSION.|  
|5|BY_REF pode ser usado.|  
|6|Os parâmetros de UDT podem ser associados como DBTYPE_IUNKNOWN no DBBINDING. A associação a DBTYPE_IUNKNOWN indica que o aplicativo deseja processar os dados como um fluxo usando a interface ISequentialStream. Quando um consumidor especifica *wType* em uma associação como tipo DBTYPE_IUNKNOWN e a coluna correspondente ou a saída o parâmetro do procedimento armazenado é um UDT, o Driver do OLE DB para SQL Server retornará ISequentialStream. Um parâmetro de entrada para o Driver do OLE DB para SQL Server irá consultar o para a interface ISequentialStream.<br /><br /> Você pode optar por não associar o comprimento de dados de UDT enquanto estiver usando a associação DBTYPE_IUNKNOWN, no caso de UDTs grandes. Porém, o comprimento deve estar associado a UDTs pequenos. Um parâmetro DBTYPE_UDT poderá ser especificado como um UDT grande nos seguintes casos:<br />*ulParamParamSize* é ~ 0.<br />Se DBPARAMFLAGS_ISLONG estiver definido na estrutura DBPARAMBINDINFO.<br /><br /> Para dados de linha, a associação de DBTYPE_IUNKNOWN é permitida só para UDTs grandes. Você pode descobrir se uma coluna é um tipo UDT grande, usando o método icolumnsinfo:: Getcolumninfo em um conjunto de linhas ou interface de IColumnsInfo do objeto de comando. Uma coluna DBTYPE_UDT será uma coluna de UDT grande se uma ou mais destas condições for verdadeira:<br />O sinalizador DBCOLUMNFLAGS_ISLONG é definido no membro *dwFlags* da estrutura DBCOLUMNINFO. <br />*ulColumnSize* membro de DBCOLUMNINFO é ~ 0.|  
  
 DBTYPE_NULL e DBTYPE_EMPTY podem ser associados aos parâmetros de entrada, mas não a parâmetros ou resultados de saída. Quando associado a parâmetros de entrada, o status deve ser definido como DBSTATUS_S_ISNULL para DBTYPE_NULL ou DBSTATUS_S_DEFAULT para DBTYPE_EMPTY. DBTYPE_BYREF não pode ser usado com DBTYPE_NULL ou DBTYPE_EMPTY.  
  
 DBTYPE_UDT também pode ser convertido em DBTYPE_EMPTY e DBTYPE_NULL. No entanto, DBTYPE_NULL e DBTYPE_EMPTY não podem ser convertidos em DBTYPE_UDT. Isso é consistente com DBTYPE_BYTES. **ISSCommandWithParameters** é usado para processar UDTs como parâmetros.  
  
 As conversões de dados fornecidas pelos serviços principais do OLE DB (**IDataConvert**) não são aplicáveis a DBTYPE_UDT.  
  
 As demais associações não têm suporte.  
  
## <a name="comparability-for-irowsetfind"></a>Comparações de IRowsetFind  
 Para os tipos UDT, apenas as seguintes comparações têm suporte:  
  
-   EQ  
  
-   NE  
  
-   IGNORE  
  
 Se qualquer outra comparação for tentada, DB_E_BADCOMPAREOP será retornado.  
  
## <a name="bcp-support-for-udts"></a>Suporte BCP para UDTs  
 Os valores UDT podem ser importados e exportados apenas como caractere ou valores binários.  
  
## <a name="down-level-client-behavior-for-udts"></a>Comportamento de cliente de nível inferior para UDTs  
 Os UDTs estão sujeitos ao mapeamento de tipo com clientes de baixo nível, conforme indicado a seguir:  
  
|Versão do cliente|DBTYPE_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|DBTYPE_UDT<br /><br /> (comprimento maior que 8.000 bytes)|  
|--------------------|------------------------------------------------------------------|---------------------------------------------------------|  
|SQL Server 2005|UDT|varbinary(max)|  
|SQL Server 2008 e posterior|UDT|UDT|  
  
 Quando **DataTypeCompatibility** (SSPROP_INIT_DATATYPECOMPATIBILITY) é definido como "80", os tipos UDT grandes são exibidos para os clientes da mesma forma que para clientes de nível inferior.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados CLR grandes definidos pelo usuário](../../oledb/features/large-clr-user-defined-types.md)  
  
  

