---
title: Metadados de parâmetro com valor de tabela adicionais | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7a83df9dde4ada571b0fc39f6ac8e45c49d9ac17
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73777902"
---
# <a name="additional-table-valued-parameter-metadata"></a>Metadados adicionais de parâmetros com valor de tabela
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para recuperar metadados para um parâmetro com valor de tabela, um aplicativo chama SQLProcedureColumns. Para um parâmetro com valor de tabela, SQLProcedureColumns retorna uma única linha. Duas colunas adicionais específicas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME, foram adicionadas para fornecer informações de esquema e de catálogo para tipos de tabela associados a parâmetros com valor de tabela. Em conformidade com a especificação ODBC, SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME aparecem antes de todas as colunas específicas do driver adicionadas em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e depois de todas as colunas exigidas pelo próprio ODBC.  
  
 A tabela a seguir lista as colunas significativas para parâmetros com valor de tabela.  
  
|Nome da coluna|Tipo de dados|Valor/comentários|  
|-----------------|---------------|---------------------|  
|DATA_TYPE|Smallint não NULL|SQL_SS_TABLE|  
|TYPE_NAME|WVarchar(128) não NULL|O nome do tipo do parâmetro com valor de tabela.|  
|COLUMN_SIZE|Integer|NULL|  
|BUFFER_LENGTH|Integer|0|  
|DECIMAL_DIGITS|Smallint|NULL|  
|NUM_PREC_RADIX|Smallint|NULL|  
|NULLABLE|Smallint não NULL|SQL_NULLABLE|  
|REMARKS|Varchar|NULL|  
|COLUMN_DEF|WVarchar(4000)|NULL|  
|SQL_DATA_TYPE|Smallint não NULL|SQL_SS_TABLE|  
|SQL_DATETIME_SUB|Smallint|NULL|  
|CHAR_OCTET_LENGTH|Integer|NULL|  
|ORDINAL_POSITION|Integer não NULL|A posição ordinal do parâmetro.|  
|IS_NULLABLE|Varchar|"YES"|  
|SS_TYPE_CATALOG_NAME|WVarchar(128) não NULL|O catálogo que contém a definição de tipo do tipo de tabela do parâmetro com valor de tabela.|  
|SS_TYPE_SCHEMA_NAME|WVarchar(128) não NULL|O esquema que contém a definição de tipo do tipo de tabela do parâmetro com valor de tabela.|  
  
 As colunas WVarchar são definidas como Varchar na especificação de ODBC, mas são retornadas de fato como WVarchar em todos os drivers ODBC recentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta alteração foi feita quando o suporte a Unicode foi adicionado à especificação de ODBC 3.5, mas não chamado explicitamente.  
  
 Para obter metadados adicionais para parâmetros com valor de tabela, um aplicativo usa as funções de catálogo SQLColumns e SQLPrimaryKeys. Antes de essas funções serem chamadas para parâmetros com valor de tabela, o aplicativo deve definir o atributo de instrução SQL_SOPT_SS_NAME_SCOPE como SQL_SS_NAME_SCOPE_TABLE_TYPE. Esse valor indica que o aplicativo exige metadados para um tipo de tabela em lugar de uma tabela real. Em seguida, o aplicativo passa a TYPE_NAME do parâmetro com valor de tabela como o parâmetro *TableName* . SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME são usados com os parâmetros *CatalogName* e *SchemaName* , respectivamente, para identificar o catálogo e o esquema para o parâmetro com valor de tabela. Quando um aplicativo concluir a recuperação de metadados para parâmetros com valor de tabela, ele deve definir SQL_SOPT_SS_NAME_SCOPE novamente com seu valor padrão SQL_SS_NAME_SCOPE_TABLE.  
  
 Quando SQL_SOPT_SS_NAME_SCOPE for definido como SQL_SS_NAME_SCOPE_TABLE, as consultas a servidores vinculados irão falhar. As chamadas para SQLColumns ou SQLPrimaryKeys com um catálogo que contém um componente de servidor falharão.  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros &#40;com valor de tabela ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
