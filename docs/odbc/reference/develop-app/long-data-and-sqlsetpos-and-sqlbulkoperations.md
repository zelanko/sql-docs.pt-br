---
title: Dados Long e SQLSetPos e SQLBulkOperations | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- long data [ODBC]
- SQLSetPos function [ODBC], long data and SQLBulkOperations
- data updates [ODBC], long data
- updating data [ODBC], long data
- SQLBulkOperations function [ODBC], long data
ms.assetid: e2fdf842-5e4c-46ca-bb21-4625c3324f28
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 308e1ad6f2d99a0a6b7e73d8a82ac62362fea9a2
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Dados Long e SQLSetPos e SQLBulkOperations
Como é o caso com parâmetros em instruções SQL, os dados longos podem ser enviados quando atualizando linhas com **SQLBulkOperations** ou **SQLSetPos** ou ao inserir linhas com **SQLBulkOperations**. Os dados são enviados em partes, com várias chamadas para **SQLPutData**. Colunas para o qual os dados são enviados em tempo de execução são conhecidas como *colunas de dados em execução*.  
  
> [!NOTE]  
>  Um aplicativo pode enviar qualquer tipo de dados em tempo de execução com **SQLPutData**, embora apenas caracteres e dados binários podem ser enviados em partes. No entanto, se os dados são pequenos o suficiente para caber em um único buffer, há geralmente não há motivo para usar **SQLPutData**. É muito mais fácil associar o buffer e permitir que o driver recupera os dados do buffer.  
  
 Como as colunas de dados long normalmente não são associadas, o aplicativo deve associar a coluna antes de chamar **SQLBulkOperations** ou **SQLSetPos** e desvincule-depois de chamar **SQLBulkOperations**  ou **SQLSetPos**. A coluna deve ser vinculada porque **SQLBulkOperations** ou **SQLSetPos** funciona apenas em colunas associadas e deve ser desligado para que **SQLGetData** pode ser usado para recuperar dados de uma coluna.  
  
 Para enviar dados em tempo de execução, o aplicativo faz o seguinte:  
  
1.  Coloca um valor de 32 bits no buffer de linhas em vez de um valor de dados. Esse valor será retornado para o aplicativo mais tarde, portanto, o aplicativo deve definir como um valor significativo, como o número da coluna ou o identificador de um arquivo que contém dados.  
  
2.  Define o valor no buffer de comprimento/indicador para o resultado do SQL_LEN_DATA_AT_EXEC (*comprimento*) macro. Esse valor indica ao driver que serão enviados com os dados para o parâmetro **SQLPutData**. O *comprimento* valor é usado ao enviar dados longos para uma fonte de dados que precisa saber quantos bytes de dados long serão enviados para que ele pode alocar espaço. Para determinar se uma fonte de dados exige que esse valor, o aplicativo chama **SQLGetInfo** com a opção SQL_NEED_LONG_DATA_LEN. Todos os drivers devem dar suporte a esta macro; Se a fonte de dados não requer o comprimento em bytes, o driver pode ignorá-lo.  
  
3.  Chamadas **SQLBulkOperations** ou **SQLSetPos**. O driver detecta que um buffer de comprimento/indicador contém o resultado do SQL_LEN_DATA_AT_EXEC (*comprimento*) macro e retorna SQL_NEED_DATA como o valor de retorno da função.  
  
4.  Chamadas **SQLParamData** em resposta ao SQL_NEED_DATA o valor de retorno. Se os dados long precisam ser enviada, **SQLParamData** retornará SQL_NEED_DATA. No buffer apontado pelo *ValuePtrPtr* argumento, o driver retorna o valor exclusivo que o aplicativo é colocado no buffer de linhas. Se houver mais de uma coluna de dados em execução, o aplicativo usa esse valor para determinar qual coluna para enviar dados para; o driver não é necessário para solicitar dados para colunas de dados em execução em uma ordem específica.  
  
5.  Chamadas **SQLPutData** para enviar os dados da coluna para o driver. Se os dados da coluna não couberem em um único buffer, como normalmente é o caso de dados longo, o aplicativo chama **SQLPutData** repetidamente para enviar os dados em partes; depende da fonte de dados e o driver remontar os dados. Se o aplicativo passa os dados de cadeia de caracteres terminada em nulo, a driver ou fonte de dados deve remover o caractere null de terminação como parte do processo de remontagem.  
  
6.  Chamadas **SQLParamData** novamente para indicar que ela enviou todos os dados da coluna. Se houver qualquer coluna de dados em execução para o qual os dados não foram enviados, o driver retorna SQL_NEED_DATA e o valor exclusivo para a próxima coluna de dados em execução; o aplicativo retorna para a etapa 5. Se dados foram enviados para todas as colunas de dados em execução, os dados para a linha serão enviados para a fonte de dados. **SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO e pode retornar qualquer SQLSTATE **SQLBulkOperations** ou **SQLSetPos** pode retornar.  
  
 Depois de **SQLBulkOperations** ou **SQLSetPos** retorna SQL_NEED_DATA e antes de dados tem sido enviados completamente para a última coluna de dados em execução, a instrução está em um estado de dados necessário. Nesse estado, o aplicativo pode chamar somente **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**, ou **SQLGetDiagRec**; todas as outras funções retornam SQLSTATE HY010 (erro de sequência de função). Chamando **SQLCancel** cancela a execução da instrução e o retorna ao estado anterior. Para obter mais informações, consulte [tabelas de transição de estado do apêndice b: ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).

