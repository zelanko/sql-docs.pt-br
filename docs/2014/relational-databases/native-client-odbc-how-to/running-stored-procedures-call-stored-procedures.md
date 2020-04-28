---
title: Chamar procedimentos armazenados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a960df20b7b07bffab900589ae4d520541d720c1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72688661"
---
# <a name="call-stored-procedures-odbc"></a>Chamar procedimentos armazenados (ODBC)
  Quando uma instrução SQL chama um procedimento armazenado usando a cláusula ODBC CALL escape, o driver Microsoft SQL Server envia o procedimento para SQL Server usando o mecanismo RPC (chamada de procedimento armazenado remoto). As solicitações de RPC ignoram grande parte da análise de instruções e do processamento de parâmetros no SQL Server e são mais rápidas do que a instrução EXECUTE do Transact-SQL.  
  
 Para obter um aplicativo de exemplo que demonstra esse recurso, consulte [processar códigos de retorno e parâmetros de saída &#40;&#41;ODBC ](running-stored-procedures-process-return-codes-and-output-parameters.md).  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>Para executar um procedimento como um RPC  
  
1.  Crie uma instrução SQL que use a sequência de escape ODBC CALL. A instrução usa marcadores de parâmetro para cada parâmetro de entrada, entrada/saída e saída, e para o valor de retorno do procedimento (se houver):  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  Chame [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md) para cada entrada, entrada/saída e parâmetro de saída e obter o valor de retorno de procedimento (se houver algum).  
  
3.  Execute a instrução com [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399).  
  
> [!NOTE]  
>  Se um aplicativo enviar um procedimento usando a sintaxe EXECUTE Transact-SQL (em oposição à sequência de escape ODBC CALL), o driver ODBC SQL Server passará a chamada de procedimento para o SQL Server como uma instrução SQL, em vez de como um RPC. Além disso, os parâmetros de saída não serão retornados se a instrução EXECUTE Transact-SQL for usada.  
  
## <a name="see-also"></a>Consulte Também  
 [Tópicos de instruções sobre como executar procedimentos armazenados &#40;&#41;ODBC](../../database-engine/dev-guide/running-stored-procedures-how-to-topics-odbc.md)   
 [Processamento em lote de chamadas de procedimento armazenado](../native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [Executando procedimentos armazenados](../native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [Chamando um procedimento armazenado](../native-client-odbc-stored-procedures/calling-a-stored-procedure.md)   
 [Procedimentos](../native-client-odbc-queries/executing-statements/procedures.md)  
  
  
