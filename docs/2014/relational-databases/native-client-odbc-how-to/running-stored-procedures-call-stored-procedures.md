---
title: Chamar procedimentos armazenados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37ce27067c4ad30e38b6d3c168b8f676815b693d
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411295"
---
# <a name="call-stored-procedures-odbc"></a>Chamar procedimentos armazenados (ODBC)
  Quando uma instrução SQL chama um procedimento armazenado por meio da cláusula escape ODBC CALL, o driver do Microsoft® SQL Server™ envia o procedimento ao SQL Server por meio do mecanismo RPC (chamada de procedimento armazenado remoto). As solicitações de RPC ignoram grande parte da análise de instruções e do processamento de parâmetros no SQL Server e são mais rápidas do que a instrução EXECUTE do Transact-SQL.  
  
 Para um aplicativo de exemplo que demonstra este recurso, consulte [processar códigos de retorno e parâmetros de saída &#40;ODBC&#41;](running-stored-procedures-process-return-codes-and-output-parameters.md).  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>Para executar um procedimento como um RPC  
  
1.  Crie uma instrução SQL que use a sequência de escape ODBC CALL. A instrução usa marcadores de parâmetro para cada parâmetro de entrada, entrada/saída e saída, e para o valor de retorno do procedimento (se houver):  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  Chame [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md) para cada entrada, entrada/saída e parâmetro de saída e para o procedimento retornar valor (se houver).  
  
3.  Execute a instrução com [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399).  
  
> [!NOTE]  
>  Se um aplicativo enviar um procedimento usando a sintaxe EXECUTE Transact-SQL (em oposição à sequência de escape ODBC CALL), o driver ODBC SQL Server passará a chamada de procedimento para o SQL Server como uma instrução SQL, em vez de como um RPC. Além disso, os parâmetros de saída não serão retornados se a instrução EXECUTE Transact-SQL for usada.  
  
## <a name="see-also"></a>Consulte também  
 [Executando procedimentos armazenados tópicos de instruções &#40;ODBC&#41;](../../database-engine/dev-guide/running-stored-procedures-how-to-topics-odbc.md)   
 [Envio em lote de chamadas de procedimento armazenado](../native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [Executando procedimentos armazenados](../native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [Chamar um procedimento armazenado](../native-client-odbc-stored-procedures/calling-a-stored-procedure.md)   
 [Procedimentos](../native-client-odbc-queries/executing-statements/procedures.md)  
  
  
