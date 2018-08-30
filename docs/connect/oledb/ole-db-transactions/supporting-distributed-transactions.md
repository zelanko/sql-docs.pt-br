---
title: Suporte a transações distribuídas | Microsoft Docs
description: Transações distribuídas no Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- distributed transactions [OLE DB]
- MS DTC
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
- ITransactionJoin interface
- MS DTC, about distributed transaction support
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 9486af5a9dbd4f607f376a5f916e35ace88be872
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43028420"
---
# <a name="supporting-distributed-transactions"></a>Dando suporte a transações distribuídas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Os consumidores do OLE DB Driver for SQL Server podem usar o método **ITransactionJoin::JoinTransaction** para participar de uma transação distribuída coordenada pelo MS DTC (Coordenador de Transações Distribuídas da Microsoft).  
  
 O MS DTC expõe objetos COM que permitem que os clientes iniciem e participem de transações coordenadas através de várias conexões com vários repositórios de dados. Para iniciar uma transação, o Driver OLE DB para o consumidor do SQL Server usa o MS DTC **ITransactionDispenser** interface. O membro **BeginTransaction** de **ITransactionDispenser** retorna uma referência a um objeto de transação distribuída. Essa referência é passada para o Driver do OLE DB para SQL Server usando **JoinTransaction**.  
  
 O MS DTC dá suporte à confirmação e à anulação assíncronas de transações distribuídas. Para obter a notificação do status da transação assíncrona, o consumidor implementa a interface **ITransactionOutcomeEvents** e a conecta a um objeto de transação do MS DTC.  
  
 Para transações distribuídas, o OLE DB Driver for SQL Server implementa os parâmetros de **ITransactionJoin::JoinTransaction**, conforme indicado a seguir.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*punkTransactionCoord*|Um ponteiro para um objeto de transação do MS DTC.|  
|*IsoLevel*|Ignorado pelo Driver do OLE DB para SQL Server. O nível de isolamento para transações coordenadas pelo MS DTC é determinado quando o consumidor faz a aquisição de um objeto de transação do MS DTC.|  
|*IsoFlags*|Deve ser 0. O Driver do OLE DB para SQL Server retornará XACT_E_NOISORETAIN se qualquer outro valor for especificado pelo consumidor.|  
|*POtherOptions*|Se não for nulo, o Driver do OLE DB para SQL Server solicita o objeto de opções da interface. O Driver do OLE DB para SQL Server retornará XACT_E_NOTIMEOUT se o objeto de opções *ulTimeout* membro não é zero. O Driver do OLE DB para SQL Server ignora o valor da *szDescription* membro.|  
  
 Este exemplo coordena a transação usando o MS DTC.  
  
```  
// Interfaces used in the example.  
IDBCreateSession*       pIDBCreateSession   = NULL;  
ITransactionJoin*       pITransactionJoin   = NULL;  
IDBCreateCommand*       pIDBCreateCommand   = NULL;  
IRowset*                pIRowset            = NULL;  
  
// Transaction dispenser and transaction from MS DTC.  
ITransactionDispenser*  pITransactionDispenser = NULL;  
ITransaction*           pITransaction       = NULL;  
  
    HRESULT             hr;  
  
// Get the command creation interface for the session.  
if (FAILED(hr = pIDBCreateSession->CreateSession(NULL,  
     IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand)))  
    {  
    // Process error from session creation. Release any references and  
    // return.  
    }  
  
// Get a transaction dispenser object from MS DTC and  
// start a transaction.  
if (FAILED(hr = DtcGetTransactionManager(NULL, NULL,  
    IID_ITransactionDispenser, 0, 0, NULL,  
    (void**) &pITransactionDispenser)))  
    {  
    // Process error message from MS DTC, release any references,  
    // and then return.  
    }  
if (FAILED(hr = pITransactionDispenser->BeginTransaction(  
    NULL, ISOLATIONLEVEL_READCOMMITTED, ISOFLAG_RETAIN_DONTCARE,  
    NULL, &pITransaction)))  
    {  
    // Process error message from MS DTC, release any references,  
    // and then return.  
    }  
  
// Join the transaction.  
if (FAILED(pIDBCreateCommand->QueryInterface(IID_ITransactionJoin,  
    (void**) &pITransactionJoin)))  
    {  
    // Process failure to get an interface, release any references, and  
    // then return.  
    }  
if (FAILED(pITransactionJoin->JoinTransaction(  
    (IUnknown*) pITransaction, 0, 0, NULL)))  
    {  
    // Process join failure, release any references, and then return.  
    }  
  
// Get data into a rowset, then update the data. Functions are not  
// illustrated in this example.  
if (FAILED(hr = ExecuteCommand(pIDBCreateCommand, &pIRowset)))  
    {  
    // Release any references and return.  
    }  
  
// If rowset data update fails, then terminate the transaction, else  
// commit. The example doesn't retain the rowset.  
if (FAILED(hr = UpdateDataInRowset(pIRowset, bDelayedUpdate)))  
    {  
    // Get error from update, then abort.  
    pITransaction->Abort(NULL, FALSE, FALSE);  
    }  
else  
    {  
    if (FAILED(hr = pITransaction->Commit(FALSE, 0, 0)))  
        {  
        // Get error from failed commit.  
        //  
        // If a distributed commit fails, application logic could  
        // analyze failure and retry. In this example, terminate. The   
        // consumer must resolve this somehow.  
        pITransaction->Abort(NULL, FALSE, FALSE);  
        }  
    }  
  
if (FAILED(hr))  
    {  
    // Update of data or commit failed. Release any references and  
    // return.  
    }  
  
// Un-enlist from the distributed transaction by setting   
// the transaction object pointer to NULL.  
if (FAILED(pITransactionJoin->JoinTransaction(  
    (IUnknown*) NULL, 0, 0, NULL)))  
    {  
    // Process failure, and then return.  
    }  
  
// Release any references and continue.  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Transações](../../oledb/ole-db-transactions/transactions.md)  
  
  
