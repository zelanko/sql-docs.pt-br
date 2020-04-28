---
title: Long data e SQLSetPos e SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- SQLSetPos function [ODBC], long data and SQLBulkOperations
- data updates [ODBC], long data
- updating data [ODBC], long data
- SQLBulkOperations function [ODBC], long data
ms.assetid: e2fdf842-5e4c-46ca-bb21-4625c3324f28
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4bc6c5d2da2f796a7c312971635fc36bc2fae8af
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287860"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Dados Long e SQLSetPos e SQLBulkOperations
Como é o caso com parâmetros em instruções SQL, dados longos podem ser enviados ao atualizar linhas com **SQLBulkOperations** ou **SQLSetPos** ou ao inserir linhas com **SQLBulkOperations**. Os dados são enviados em partes, com várias chamadas para **SQLPutData**. As colunas para as quais os dados são enviados no momento da execução são conhecidas como *colunas de dados em execução*.  
  
> [!NOTE]  
>  Um aplicativo pode, na verdade, enviar qualquer tipo de dados no momento da execução com **SQLPutData**, embora apenas dados de caractere e binários possam ser enviados em partes. No entanto, se os dados forem pequenos o suficiente para caber em um único buffer, geralmente não há motivo para usar **SQLPutData**. É muito mais fácil associar o buffer e permitir que o driver recupere os dados do buffer.  
  
 Como as colunas de dados longas normalmente não são associadas, o aplicativo deve associar a coluna antes de chamar **SQLBulkOperations** ou **SQLSetPos** e desassociá-la após chamar **SQLBulkOperations** ou **SQLSetPos**. A coluna deve ser associada porque **SQLBulkOperations** ou **SQLSetPos** só funciona em colunas associadas e deve ser desassociado para que **SQLGetData** possa ser usado para recuperar dados da coluna.  
  
 Para enviar dados no momento da execução, o aplicativo faz o seguinte:  
  
1.  Coloca um valor de 32 bits no buffer do conjunto de linhas em vez de um valor de dados. Esse valor será retornado para o aplicativo posteriormente, de modo que o aplicativo deve defini-lo como um valor significativo, como o número da coluna ou o identificador de um arquivo que contém dados.  
  
2.  Define o valor no buffer de comprimento/indicador para o resultado da macro SQL_LEN_DATA_AT_EXEC (*comprimento*). Esse valor indica ao driver que os dados para o parâmetro serão enviados com **SQLPutData**. O valor de *comprimento* é usado ao enviar dados longos para uma fonte de dados que precisa saber quantos bytes de dados longos serão enviados para que possa alocar espaço. Para determinar se uma fonte de dados requer esse valor, o aplicativo chama **SQLGetInfo** com a opção SQL_NEED_LONG_DATA_LEN. Todos os drivers devem dar suporte a essa macro; se a fonte de dados não exigir o comprimento do byte, o driver poderá ignorá-lo.  
  
3.  Chama **SQLBulkOperations** ou **SQLSetPos**. O driver descobre que um buffer de comprimento/indicador contém o resultado da macro SQL_LEN_DATA_AT_EXEC (*comprimento*) e retorna SQL_NEED_DATA como o valor de retorno da função.  
  
4.  Chama **SQLParamData** em resposta ao valor de retorno de SQL_NEED_DATA. Se for necessário enviar dados longos, **SQLParamData** retornará SQL_NEED_DATA. No buffer apontado pelo argumento *ValuePtrPtr* , o driver retorna o valor exclusivo que o aplicativo colocou no buffer do conjunto de linhas. Se houver mais de uma coluna de dados em execução, o aplicativo usará esse valor para determinar a qual coluna enviar dados; o driver não precisa solicitar dados para colunas de dados em execução em qualquer ordem específica.  
  
5.  Chama **SQLPutData** para enviar os dados da coluna para o driver. Se os dados da coluna não couberem em um único buffer, como geralmente é o caso com dados longos, o aplicativo chamará **SQLPutData** repetidamente para enviar os dados em partes; cabe ao driver e à fonte de dados remontar os dados. Se o aplicativo passar dados de cadeia de caracteres terminados em nulo, o driver ou a fonte de dados deverá remover o caractere de terminação nula como parte do processo de remontagem.  
  
6.  Chama **SQLParamData** novamente para indicar que ele enviou todos os dados para a coluna. Se houver qualquer coluna de dados em execução para a qual os dados não foram enviados, o driver retornará SQL_NEED_DATA e o valor exclusivo para a próxima coluna de dados em execução; o aplicativo retorna para a etapa 5. Se os dados forem enviados para todas as colunas de dados em execução, os dados da linha serão enviados para a fonte de dados. **SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO e pode retornar o SQLSTATE que pode ser retornado por **SQLBulkOperations** ou **SQLSetPos** .  
  
 Depois que **SQLBulkOperations** ou **SQLSetPos** retorna SQL_NEED_DATA e antes de os dados serem completamente enviados para a última coluna de dados em execução, a instrução está em um estado de dados necessário. Nesse estado, o aplicativo pode chamar somente **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**ou **SQLGetDiagRec**; todas as outras funções retornam SQLSTATE HY010 (erro de sequência de função). Chamar **SQLCancel** cancela a execução da instrução e a retorna ao estado anterior. Para obter mais informações, consulte o [Apêndice B: tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
