---
title: Oferecendo suporte a transações locais | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 76e14df87e8dca104fc0b9da44836288dc56ea69
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761544"
---
# <a name="supporting-local-transactions"></a>Dando suporte a transações locais
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Uma sessão delimita o escopo da transação para uma transação local do provedor de OLE DB do cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo. Quando, na direção de um consumidor, o provedor de OLE DB do cliente nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envia uma solicitação para uma instância conectada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a solicitação constitui uma unidade de trabalho para o provedor de OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo Client. As transações locais sempre encapsulam uma ou mais unidades de trabalho em uma única [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sessão do provedor de OLE DB do cliente nativo.  
  
 Usando o modo de confirmação automática do provedor de OLE DB de cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] padrão, uma única unidade de trabalho é tratada como o escopo de uma transação local. Apenas uma unidade participa da transação local. Quando uma sessão é criada, o provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client inicia uma transação para a sessão. Na conclusão bem-sucedida de uma unidade de trabalho, o trabalho é confirmado. Em caso de falha, qualquer trabalho começado é revertido e o erro é relatado ao consumidor. Em ambos os casos, o provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo inicia uma nova transação local para a sessão, de forma que todo o trabalho seja realizado em uma transação.  
  
 O consumidor do provedor de OLE DB de cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode direcionar um controle mais preciso sobre o escopo da transação local usando a interface **ITransactionLocal** . Quando uma sessão do consumidor inicia uma transação, todas as unidades de trabalho da sessão entre o ponto inicial da transação e as eventuais chamadas do método **Commit** ou **Abort** são tratadas como uma unidade atômica. O provedor de OLE DB do cliente nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicia implicitamente uma transação quando instruído a fazer isso pelo consumidor. Se o consumidor não solicitar retenção, a sessão reverterá para o comportamento pai em nível de transação, geralmente o modo de confirmação automática.  
  
 O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client oferece suporte aos parâmetros **ITransactionLocal:: StartTransaction** da seguinte maneira.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*isoLevel*[in]|O nível de isolamento a ser usado com esta transação. Em transações locais, o provedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo do cliente oferece suporte ao seguinte:<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> Observação: do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] em diante, ISOLATIONLEVEL_SNAPSHOT é válido para o argumento *isoLevel*, independentemente de o controle de versão estar habilitado ou não para o banco de dados. Porém, ocorrerá um erro se o usuário tentar executar uma instrução e o controle de versão não estiver habilitado e/ou o banco de dados não for somente leitura. Além disso, o erro XACT_E_ISOLATIONLEVEL ocorrerá se ISOLATIONLEVEL_SNAPSHOT for especificado como o *isoLevel* quando conectado a uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|*isoFlags*[in]|O provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo retorna um erro para qualquer valor diferente de zero.|  
|*pOtherOptions*[in]|Se não for NULL, o provedor de OLE DB do cliente nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicitará o objeto de opções da interface. O provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo retorna XACT_E_NOTIMEOUT se o membro *ulTimeout* do objeto de opções não for zero. O provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo ignora o valor do membro *szDescription* .|  
|*pulTransactionLevel*[out]|Se não for NULL, o provedor de OLE DB do cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará o nível aninhado da transação.|  
  
 Para transações locais, o provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client implementa os parâmetros **ITransaction:: Abort** da seguinte maneira.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*pboidReason*[in]|Ignorado se definido. Pode ser NULL com segurança.|  
|*fRetaining*[in]|Quando TRUE, uma nova transação é iniciada implicitamente para a sessão. A transação deve ser confirmada ou encerrada pelo consumidor. Quando for falso, o provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo do cliente será revertido para o modo de confirmação automática da sessão.|  
|*fAsync*[in]|A anulação assíncrona não tem suporte pelo provedor de OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. O provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo retorna XACT_E_NOTSUPPORTED se o valor não for FALSE.|  
  
 Para transações locais, o provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client implementa os parâmetros **ITransaction:: Commit** da seguinte maneira.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*fRetaining*[in]|Quando TRUE, uma nova transação é iniciada implicitamente para a sessão. A transação deve ser confirmada ou encerrada pelo consumidor. Quando for falso, o provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo do cliente será revertido para o modo de confirmação automática da sessão.|  
|*grfTC*[in]|Os retornos assíncronos e da fase um não têm suporte pelo provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. O provedor de OLE DB de cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo retorna XACT_E_NOTSUPPORTED para qualquer valor diferente de XACTTC_SYNC.|  
|*grfRM*[in]|Deve ser 0.|  
  
 Os conjuntos de linhas do provedor de OLE DB de cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na sessão são preservados em uma operação de confirmação ou anulação local com base nos valores das propriedades do conjunto de linhas DBPROP_ABORTPRESERVE e DBPROP_COMMITPRESERVE. Por padrão, essas propriedades são VARIANT_FALSE e todas as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de linhas do provedor de OLE DB de cliente nativo na sessão são perdidas após uma operação de anulação ou confirmação.  
  
 O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client não implementa a interface **ITransactionObject** . Uma tentativa do consumidor de recuperar uma referência na interface retorna E_NOINTERFACE.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Transações](../../relational-databases/native-client-ole-db-transactions/transactions.md)   
 [Trabalhando com isolamento de instantâneo](../../relational-databases/native-client/features/working-with-snapshot-isolation.md)  
  
  
