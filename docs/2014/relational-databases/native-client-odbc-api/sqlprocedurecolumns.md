---
title: SQLProcedureColumns | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLProcedureColumns function
ms.assetid: 6671e180-0072-4de5-90f5-314306d2ba9c
caps.latest.revision: 50
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5b693d06e42f0fc5d2815b188826b21f5d89cae7
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37428385"
---
# <a name="sqlprocedurecolumns"></a>SQLProcedureColumns
  `SQLProcedureColumns` Retorna uma linha que relata os atributos de valor de retorno de todos os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedimentos armazenados.  
  
 `SQLProcedureColumns` Retorna SQL_SUCCESS havendo ou não valores para *CatalogName*, *SchemaName*, *ProcName*, ou *ColumnName* parâmetros. **SQLFetch** retorna SQL_NO_DATA quando são usados valores inválidos nesses parâmetros.  
  
 É possível executar `SQLProcedureColumns` em um cursor de servidor estático. Uma tentativa de executar `SQLProcedureColumns` em um cursor atualizável (dinâmico ou conjunto de chaves) retornará SQL_SUCCESS_WITH_INFO, indicando que o tipo de cursor foi alterado.  
  
 A tabela a seguir lista as colunas retornadas pelo conjunto de resultados e como elas foram estendidas para lidar com o **udt** e **xml** tipos de dados por meio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client:  
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|SS_UDT_CATALOG_NAME|Retorna o nome do catálogo que contém o UDT (tipo definido pelo usuário).|  
|SS_UDT_SCHEMA_NAME|Retorna o nome do esquema que contém o UDT.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|Retorna o nome qualificado do assembly do UDT.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|Retorna o nome do catálogo no qual é definido o nome de uma coleção de esquemas XML. Se não for possível localizar o nome do catálogo, essa variável conterá uma cadeia de caracteres vazia.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|Retorna o nome do esquema no qual é definido o nome de uma coleção de esquemas XML. Se não for possível localizar o nome do esquema, essa variável conterá uma cadeia de caracteres vazia.|  
|SS_XML_SCHEMACOLLECTION_NAME|Retorna o nome de uma coleção de esquemas XML. Se não for possível localizar o nome, essa variável conterá uma cadeia de caracteres vazia.|  
  
## <a name="sqlprocedurecolumns-and-table-valued-parameters"></a>SQLProcedureColumns e parâmetros com valor de tabela  
 SQLProcedureColumns lida com os parâmetros com valor de tabela de maneira semelhante para tipos CLR definidos pelo usuário. Em linhas retornadas para parâmetros com valor de tabela, as colunas têm os seguintes valores:  
  
|Nome da coluna|Descrição/valor|  
|-----------------|------------------------|  
|DATA_TYPE|SQL_SS_TABLE|  
|TYPE_NAME|O nome do tipo de tabela para o parâmetro com valor de tabela.|  
|COLUMN_SIZE|NULL|  
|BUFFER_LENGTH|0|  
|DECIMAL_DIGITS|O número de colunas no parâmetro com valor de tabela.|  
|NUM_PREC_RADIX|NULL|  
|NULLABLE|SQL_NULLABLE|  
|REMARKS|NULL|  
|COLUMN_DEF|NULL. Os tipos de tabela não podem ter valores padrão.|  
|SQL_DATA_TYPE|SQL_SS_TABLE|  
|SQL_DATETIME_SUB|NULL|  
|CHAR_OCTET_LENGTH|NULL|  
|IS_NULLABLE|"YES"|  
|SS_TYPE_CATALOG_NAME|Retorna o nome do catálogo que contém a tabela ou o tipo CLR definido pelo usuário.|  
|SS_TYPE_SCHEMA_NAME|Retorna o nome do esquema que contém a tabela ou o tipo CLR definido pelo usuário.|  
  
 As colunas SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME estão disponíveis no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores para retornar o catálogo e o esquema, respectivamente, para parâmetros com valor de tabela. Essas colunas são preenchidas para parâmetros com valor de tabela e também para parâmetros de tipos CLR definidos pelo usuário. (As colunas de esquema e de catálogo existentes para parâmetros de tipos CLR definidos pelo usuário não são afetadas por esta funcionalidade adicional. Elas também são preenchidas para manter a compatibilidade com versões anteriores).  
  
 De acordo com a especificação de ODBC, SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME aparecem antes de todas as colunas específicas do driver adicionadas em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e depois de todas as colunas autorizadas pelo próprio ODBC.  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlprocedurecolumns-support-for-enhanced-date-and-time-features"></a>Suporte de SQLProcedureColumns a recursos aprimorados de data e hora  
 Para os valores retornados para tipos de data/hora, consulte [metadados de catálogo](../native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obter mais informações, consulte [aprimoramentos de data e hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlprocedurecolumns-support-for-large-clr-udts"></a>Suporte de SQLProcedureColumns a UDTs CLR grandes  
 `SQLProcedureColumns` dá suporte a UDTs grandes do CLR. Para obter mais informações, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLProcedureColumns](http://go.microsoft.com/fwlink/?LinkId=59363)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
