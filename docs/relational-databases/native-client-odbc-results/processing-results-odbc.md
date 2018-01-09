---
title: Processando resultados (ODBC) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-results
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2c73a96fec76119cbe1739a1752e22e7acee25f5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="processing-results-odbc"></a>Processando resultados (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Depois que um aplicativo envia uma instrução SQL, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna qualquer dado resultante como um ou mais conjuntos de resultados. Um conjunto de resultados é um conjunto de linhas e colunas que correspondem aos critérios da consulta. As instruções SELECT, funções de catálogo e alguns procedimentos armazenados geram um conjunto de resultados disponibilizado para um aplicativo no formato tabular. Se a instrução SQL executada for um procedimento armazenado, um lote contendo vários comandos ou uma instrução SELECT contendo palavras-chave, haverá vários conjuntos de resultados a serem processados.  
  
 As funções de catálogo ODBC também podem recuperar dados. Por exemplo, [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md) recupera dados de colunas na fonte de dados. Esses conjuntos de resultados podem conter zero ou mais linhas.  
  
 Outras instruções SQL, como GRANT ou REVOKE, não retornam conjuntos de resultados. Para essas instruções, código de retorno de **SQLExecute** ou **SQLExecDirect** geralmente é a única indicação a instrução foi bem-sucedida.  
  
 Cada instrução INSERT, UPDATE e DELETE retorna um conjunto de resultados que contém apenas o número de linhas afetado pela modificação. Essa contagem fica disponível quando o aplicativo chama [SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md). ODBC 3. *x* aplicativos devem chamar **SQLRowCount** para recuperar o resultado do conjunto ou [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) para cancelá-la. Quando um aplicativo executa um lote ou procedimento armazenado que contém várias instruções INSERT, UPDATE ou DELETE, o conjunto de resultados de cada instrução de modificação deve ser processado usando **SQLRowCount** ou cancelada usando **SQLMoreResults**. Essas contagens podem ser canceladas incluindo uma instrução SET NOCOUNT ON no lote ou no procedimento armazenado.  
  
 O Transact-SQL inclui a instrução SET NOCOUNT. Quando a opção NOCOUNT está ativada, o SQL Server não retorna as contagens de linhas afetadas por uma instrução e **SQLRowCount** retornará 0. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão do driver ODBC do Native Client apresenta um driver específico [SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) opção SQL_SOPT_SS_NOCOUNT_STATUS, para relatar se a opção NOCOUNT está ativada ou desativada. A qualquer momento **SQLRowCount** retornar 0, o aplicativo deverá testar SQL_SOPT_SS_NOCOUNT_STATUS. Se SQL_NC_ON for retornado, o valor 0 de **SQLRowCount** só indica que o SQL Server não retornou uma contagem de linhas. Se SQL_NC_OFF for retornado, isso significa que NOCOUNT está desativado e o valor 0 de **SQLRowCount** indica que a instrução não afetou nenhuma linha. Aplicativos não deverão exibir o valor de **SQLRowCount** quando SQL_SOPT_SS_NOCOUNT_STATUS for SQL_NC_OFF. Lotes ou procedimentos armazenados grandes podem conter várias instruções SET NOCOUNT, de forma que os programadores não podem supor que SQL_SOPT_SS_NOCOUNT_STATUS permaneça constante. A opção deve ser testada sempre **SQLRowCount** retornará 0.  
  
 Várias outras instruções Transact-SQL retornam seus dados em mensagens e não em conjuntos de resultados. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client recebe essas mensagens, ele retornará SQL_SUCCESS_WITH_INFO para informar o aplicativo que mensagens informativas estão disponíveis. O aplicativo pode chamar **SQLGetDiagRec** para recuperar essas mensagens. As instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que funcionam deste modo são as seguintes:  
  
-   DBCC  
  
-   SET SHOWPLAN (disponível com versões anteriores do SQL Server)  
  
-   SET STATISTICS  
  
-   PRINT  
  
-   RAISERROR  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client retornará SQL_ERROR em um RAISERROR com severidade de 11 ou superior. Se a severidade do RAISERROR for 19 ou superior, a conexão também será descartada.  
  
 Para processar os conjuntos de resultados a partir de uma instrução SQL, o aplicativo:  
  
-   Determina as características do conjunto de resultados.  
  
-   Associa as colunas às variáveis do programa.  
  
-   Recupera um único valor, uma linha inteira de valores ou várias linhas de valores.  
  
-   Testa se há mais conjuntos de resultados e, se houver, faz loops de volta para determinar as características do novo conjunto de resultados.  
  
 O processo de recuperação de linhas da fonte de dados e de seu retorno ao aplicativo é chamado de busca.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Determinar as características de um conjunto de resultados &#40; ODBC &#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
-   [Atribuindo armazenamento](../../relational-databases/native-client-odbc-results/assigning-storage.md)  
  
-   [Buscando dados de resultados](../../relational-databases/native-client-odbc-results/fetching-result-data.md)  
  
-   [Mapeamento de tipos de dados &#40; ODBC &#41;](../../relational-databases/native-client-odbc-results/mapping-data-types-odbc.md)  
  
-   [Uso do tipo de dados](../../relational-databases/native-client-odbc-results/data-type-usage.md)  
  
-   [Tradução automática de dados de caracteres](../../relational-databases/native-client-odbc-results/autotranslation-of-character-data.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Cliente nativo do SQL Server &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [Tópicos de instruções de resultados do processamento &#40; ODBC &#41;](http://msdn.microsoft.com/library/772d9064-c91d-4cac-8b60-fcc16bf76e10)  
  
  
