---
title: Dando suporte a transações locais | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- SQL Server Native Client OLE DB provider, transactions
- local transactions [OLE DB]
ms.assetid: 78f2e5fc-b6fb-4eda-9f71-991a4d6c4902
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8533747bbe5ccb79a06b10a754c4af45ab241843
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280080"
---
# <a name="supporting-local-transactions"></a>Dando suporte a transações locais
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Uma sessão delimita o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escopo de transação de uma transação local do provedor DeLE DB do cliente nativo. Quando, na direção de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um consumidor, o provedor Nativo Cliente OLE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DB submete uma solicitação a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uma instância conectada de , a solicitação constitui uma unidade de trabalho para o provedor Nativo Cliente OLE DB. As transações locais sempre envolvem uma ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mais unidades de trabalho em uma única sessão do provedor Decliente Nativo OLE DB.  
  
 Usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modo de confirmação automática do provedor DeLE DB do cliente nativo, uma única unidade de trabalho é tratada como o escopo de uma transação local. Apenas uma unidade participa da transação local. Quando uma sessão é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criada, o provedor Native Client OLE DB inicia uma transação para a sessão. Na conclusão bem-sucedida de uma unidade de trabalho, o trabalho é confirmado. Em caso de falha, qualquer trabalho começado é revertido e o erro é relatado ao consumidor. Em ambos os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] casos, o provedor Native Client OLE DB inicia uma nova transação local para a sessão para que todo o trabalho seja realizado dentro de uma transação.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor Nativo Cliente OLE DB pode direcionar um controle mais preciso sobre o escopo de transações locais usando a interface **ITransactionLocal.** Quando uma sessão do consumidor inicia uma transação, todas as unidades de trabalho da sessão entre o ponto inicial da transação e as eventuais chamadas do método **Commit** ou **Abort** são tratadas como uma unidade atômica. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB inicia implicitamente uma transação quando orientado a fazê-lo pelo consumidor. Se o consumidor não solicitar retenção, a sessão reverterá para o comportamento pai em nível de transação, geralmente o modo de confirmação automática.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB suporta **parâmetros ITransactionLocal::StartTransaction** da seguinte forma.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*isoLevel*[in]|O nível de isolamento a ser usado com esta transação. Nas transações locais, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB suporta o seguinte:<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> Observação: do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] em diante, ISOLATIONLEVEL_SNAPSHOT é válido para o argumento *isoLevel*, independentemente de o controle de versão estar habilitado ou não para o banco de dados. Porém, ocorrerá um erro se o usuário tentar executar uma instrução e o controle de versão não estiver habilitado e/ou o banco de dados não for somente leitura. Além disso, o erro XACT_E_ISOLATIONLEVEL ocorrerá se ISOLATIONLEVEL_SNAPSHOT for especificado como o *isoLevel* quando conectado a uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|*isoFlags*[in]|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB retorna um erro por qualquer valor que não seja zero.|  
|*pOtherOptions*[in]|Se não for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NULO, o provedor Native Client OLE DB solicita o objeto de opções da interface. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB retorna XACT_E_NOTIMEOUT se o membro *ulTimeout* do objeto de opções não for zero. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB ignora o valor do membro *szDescription.*|  
|*pulTransactionLevel*[out]|Se não for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NULO, o provedor Native Client OLE DB retorna o nível aninhado da transação.|  
  
 Para transações locais, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Nativo Cliente OLE DB implementa **parâmetros ITransaction::Abort** da seguinte forma.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*pboidReason*[in]|Ignorado se definido. Pode ser NULL com segurança.|  
|*fRetaining*[in]|Quando TRUE, uma nova transação é iniciada implicitamente para a sessão. A transação deve ser confirmada ou encerrada pelo consumidor. Quando FALSE, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o provedor Native Client OLE DB volta ao modo de confirmação automática para a sessão.|  
|*fAsync*[in]|O abortamento assíncrono [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é suportado pelo provedor Native Client OLE DB. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB retorna XACT_E_NOTSUPPORTED se o valor não for FALSO.|  
  
 Para transações locais, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Nativo Cliente OLE DB implementa **iTransaction:::Commit** parâmetros da seguinte forma.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*fRetaining*[in]|Quando TRUE, uma nova transação é iniciada implicitamente para a sessão. A transação deve ser confirmada ou encerrada pelo consumidor. Quando FALSE, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o provedor Native Client OLE DB volta ao modo de confirmação automática para a sessão.|  
|*grfTC*[in]|Os retornos assíncronos e de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fase um não são suportados pelo provedor Native Client OLE DB. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB retorna XACT_E_NOTSUPPORTED por qualquer valor que não XACTTC_SYNC.|  
|*grfRM*[in]|Deve ser 0.|  
  
 Os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de linhas do provedor Cliente Nativo OLE DB na sessão são preservados em uma operação local de confirmação ou abortamento com base nos valores das propriedades rowset DBPROP_ABORTPRESERVE e DBPROP_COMMITPRESERVE. Por padrão, essas propriedades são [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VARIANT_FALSE e todos os conjuntos de linhas do provedor Nativo Cliente OLE DB na sessão são perdidos após uma operação de abortamento ou confirmação.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB não implementa a interface **ITransactionObject.** Uma tentativa do consumidor de recuperar uma referência na interface retorna E_NOINTERFACE.  
  
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
 [Transações](../../relational-databases/native-client-ole-db-transactions/transactions.md)   
 [Trabalhando com isolamento de instantâneo](../../relational-databases/native-client/features/working-with-snapshot-isolation.md)  
  
  
