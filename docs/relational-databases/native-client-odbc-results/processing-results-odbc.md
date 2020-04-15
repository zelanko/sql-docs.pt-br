---
title: Resultados de Processamento (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], about result sets
- SQLRowCount function
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- COMPUTE clause
- result sets [ODBC]
- COMPUTE BY clause
ms.assetid: 61a8db19-6571-47dd-84e8-fcc97cb60b45
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 39dafbb865ef951356bb01c4fd8f646bf943346b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304577"
---
# <a name="processing-results-odbc"></a>Processando resultados (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Depois que um aplicativo envia uma instrução SQL, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna qualquer dado resultante como um ou mais conjuntos de resultados. Um conjunto de resultados é um conjunto de linhas e colunas que correspondem aos critérios da consulta. As instruções SELECT, funções de catálogo e alguns procedimentos armazenados geram um conjunto de resultados disponibilizado para um aplicativo no formato tabular. Se a instrução SQL executada for um procedimento armazenado, um lote contendo vários comandos ou uma instrução SELECT contendo palavras-chave, haverá vários conjuntos de resultados a serem processados.  
  
 As funções de catálogo ODBC também podem recuperar dados. Por exemplo, [o SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md) recupera dados sobre colunas na fonte de dados. Esses conjuntos de resultados podem conter zero ou mais linhas.  
  
 Outras instruções SQL, como GRANT ou REVOKE, não retornam conjuntos de resultados. Para essas instruções, o código de retorno de **SQLExecute** ou **SQLExecDirect** é geralmente a única indicação de que a instrução foi bem sucedida.  
  
 Cada instrução INSERT, UPDATE e DELETE retorna um conjunto de resultados que contém apenas o número de linhas afetado pela modificação. Essa contagem é disponibilizada quando o aplicativo chama [SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md). ODBC 3. *os* aplicativos x devem ligar para **o SQLRowCount** para recuperar o conjunto de resultados ou [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) para cancelá-lo. Quando um aplicativo executa um procedimento em lote ou armazenado contendo várias instruções INSERT, UPDATE ou DELETE, o conjunto de resultados de cada instrução de modificação deve ser processado usando **SQLRowCount** ou cancelado usando **SQLMoreResults**. Essas contagens podem ser canceladas incluindo uma instrução SET NOCOUNT ON no lote ou no procedimento armazenado.  
  
 O Transact-SQL inclui a instrução SET NOCOUNT. Quando a opção NOCOUNT é definida, o SQL Server não retorna as contagens das linhas afetadas por uma declaração e **o SQLRowCount** retorna 0. A [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão do driver Native Client ODBC introduz uma opção [SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) específica para o driver, SQL_SOPT_SS_NOCOUNT_STATUS, para informar se a opção NOCOUNT está ativada ou desativada. Sempre que **o SQLRowCount** retornar 0, o aplicativo deve testar SQL_SOPT_SS_NOCOUNT_STATUS. Se SQL_NC_ON for devolvido, o valor de 0 do **SQLRowCount** indica apenas que o SQL Server não retornou uma contagem de linhas. Se SQL_NC_OFF for devolvida, significa que nocount está desligado e o valor de 0 do **SQLRowCount** indica que a declaração não afetou nenhuma linha. Os aplicativos não devem exibir o valor do **SQLRowCount** quando SQL_SOPT_SS_NOCOUNT_STATUS estiver SQL_NC_OFF. Lotes ou procedimentos armazenados grandes podem conter várias instruções SET NOCOUNT, de forma que os programadores não podem supor que SQL_SOPT_SS_NOCOUNT_STATUS permaneça constante. A opção deve ser testada cada vez **que O SQLRowCount** retornar 0.  
  
 Várias outras instruções Transact-SQL retornam seus dados em mensagens e não em conjuntos de resultados. Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o driver Cliente Nativo ODBC recebe essas mensagens, ele retorna SQL_SUCCESS_WITH_INFO para informar o aplicativo de que as mensagens informacionais estão disponíveis. O aplicativo pode então chamar **sqlGetDiagRec** para recuperar essas mensagens. As instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que funcionam deste modo são as seguintes:  
  
-   DBCC  
  
-   SET SHOWPLAN (disponível com versões anteriores do SQL Server)  
  
-   SET STATISTICS  
  
-   PRINT  
  
-   RAISERROR  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver Cliente Nativo ODBC retorna SQL_ERROR em um RAISERROR com uma gravidade de 11 ou mais. Se a severidade do RAISERROR for 19 ou superior, a conexão também será descartada.  
  
 Para processar os conjuntos de resultados a partir de uma instrução SQL, o aplicativo:  
  
-   Determina as características do conjunto de resultados.  
  
-   Associa as colunas às variáveis do programa.  
  
-   Recupera um único valor, uma linha inteira de valores ou várias linhas de valores.  
  
-   Testa se há mais conjuntos de resultados e, se houver, faz loops de volta para determinar as características do novo conjunto de resultados.  
  
 O processo de recuperação de linhas da fonte de dados e de seu retorno ao aplicativo é chamado de busca.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Determinando as características de um conjunto de resultados &#40;o&#41;da ODBC](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
-   [Atribuindo armazenamento](../../relational-databases/native-client-odbc-results/assigning-storage.md)  
  
-   [Buscando dados de resultados](../../relational-databases/native-client-odbc-results/fetching-result-data.md)  
  
-   [Mapeamento de tipos de dados &#40;&#41;da ODBC](../../relational-databases/native-client-odbc-results/mapping-data-types-odbc.md)  
  
-   [Uso do tipo de dados](../../relational-databases/native-client-odbc-results/data-type-usage.md)  
  
-   [Tradução automática de dados de caracteres](../../relational-databases/native-client-odbc-results/autotranslation-of-character-data.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Cliente nativo do servidor SQL &#40;&#41;ODBC](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [Processamento de resultados como fazer tópicos &#40;o&#41;da ODBC](https://msdn.microsoft.com/library/772d9064-c91d-4cac-8b60-fcc16bf76e10)  
  
  
