---
title: Dados longos e SQLSetPos e SQLBulkOperations | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287860"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Dados Long e SQLSetPos e SQLBulkOperations
Como é o caso dos parâmetros nas instruções SQL, dados longos podem ser enviados ao atualizar linhas com **SQLBulkOperations** ou **SQLSetPos** ou ao inserir linhas com **SQLBulkOperations**. Os dados são enviados em partes, com várias chamadas para **SQLPutData**. As colunas para as quais os dados são enviados no momento da execução são conhecidas como *colunas de dados em execução*.  
  
> [!NOTE]  
>  Um aplicativo realmente pode enviar qualquer tipo de dados no momento de execução com **SQLPutData**, embora apenas dados de caracteres e binários possam ser enviados em partes. No entanto, se os dados são pequenos o suficiente para caber em um único buffer, geralmente não há razão para usar **SQLPutData**. É muito mais fácil vincular o buffer e deixar o driver recuperar os dados do buffer.  
  
 Como as colunas de dados longos normalmente não estão vinculadas, o aplicativo deve vincular a coluna antes de chamar **SQLBulkOperations** ou **SQLSetPos** e desvinculá-la depois de chamar **SQLBulkOperations** ou **SQLSetPos**. A coluna deve ser vinculada porque **sqlBulkOperations** ou **SQLSetPos** opera apenas em colunas vinculadas e deve ser desvinculada para que **o SQLGetData** possa ser usado para recuperar dados da coluna.  
  
 Para enviar dados no momento da execução, o aplicativo faz o seguinte:  
  
1.  Coloca um valor de 32 bits no buffer de conjunto de linhas em vez de um valor de dados. Esse valor será devolvido ao aplicativo posteriormente, de modo que o aplicativo deve defini-lo para um valor significativo, como o número da coluna ou a alça de um arquivo contendo dados.  
  
2.  Define o valor no buffer de comprimento/indicador para o resultado da macro SQL_LEN_DATA_AT_EXEC *(comprimento).* Este valor indica ao driver que os dados para o parâmetro serão enviados com **SQLPutData**. O valor *de comprimento* é usado ao enviar dados longos para uma fonte de dados que precisa saber quantos bytes de dados longos serão enviados para que ele possa prealocar o espaço. Para determinar se uma fonte de dados requer esse valor, o aplicativo chama **sqlGetInfo** com a opção SQL_NEED_LONG_DATA_LEN. Todos os drivers devem suportar essa macro; se a fonte de dados não exigir o comprimento do byte, o driver pode ignorá-lo.  
  
3.  Chamadas **SQLBulkOperations** ou **SQLSetPos**. O driver descobre que um buffer de comprimento/indicador contém o resultado da macro de SQL_LEN_DATA_AT_EXEC *(comprimento)* e retorna SQL_NEED_DATA como o valor de retorno da função.  
  
4.  Chama **SQLParamData** em resposta ao valor de retorno SQL_NEED_DATA. Se os dados longos precisarem ser enviados, **o SQLParamData** retorna SQL_NEED_DATA. No buffer apontado pelo argumento *ValuePtrPtr,* o driver retorna o valor único que o aplicativo colocou no buffer de conjunto de linhas. Se houver mais de uma coluna de dados em execução, o aplicativo usará esse valor para determinar para qual coluna enviar dados; o driver não é obrigado a solicitar dados para colunas de dados em execução em qualquer ordem específica.  
  
5.  Chama **sqlPutData** para enviar os dados da coluna para o driver. Se os dados da coluna não se encaixam em um único buffer, como é frequentemente o caso com dados longos, o aplicativo chama **SQLPutData** repetidamente para enviar os dados em partes; cabe ao driver e à fonte de dados remontar os dados. Se o aplicativo passar dados de seqüência de caracteres com término nulo, o driver ou a fonte de dados devem remover o caractere de rescisão nula como parte do processo de remontagem.  
  
6.  Chama **o SQLParamData** novamente para indicar que enviou todos os dados para a coluna. Se houver colunas de dados em execução para as quais os dados não foram enviados, o driver retorna SQL_NEED_DATA e o valor único para a próxima coluna data-at-execution; o aplicativo retorna à etapa 5. Se os dados forem enviados para todas as colunas de execução de dados, os dados da linha são enviados para a fonte de dados. **SQLParamData** então retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO e pode retornar qualquer SQLSTATE que **SQLBulkOperations** ou **SQLSetPos** possam retornar.  
  
 Depois **que sqlBulkOperations** ou **SQLSetPos** retornar SQL_NEED_DATA e antes que os dados sejam completamente enviados para a última coluna de dados em execução, a declaração está em um estado de Dados de Necessidade. Neste estado, o aplicativo pode chamar apenas **SQLPutData,** **SQLParamData,** **SQLCancel,** **SQLGetDiagField**ou **SQLGetDiagRec;** todas as outras funções retornam SQLSTATE HY010 (erro de seqüência de função). Chamar **o SQLCancel** cancela a execução da declaração e a devolve ao seu estado anterior. Para obter mais informações, consulte [o apêndice B: Tabelas de transição do estado oDBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
