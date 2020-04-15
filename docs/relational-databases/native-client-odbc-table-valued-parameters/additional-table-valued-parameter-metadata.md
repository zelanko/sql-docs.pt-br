---
title: Metadados adicionais de parâmetros avaliados em tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), catalog functions to retrieve metadata
- table-valued parameters (ODBC), metadata
ms.assetid: 6c193188-5185-4373-9a0d-76cfc150c828
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6b52f83e36c315ccd86d1516df9e11b913c80ba8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304520"
---
# <a name="additional-table-valued-parameter-metadata"></a>Metadados adicionais de parâmetros com valor de tabela
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para recuperar metadados para um parâmetro avaliado em tabela, um aplicativo chama SQLProcedureColumns. Para um parâmetro avaliado em tabela, SQLProcedureColumns retorna uma única linha. Duas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]colunas específicas adicionais, SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME, foram adicionadas para fornecer informações de esquema e catálogo para tipos de tabela associados a parâmetros de valor de tabela. Em conformidade com a especificação ODBC, SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME aparecem antes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]todas as colunas específicas do driver adicionadas em versões anteriores de , e depois de todas as colunas exigidas pelo próprio ODBC.  
  
 A tabela a seguir lista as colunas significativas para parâmetros com valor de tabela.  
  
|Nome da coluna|Tipo de dados|Valor/comentários|  
|-----------------|---------------|---------------------|  
|DATA_TYPE|Smallint não NULL|SQL_SS_TABLE|  
|TYPE_NAME|WVarchar(128) não NULL|O nome do tipo do parâmetro com valor de tabela.|  
|COLUMN_SIZE|Integer|NULO|  
|BUFFER_LENGTH|Integer|0|  
|DECIMAL_DIGITS|Smallint|NULO|  
|NUM_PREC_RADIX|Smallint|NULO|  
|NULLABLE|Smallint não NULL|SQL_NULLABLE|  
|COMENTÁRIOS|Varchar|NULO|  
|COLUMN_DEF|WVarchar(4000)|NULO|  
|SQL_DATA_TYPE|Smallint não NULL|SQL_SS_TABLE|  
|SQL_DATETIME_SUB|Smallint|NULO|  
|CHAR_OCTET_LENGTH|Integer|NULO|  
|ORDINAL_POSITION|Integer não NULL|A posição ordinal do parâmetro.|  
|IS_NULLABLE|Varchar|"YES"|  
|SS_TYPE_CATALOG_NAME|WVarchar(128) não NULL|O catálogo que contém a definição de tipo do tipo de tabela do parâmetro com valor de tabela.|  
|SS_TYPE_SCHEMA_NAME|WVarchar(128) não NULL|O esquema que contém a definição de tipo do tipo de tabela do parâmetro com valor de tabela.|  
  
 As colunas WVarchar são definidas como Varchar na especificação de ODBC, mas são retornadas de fato como WVarchar em todos os drivers ODBC recentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta alteração foi feita quando o suporte a Unicode foi adicionado à especificação de ODBC 3.5, mas não chamado explicitamente.  
  
 Para obter metadados adicionais para parâmetros de valor de tabela, um aplicativo usa as funções de catálogo SQLColumns e SQLPrimaryKeys. Antes de essas funções serem chamadas para parâmetros com valor de tabela, o aplicativo deve definir o atributo de instrução SQL_SOPT_SS_NAME_SCOPE como SQL_SS_NAME_SCOPE_TABLE_TYPE. Esse valor indica que o aplicativo exige metadados para um tipo de tabela em lugar de uma tabela real. Em seguida, o aplicativo passa o TYPE_NAME do parâmetro avaliado em tabela como parâmetro *TableName.* SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME são usados com os parâmetros *CatalogName* e *SchemaName,* respectivamente, para identificar o catálogo e o esquema para o parâmetro avaliado em tabela. Quando um aplicativo concluir a recuperação de metadados para parâmetros com valor de tabela, ele deve definir SQL_SOPT_SS_NAME_SCOPE novamente com seu valor padrão SQL_SS_NAME_SCOPE_TABLE.  
  
 Quando SQL_SOPT_SS_NAME_SCOPE for definido como SQL_SS_NAME_SCOPE_TABLE, as consultas a servidores vinculados irão falhar. Chamadas para SQLColumns ou SQLPrimaryKeys com um catálogo que contém um componente de servidor falharão.  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros avaliados em tabela &#40;&#41;o ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
