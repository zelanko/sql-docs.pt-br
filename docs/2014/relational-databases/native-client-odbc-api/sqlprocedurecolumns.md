---
title: SQLProcedureColumns | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLProcedureColumns function
ms.assetid: 6671e180-0072-4de5-90f5-314306d2ba9c
author: rothja
ms.author: jroth
ms.openlocfilehash: 078e391bd39fdc49cde539c4004ed51d25eef93f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021917"
---
# <a name="sqlprocedurecolumns"></a>SQLProcedureColumns
  `SQLProcedureColumns`Retorna uma linha relatando os atributos de valor de retorno de todos os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedimentos armazenados.  
  
 `SQLProcedureColumns`retorna SQL_SUCCESS se os valores existem ou não para os parâmetros *CatalogName*, *schemas*, *ProcName*ou *ColumnName* . **SQLFetch** retorna SQL_NO_DATA quando são usados valores inválidos nesses parâmetros.  
  
 É possível executar `SQLProcedureColumns` em um cursor de servidor estático. Uma tentativa de executar `SQLProcedureColumns` em um cursor atualizável (dinâmico ou conjunto de chaves) retornará SQL_SUCCESS_WITH_INFO, indicando que o tipo de cursor foi alterado.  
  
 A tabela a seguir lista as colunas retornadas pelo conjunto de resultados e como elas foram estendidas para tratar os tipos de dados **udt** e **xml** por meio do driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client:  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|SS_UDT_CATALOG_NAME|Retorna o nome do catálogo que contém o UDT (tipo definido pelo usuário).|  
|SS_UDT_SCHEMA_NAME|Retorna o nome do esquema que contém o UDT.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|Retorna o nome qualificado do assembly do UDT.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|Retorna o nome do catálogo no qual é definido o nome de uma coleção de esquemas XML. Se não for possível localizar o nome do catálogo, essa variável conterá uma cadeia de caracteres vazia.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|Retorna o nome do esquema no qual é definido o nome de uma coleção de esquemas XML. Se não for possível localizar o nome do esquema, essa variável conterá uma cadeia de caracteres vazia.|  
|SS_XML_SCHEMACOLLECTION_NAME|Retorna o nome de uma coleção de esquemas XML. Se não for possível localizar o nome, essa variável conterá uma cadeia de caracteres vazia.|  
  
## <a name="sqlprocedurecolumns-and-table-valued-parameters"></a>SQLProcedureColumns e parâmetros com valor de tabela  
 SQLProcedureColumns manipula parâmetros com valor de tabela de maneira semelhante aos tipos CLR definidos pelo usuário. Em linhas retornadas para parâmetros com valor de tabela, as colunas têm os seguintes valores:  
  
|Nome da coluna|Descrição/valor|  
|-----------------|------------------------|  
|DATA_TYPE|SQL_SS_TABLE|  
|TYPE_NAME|O nome do tipo de tabela para o parâmetro com valor de tabela.|  
|COLUMN_SIZE|NULO|  
|BUFFER_LENGTH|0|  
|DECIMAL_DIGITS|O número de colunas no parâmetro com valor de tabela.|  
|NUM_PREC_RADIX|NULO|  
|NULLABLE|SQL_NULLABLE|  
|COMENTÁRIOS|NULO|  
|COLUMN_DEF|NULL. Os tipos de tabela não podem ter valores padrão.|  
|SQL_DATA_TYPE|SQL_SS_TABLE|  
|SQL_DATETIME_SUB|NULO|  
|CHAR_OCTET_LENGTH|NULO|  
|IS_NULLABLE|"YES"|  
|SS_TYPE_CATALOG_NAME|Retorna o nome do catálogo que contém a tabela ou o tipo CLR definido pelo usuário.|  
|SS_TYPE_SCHEMA_NAME|Retorna o nome do esquema que contém a tabela ou o tipo CLR definido pelo usuário.|  
  
 As colunas SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME estão disponíveis no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores para retornar o catálogo e o esquema, respectivamente, para parâmetros com valor de tabela. Essas colunas são preenchidas para parâmetros com valor de tabela e também para parâmetros de tipos CLR definidos pelo usuário. (As colunas de esquema e de catálogo existentes para parâmetros de tipos CLR definidos pelo usuário não são afetadas por esta funcionalidade adicional. Elas também são preenchidas para manter a compatibilidade com versões anteriores).  
  
 De acordo com a especificação de ODBC, SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME aparecem antes de todas as colunas específicas do driver adicionadas em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e depois de todas as colunas autorizadas pelo próprio ODBC.  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlprocedurecolumns-support-for-enhanced-date-and-time-features"></a>Suporte de SQLProcedureColumns a recursos aprimorados de data e hora  
 Para obter os valores retornados para tipos de data/hora, consulte [Catalog Metadata](../native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obter mais informações gerais, consulte [melhorias de data e hora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlprocedurecolumns-support-for-large-clr-udts"></a>Suporte de SQLProcedureColumns a UDTs CLR grandes  
 `SQLProcedureColumns` dá suporte a UDTs grandes do CLR. Para obter mais informações, consulte [tipos CLR grandes definidos pelo usuário &#40;&#41;ODBC ](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLProcedureColumns](https://go.microsoft.com/fwlink/?LinkId=59363)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
