---
title: Dando suporte a transações locais | Microsoft Docs
description: Transações locais no OLE DB Driver para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- OLE DB Driver for SQL Server, transactions
- local transactions [OLE DB]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: c0cfc1ad6ff3439efe458f97394909c919b77075
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993965"
---
# <a name="supporting-local-transactions"></a>Dando suporte a transações locais
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Uma sessão delimita o escopo da transação para uma transação local do Driver do OLE DB para SQL Server. Quando, na direção de um consumidor, o Driver do OLE DB para SQL Server envia uma solicitação para uma instância conectada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a solicitação constitui uma unidade de trabalho para o Driver do OLE DB para SQL Server. As transações locais sempre encapsulam uma ou mais unidades de trabalho em uma sessão do Driver do OLE DB para SQL Server.  
  
 Usando o modo de confirmação automática do OLE DB Driver for SQL Server padrão, uma única unidade de trabalho é tratada como o escopo de uma transação local. Apenas uma unidade participa da transação local. Quando uma sessão é criada, o Driver do OLE DB para SQL Server inicia uma transação para a sessão. Na conclusão bem-sucedida de uma unidade de trabalho, o trabalho é confirmado. Em caso de falha, qualquer trabalho começado é revertido e o erro é relatado ao consumidor. De qualquer maneira, o OLE DB Driver for SQL Server inicia uma nova transação local para a sessão, de forma que todo o trabalho seja realizado em uma transação.  
  
 O consumidor do OLE DB Driver for SQL Server pode direcionar um controle mais preciso sobre o escopo da transação local usando a interface **ITransactionLocal**. Quando uma sessão do consumidor inicia uma transação, todas as unidades de trabalho da sessão entre o ponto inicial da transação e as eventuais chamadas do método **Commit** ou **Abort** são tratadas como uma unidade atômica. O Driver do OLE DB para SQL Server inicia uma transação implicitamente quando direcionado a fazê-lo pelo consumidor. Se o consumidor não solicitar retenção, a sessão reverterá para o comportamento pai em nível de transação, geralmente o modo de confirmação automática.  
  
 O Driver do OLE DB para SQL Server dá suporte aos parâmetros **ITransactionLocal::StartTransaction**, conforme mostrado a seguir.  
  
|Parâmetro|DESCRIÇÃO|  
|---------------|-----------------|  
|*isoLevel*[in]|O nível de isolamento a ser usado com esta transação. Em transações locais, o Driver do OLE DB para SQL Server dá suporte ao seguinte:<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> Observação: do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] em diante, ISOLATIONLEVEL_SNAPSHOT é válido para o argumento *isoLevel*, independentemente de o controle de versão estar habilitado ou não para o banco de dados. Porém, ocorrerá um erro se o usuário tentar executar uma instrução e o controle de versão não estiver habilitado e/ou o banco de dados não for somente leitura. Além disso, o erro XACT_E_ISOLATIONLEVEL ocorrerá se ISOLATIONLEVEL_SNAPSHOT for especificado como o *isoLevel* quando conectado a uma versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anterior ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].|  
|*isoFlags*[in]|O Driver do OLE DB para SQL Server retorna um erro para qualquer valor diferente de zero.|  
|*pOtherOptions*[in]|Se for diferente de NULL, o Driver do OLE DB para SQL Server solicitará o objeto de opções da interface. O Driver do OLE DB para SQL Server retornará XACT_E_NOTIMEOUT se o membro *ulTimeout* do objeto de opções for diferente de zero. O Driver do OLE DB para SQL Server ignora o valor do membro *szDescription*.|  
|*pulTransactionLevel*[out]|Se for diferente de NULL, o Driver do OLE DB para SQL Server retornará o nível aninhado da transação.|  
  
 Para transações locais, o Driver do OLE DB para SQL Server implementa parâmetros **ITransaction::Abort**, conforme mostrado a seguir.  
  
|Parâmetro|DESCRIÇÃO|  
|---------------|-----------------|  
|*pboidReason*[in]|Ignorado se definido. Pode ser NULL com segurança.|  
|*fRetaining*[in]|Quando TRUE, uma nova transação é iniciada implicitamente para a sessão. A transação deve ser confirmada ou encerrada pelo consumidor. Quando FALSE, o Driver do OLE DB para SQL Server reverte ao modo de confirmação automática para a sessão.|  
|*fAsync*[in]|A anulação assíncrona não é compatível com o Driver do OLE DB para SQL Server. O Driver do OLE DB para SQL Server retornará XACT_E_NOTSUPPORTED se o valor não for FALSE.|  
  
 Para transações locais, o Driver do OLE DB para SQL Server implementa parâmetros **ITransaction::Commit**, conforme mostrado a seguir.  
  
|Parâmetro|DESCRIÇÃO|  
|---------------|-----------------|  
|*fRetaining*[in]|Quando TRUE, uma nova transação é iniciada implicitamente para a sessão. A transação deve ser confirmada ou encerrada pelo consumidor. Quando FALSE, o Driver do OLE DB para SQL Server reverte ao modo de confirmação automática para a sessão.|  
|*grfTC*[in]|Retornos assíncronos e de fase um não são compatíveis com o Driver do OLE DB para SQL Server. O Driver do OLE DB para SQL Server retorna XACT_E_NOTSUPPORTED para qualquer valor diferente de XACTTC_SYNC.|  
|*grfRM*[in]|Deve ser 0.|  
  
 Os conjuntos de linhas do OLE DB Driver for SQL Server na sessão são preservados em uma operação de confirmação ou anulação local com base nos valores das propriedades do conjunto de linhas DBPROP_ABORTPRESERVE e DBPROP_COMMITPRESERVE. Por padrão, essas propriedades são VARIANT_FALSE e todos os conjuntos de linhas do OLE DB Driver for SQL Server na sessão são perdidas após uma operação de anulação ou de confirmação.  
  
 O Driver do OLE DB para SQL Server não implementa a interface **ITransactionObject**. Uma tentativa do consumidor de recuperar uma referência na interface retorna E_NOINTERFACE.  
  
 Este exemplo usa **ITransactionLocal**.  
  
```  
// Interfaces used in the example.  
IDBCreateSession*   pIDBCreateSession   = NULL;  
ITransaction*       pITransaction       = NULL;  
IDBCreateCommand*   pIDBCreateCommand   = NULL;  
IRowset*            pIRowset            = NULL;  
  
HRESULT             hr;  
  
// Get the command creation and local transaction interfaces for the  
// session.  
if (FAILED(hr = pIDBCreateSession->CreateSession(NULL,  
     IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand)))  
    {  
    // Process error from session creation. Release any references and  
    // return.  
    }  
  
if (FAILED(hr = pIDBCreateCommand->QueryInterface(IID_ITransactionLocal,  
    (void**) &pITransaction)))  
    {  
    // Process error. Release any references and return.  
    }  
  
// Start the local transaction.  
if (FAILED(hr = ((ITransactionLocal*) pITransaction)->StartTransaction(  
    ISOLATIONLEVEL_REPEATABLEREAD, 0, NULL, NULL)))  
    {  
    // Process error from StartTransaction. Release any references and  
    // return.  
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
    // Get error from update, then terminate.  
    pITransaction->Abort(NULL, FALSE, FALSE);  
    }  
else  
    {  
    if (FAILED(hr = pITransaction->Commit(FALSE, XACTTC_SYNC, 0)))  
        {  
        // Get error from failed commit.  
        }  
    }  
  
if (FAILED(hr))  
    {  
    // Update of data or commit failed. Release any references and  
    // return.  
    }  
  
// Release any references and continue.  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Transações](../../oledb/ole-db-transactions/transactions.md)   
 [Trabalhando com isolamento de instantâneo](../../oledb/features/working-with-snapshot-isolation.md)  
  
  
