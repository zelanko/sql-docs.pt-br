---
title: Tipos de CLR grandes definidos pelo usuário (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC, large user-defined types
- large user-defined types [ODBC]
ms.assetid: ddce337e-bb6e-4a30-b7cc-4969bb1520a9
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: ac70196d3b343a0f5a4fedbbedb2367a80665abb
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39565790"
---
# <a name="large-clr-user-defined-types-odbc"></a>Tipos de dados CLR grandes definidos pelo usuário (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Este tópico aborda as alterações feitas ao ODBC no SQL Server Native Client para dar suporte aos UDTs (tipos definidos pelo usuário) de CLR (Common Language Runtime) grande.  
  
 Para obter um exemplo que mostra o suporte a ODBC para UDTs grandes do CLR, consulte [dar suporte a UDTs grandes](../../../relational-databases/native-client-odbc-how-to/support-for-large-udts.md).  
  
 Para obter mais informações sobre o suporte para UDTs grandes do CLR no SQL Server Native Client, consulte [Large CLR User-Defined tipos](../../../relational-databases/native-client/features/large-clr-user-defined-types.md).  
  
## <a name="data-format"></a>Formato de Dados  
 O SQL Server Native Client usa SQL_SS_LENGTH_UNLIMITED para indicar que o tamanho de uma coluna é maior que 8.000 bytes para tipos LOB. A partir do SQL Server 2008, o mesmo valor é usado para UDTs do CLR quando seu tamanho for maior que 8.000 bytes.  
  
 Os valores UDT são representados como matrizes de bytes. Há suporte para conversões de cadeias hexadecimais e para cadeias hexadecimais. Os valores literais são representados como cadeias de caracteres hexadecimais com um prefixo "0x".  
  
 A seguinte tabela mostra o mapeamento de tipos de dados em parâmetros e conjuntos de resultados:  
  
|Tipo de dados do SQL Server|Tipo de dados SQL|Valor|  
|--------------------------|-------------------|-----------|  
|CLR UDT|SQL_SS_UDT|-151 (sqlncli.h)|  
  
 A seguinte tabela discute a estrutura correspondente e o tipo do C do ODBC. Essencialmente, UDT do CLR é um **varbinary** tipo com metadados adicionais.  
  
|Tipo de dados SQL|Layout de memória|Tipos de dados do C|Valor (sqlext.h)|  
|-------------------|-------------------|-----------------|------------------------|  
|SQL_SS_UDT|SQLCHAR * (unsigned char \*)|SQL_C_BINARY|SQL_BINARY (-2)|  
  
## <a name="descriptor-fields-for-parameters"></a>Campos do descritor dos parâmetros  
 As informações são retornadas nos campos IPD são as seguintes:  
  
|Campo do descritor|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|  
|----------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_LOCAL_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_SCALE|0|0|  
|SQL_DESC_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|  
|SQL_CA_SS_UDT_CATALOG_NAME|O nome do catálogo que contém o UDT.|O nome do catálogo que contém o UDT.|  
|SQL_CA_SS_UDT_SCHEMA_NAME|O nome do esquema que contém o UDT.|O nome do esquema de contém o UDT.|  
|SQL_CA_SS_UDT_TYPE_NAME|O nome do UDT.|O nome do UDT.|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|O nome totalmente qualificado do assembly do UDT.|O nome totalmente qualificado do assembly do UDT.|  
  
 Para parâmetros de UDT, SQL_CA_SS_UDT_TYPE_NAME deve sempre ser definida **SQLSetDescField**. SQL_CA_SS_UDT_CATALOG_NAME e SQL_CA_SS_UDT_SCHEMA_NAME são opcionais.  
  
 Se o UDT for definido no mesmo banco de dados com um esquema diferente que a tabela, SQL_CA_SS_UDT_SCHEMA_NAME deve ser definido.  
  
 Se o UDT for definido em um banco de dados diferente da tabela, SQL_CA_SS_UDT_CATALOG_NAME e SQL_CA_SS_UDT_SCHEMA_NAME devem ser definidos.  
  
 Se houver quaisquer erros ou omissões nas definições de SQL_CA_SS_UDT_TYPE_NAME, SQL_CA_SS_UDT_CATALOG_NAME ou SQL_CA_SS_UDT_SCHEMA_NAME, é gerado um registro de diagnóstico com SQLSTATE HY000 e texto de mensagem específico do servidor.  
  
## <a name="descriptor-fields-for-results"></a>Campos do descritor dos resultados  
 As informações retornadas nos campos IRD são as seguintes:  
  
|Campo do descritor|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|  
|----------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_DISPLAY_SIZE|2*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_LITERAL_PREFIX|"0x"|"0x"|  
|SQL_DESC_LITERAL_SUFFIX|""|""|  
|SQL_DESC_LOCAL_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_PRECISION|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SQL_DESC_SCALE|0|0|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|SQL_PRED_NONE|  
|SQL_DESC_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DESC_TYPE_NAME|"udt"|"udt"|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|  
|SQL_CA_SS_UDT_CATALOG_NAME|O nome do catálogo que contém o UDT.|O nome do catálogo que contém o UDT.|  
|SQL_CA_SS_UDT_SCHEMA_NAME|O nome do esquema que contém o UDT.|O nome do esquema que contém o UDT.|  
|SQL_CA_SS_UDT_TYPE_NAME|O nome do UDT.|O nome do UDT.|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|O nome totalmente qualificado do assembly do UDT.|O nome totalmente qualificado do assembly do UDT.|  
  
## <a name="column-metadata-returned-by-sqlcolumns-and-sqlprocedurecolumns-catalog-metadata"></a>Metadados de coluna retornados por SQLColumns e SQLProcedureColumns (metadados de catálogo)  
 Os seguintes valores de coluna são retornados para UDTs:  
  
|Nome da coluna|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|  
|-----------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|DATA_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|TYPE_NAME|O nome do UDT.|O nome do UDT.|  
|COLUMN_SIZE|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|BUFFER_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|DECIMAL_DIGITS|NULL|NULL|  
|SQL_DATA_TYPE|SQL_SS_UDT|SQL_SS_UDT|  
|SQL_DATETIME_SUB|NULL|NULL|  
|CHAR_OCTET_LENGTH|*n*|SQL_SS_LENGTH_UNLIMITED (0)|  
|SS_UDT_CATALOG_NAME|O nome do catálogo que contém o UDT.|O nome do catálogo que contém o UDT.|  
|SS_UDT_SCHEMA_NAME|O nome do esquema que contém o UDT.|O nome do esquema que contém o UDT.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|O nome totalmente qualificado do assembly do UDT.|O nome totalmente qualificado do assembly do UDT.|  
  
 As últimas três colunas são específicas do driver. Elas são adicionadas depois de quaisquer colunas definidas pelo ODBC, mas antes de quaisquer colunas específicas de driver existentes do conjunto de resultados de SQLColumns ou SQLProcedureColumns.  
  
 Nenhuma linha é retornada por SQLGetTypeInfo, para UDTs individuais ou para o tipo genérico "udt".  
  
## <a name="bindings-and-conversions"></a>Associações e conversões  
 As conversões de tipos de dados de C para SQL com suporte são as seguintes:  
  
|Conversão para e de:|SQL_SS_UDT|  
|-----------------------------|------------------|  
|SQL_C_WCHAR|Suporte para *|  
|SQL_C_BINARY|Tem suporte|  
|SQL_C_CHAR|Suporte para *|  
  
 \* Dados binários são convertidos em uma cadeia de caracteres hexadecimal.  
  
 As conversões com suporte dos tipos de dados do C para SQL são as seguintes:  
  
|Conversão para e de:|SQL_SS_UDT|  
|-----------------------------|------------------|  
|SQL_C_WCHAR|Suporte para *|  
|SQL_C_BINARY|Tem suporte|  
|SQL_C_CHAR|Suporte para *|  
  
 \* Ocorre a cadeia de caracteres hexadecimal para a conversão de dados binários.  
  
## <a name="sqlvariant-support-for-udts"></a>Suporte SQL_VARIANT para UDTs  
 Não há suporte para UDTs em colunas de SQL_VARIANT.  
  
## <a name="bcp-support-for-udts"></a>Suporte BCP para UDTs  
 Valores de UDTs podem ser importados e exportados somente como valores de caracteres ou binários.  
  
## <a name="downlevel-client-behavior-for-udts"></a>Comportamento do cliente de baixo nível para UDTs  
 Os UDTs estão sujeitos ao mapeamento de tipo com clientes de baixo nível, conforme indicado a seguir:  
  
|Versão do servidor __|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|  
|--------------------|-------------------------------------------------------------------|----------------------------------------------------------|  
|SQL Server 2005|**UDT**|**varbinary(max)**|  
|SQL Server 2008 e posterior|**UDT**|**UDT**|  
  
## <a name="odbc-functions-supporting-large-clr-udts"></a>Funções ODBC que dão suporte a UDTs de CLR grande  
 Esta seção discute as alterações feitas nas funções ODBC do SQL Server Native Client para dar suporte a UDTs de CLR grande.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 Valores de colunas de resultado UDT são convertidos de tipos de dados SQL para C, conforme descrito na seção "Associações e conversões", anteriormente neste tópico.  
  
### <a name="sqlbindparameter"></a>SQLBindParameter  
 Os valores necessários para UDTs são os seguintes:  
  
|Tipo de dados SQL|*ParameterType*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|---------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 Os valores retornados para UDTs são os descritos na seção "Campos do descritor dos resultados", anteriormente neste tópico.  
  
### <a name="sqlcolumns"></a>SQLColumns  
 Os valores retornados para UDTs são conforme descrito na seção "Retornou de metadados de coluna por SQLColumns e SQLProcedureColumns (metadados de catálogo)", neste tópico.  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 Os valores retornados para UDTs são os seguintes:  
  
|Tipo de dados SQL|*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|-------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqldescribeparam"></a>SQLDescribeParam  
 Os valores retornados para UDTs são os seguintes:  
  
|Tipo de dados SQL|*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-------------------|-------------------|---------------------|------------------------|  
|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT|*n*|0|  
|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|SQL_SS_UDT|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlfetch"></a>SQLFetch  
 Valores de colunas de resultado UDT são convertidos de tipos de dados SQL para C, conforme descrito na seção "Associações e conversões", anteriormente neste tópico.  
  
### <a name="sqlfetchscroll"></a>SQLFetchScroll  
 Valores de colunas de resultado UDT são convertidos de tipos de dados SQL para C, conforme descrito na seção "Associações e conversões", anteriormente neste tópico.  
  
### <a name="sqlgetdata"></a>SQLGetData  
 Valores de colunas de resultado UDT são convertidos de tipos de dados SQL para C, conforme descrito na seção "Associações e conversões", anteriormente neste tópico.  
  
### <a name="sqlgetdescfield"></a>SQLGetDescField  
 Os campos de descritor disponíveis como os novos tipos são descritos nas seções "Campos do descritor dos parâmetros" e "Campos do descritor dos resultados", anteriormente neste tópico.  
  
### <a name="sqlgetdescrec"></a>SQLGetDescRec  
 Os valores retornados para UDTs são os seguintes:  
  
|Tipo de dados SQL|Tipo|Subtipo|Comprimento|Precisão|Escala|  
|-------------------|----------|-------------|------------|---------------|-----------|  
|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT|0|*n*|n|0|  
|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|SQL_SS_UDT|0|SQL_SS_LENGTH_UNLIMITED (0)|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlgettypeinfo"></a>SQLGetTypeInfo  
 Os valores retornados para UDTs são os descritos na seção "Metadados de coluna retornados por SQLColumns e SQLProcedureColumns (metadados de catálogo)", anteriormente neste tópico.  
  
### <a name="sqlprocedurecolumns"></a>SQLProcedureColumns  
 Os valores retornados para UDTs são os descritos na seção "Metadados de coluna retornados por SQLColumns e SQLProcedureColumns (metadados de catálogo)", anteriormente neste tópico.  
  
### <a name="sqlputdata"></a>SQLPutData  
 Valores de parâmetros UDT são convertidos de tipos de dados de C para SQL, conforme descrito na seção "Associações e conversões", anteriormente neste tópico.  
  
### <a name="sqlsetdescfield"></a>SQLSetDescField  
 Campo de descritor disponível com os novos tipos são descritos nas seções "Campos do descritor dos resultados", neste tópico e "Campos de descritor para parâmetros".  
  
### <a name="sqlsetdescrec"></a>SQLSetDescRec  
 Os valores permitidos para UDTs são os seguintes:  
  
|Tipo de dados SQL|Tipo|Subtipo|Comprimento|Precisão|Escala|  
|-------------------|----------|-------------|------------|---------------|-----------|  
|SQL_SS_UDT<br /><br /> (comprimento inferior ou igual a 8.000 bytes)|SQL_SS_UDT|0|*n*|*n*|0|  
|SQL_SS_UDT<br /><br /> (comprimento maior que 8.000 bytes)|SQL_SS_UDT|0|SQL_SS_LENGTH_UNLIMITED (0)|SQL_SS_LENGTH_UNLIMITED (0)|0|  
  
### <a name="sqlspecialcolumns"></a>SQLSpecialColumns  
 Os valores retornados para os UDTs das colunas DATA_TYPE, TYPE_NAME, COLUMN_SIZE, BUFFER_LENGTH e DECIMAL_DIGITS são os descritos na seção "Metadados de coluna retornados por SQLColumns e SQLProcedureColumns (metadados de catálogo)", anteriormente neste tópico.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados CLR grandes definidos pelo usuário](../../../relational-databases/native-client/features/large-clr-user-defined-types.md)  
  
  
