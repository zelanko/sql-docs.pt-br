---
description: SQLBindParameter
title: SQLBindParameter | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBindParameter function
ms.assetid: c302c87a-e7f4-4d2b-a0a7-de42210174ac
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aef702d89da9a4277fcc01bddc619eab5878ba6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428368"
---
# <a name="sqlbindparameter"></a>SQLBindParameter
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O**SQLBindParameter** pode eliminar o peso da conversão de dados quando usado para fornecer dados para o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, o que resulta em ganhos de desempenho significativos para os componentes de cliente e servidor dos aplicativos. Entre os outros benefícios está a menor perda de precisão ao inserir ou atualizar tipos de dados numéricos aproximados.  
  
> [!NOTE]  
>  Ao inserir dados de tipos **char** e **wchar** em uma coluna de imagem, é usado o tamanho dos dados sendo passados, e não o tamanho dos dados após a conversão em formato binário.  
  
 Se o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client encontrar um erro em um único elemento de uma matriz de parâmetros, o driver continuará executando a instrução para os elementos restantes. Se o aplicativo tiver associado uma matriz de elementos de status de parâmetro para a instrução, as linhas dos parâmetros que geram erros poderão ser determinadas a partir da matriz.  
  
 Ao usar o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, especifique SQL_PARAM_INPUT ao associar parâmetros de entrada. Só especifique SQL_PARAM_OUTPUT ou SQL_PARAM_INPUT_OUTPUT ao associar parâmetros de procedimento armazenado definidos com a palavra-chave OUTPUT.  
  
 [SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md) não será confiável com o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se um elemento de uma matriz de parâmetro associado causar erro na execução da instrução. O atributo da instrução ODBC – SQL_ATTR_PARAMS_PROCESSED_PTR – informa o número de linhas processadas antes da ocorrência do erro. O aplicativo pode atravessar sua matriz de status de parâmetro para descobrir o número de instruções executadas com êxito, se necessário.  
  
## <a name="binding-parameters-for-sql-character-types"></a>Associando parâmetros para tipos de caractere SQL  
 Se o tipo de dados SQL passado for um tipo de caractere, *ColumnSize* será o tamanho em caracteres (não em bytes). Se o comprimento da cadeia de dados em bytes for maior que 8000, *ColumnSize* deverá ser definido como **SQL_SS_LENGTH_UNLIMITED**, indicando que não há limite para o tamanho do tipo SQL.  
  
 Por exemplo, se o tipo de dados SQL for **SQL_WVARCHAR**, *ColumnSize* não deverá ser maior que 4000. Se o comprimento de dados real for maior que 4000, *ColumnSize* deverá ser definido como **SQL_SS_LENGTH_UNLIMITED** , de modo que **nvarchar(max)** será usado pelo driver.  
  
## <a name="sqlbindparameter-and-table-valued-parameters"></a>SQLBindParameter e parâmetros com valor de tabela  
 Assim como outros tipos de parâmetro, os parâmetros com valor de tabela são associados por SQLBindParameter.  
  
 Depois que um parâmetro com valor de tabela é associado, suas colunas também são associadas. Para associar as colunas, chame [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para definir SQL_SOPT_SS_PARAM_FOCUS como o ordinal do parâmetro com valor de tabela. Em seguida, chame SQLBindParameter para cada coluna no parâmetro com valor de tabela. Para voltar às associações de parâmetro de nível superior, defina SQL_SOPT_SS_PARAM_FOCUS como 0.  
  
 Para obter informações sobre como mapear parâmetros para campos de descritor para parâmetros com valor de tabela, consulte [Binding and transferência de dados of table-valued Parameters and Column Values](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlbindparameter-support-for-enhanced-date-and-time-features"></a>Suporte de SQLBindParameter a recursos aprimorados de data e hora  
 Os valores de parâmetro dos tipos de data/hora são convertidos conforme descrito em [conversões de C para SQL](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md). Observe que parâmetros de tipo **time** e **datetimeoffset** precisam ter *ValueType* especificado como **SQL_C_DEFAULT** ou **SQL_C_BINARY** quando são usadas suas estruturas correspondentes (**SQL_SS_TIME2_STRUCT** e **SQL_SS_TIMESTAMPOFFSET_STRUCT**).  
  
 Para obter mais informações, consulte [melhorias de data e hora &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlbindparameter-support-for-large-clr-udts"></a>Suporte de SQLBindParameter a UDTs CLR grandes  
 O**SQLBindParameter** suporta UDTs (tipos de dados definidos pelo usuário) CLR grandes. Para obter mais informações, consulte [tipos CLR grandes definidos pelo usuário &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Detalhes de implementação da API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [Função SQLBindParameter](https://go.microsoft.com/fwlink/?LinkId=59328)  
  
  
