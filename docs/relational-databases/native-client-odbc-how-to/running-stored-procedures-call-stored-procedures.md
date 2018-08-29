---
title: Chamar procedimentos armazenados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 82845d2faac407385cf3ec8036fd6b63e5457b3c
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43085170"
---
# <a name="running-stored-procedures---call-stored-procedures"></a>Executar procedimentos armazenados – Chamar procedimentos armazenados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suporta a execução de procedimentos armazenados como procedimentos armazenados remotos. Executar um procedimento armazenado como um procedimento armazenado remoto permite que o driver e o servidor otimizem o desempenho da execução do procedimento.  
  
  Quando uma instrução SQL chama um procedimento armazenado por meio da cláusula escape ODBC CALL, o driver do Microsoft® SQL Server™ envia o procedimento ao SQL Server por meio do mecanismo RPC (chamada de procedimento armazenado remoto). As solicitações de RPC ignoram grande parte da análise de instruções e do processamento de parâmetros no SQL Server e são mais rápidas do que a instrução EXECUTE do Transact-SQL.  
  
 Para um aplicativo de exemplo que demonstra este recurso, consulte [processar códigos de retorno e parâmetros de saída &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/running-stored-procedures-process-return-codes-and-output-parameters.md).  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>Para executar um procedimento como um RPC  
  
1.  Crie uma instrução SQL que use a sequência de escape ODBC CALL. A instrução usa marcadores de parâmetro para cada parâmetro de entrada, entrada/saída e saída, e para o valor de retorno do procedimento (se houver):  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  Chame [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) para cada entrada, entrada/saída e parâmetro de saída e para o procedimento retornar valor (se houver).  
  
3.  Execute a instrução com [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399).  
  
> [!NOTE]  
>  Se um aplicativo enviar um procedimento usando a sintaxe EXECUTE Transact-SQL (em oposição à sequência de escape ODBC CALL), o driver ODBC SQL Server passará a chamada de procedimento para o SQL Server como uma instrução SQL, em vez de como um RPC. Além disso, os parâmetros de saída não serão retornados se a instrução EXECUTE Transact-SQL for usada.  
  
## <a name="see-also"></a>Consulte também  
  [Envio em lote de chamadas de procedimento armazenado](../../relational-databases/native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [Executando procedimentos armazenados](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [Chamar um procedimento armazenado](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)   
 [Procedimentos](../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  
  
