---
title: Oferecendo suporte a transações locais | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: b75104940cca183005f8a465ea19d0a517247c25
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63213812"
---
# <a name="supporting-local-transactions"></a>Dando suporte a transações locais
  Uma sessão delimita o escopo da transação para uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transação local do provedor de OLE DB de cliente nativo. Quando, na direção de um consumidor, o provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de OLE DB de cliente nativo envia uma solicitação para uma instância conectada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do, a solicitação constitui uma unidade de trabalho para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o provedor de OLE DB de cliente nativo. As transações locais sempre encapsulam uma ou mais unidades de trabalho em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uma única sessão de provedor de OLE DB de cliente nativo.  
  
 Usando o modo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de confirmação automática do provedor de OLE DB de cliente nativo padrão, uma única unidade de trabalho é tratada como o escopo de uma transação local. Apenas uma unidade participa da transação local. Quando uma sessão é criada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo inicia uma transação para a sessão. Na conclusão bem-sucedida de uma unidade de trabalho, o trabalho é confirmado. Em caso de falha, qualquer trabalho começado é revertido e o erro é relatado ao consumidor. Em ambos os casos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o provedor de OLE DB de cliente nativo inicia uma nova transação local para a sessão para que todo o trabalho seja realizado em uma transação.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor de OLE DB de cliente nativo pode direcionar um controle mais preciso sobre o escopo da transação local usando a interface **ITransactionLocal** . Quando uma sessão do consumidor inicia uma transação, todas as unidades de trabalho da sessão entre o ponto inicial da transação e as eventuais chamadas do método **Commit** ou **Abort** são tratadas como uma unidade atômica. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo inicia implicitamente uma transação quando instruído a fazer isso pelo consumidor. Se o consumidor não solicitar retenção, a sessão reverterá para o comportamento pai em nível de transação, geralmente o modo de confirmação automática.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo oferece suporte aos parâmetros **ITransactionLocal:: StartTransaction** da seguinte maneira.  
  
|Parâmetro|DESCRIÇÃO|  
|---------------|-----------------|  
|*isoLevel*[in]|O nível de isolamento a ser usado com esta transação. Em transações locais, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte ao seguinte:<br /><br /> -ISOLATIONLEVEL_UNSPECIFIED<br />-ISOLATIONLEVEL_CHAOS<br />-ISOLATIONLEVEL_READUNCOMMITTED<br />-ISOLATIONLEVEL_READCOMMITTED<br />-ISOLATIONLEVEL_REPEATABLEREAD<br />-ISOLATIONLEVEL_CURSORSTABILITY<br />-ISOLATIONLEVEL_REPEATABLEREAD<br />-ISOLATIONLEVEL_SERIALIZABLE<br />-ISOLATIONLEVEL_ISOLATED<br />-ISOLATIONLEVEL_SNAPSHOT **Observação:** começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], ISOLATIONLEVEL_SNAPSHOT é válido para o argumento *isoLevel* se o controle de versão está habilitado ou não para o banco de dados. Porém, ocorrerá um erro se o usuário tentar executar uma instrução e o controle de versão não estiver habilitado e/ou o banco de dados não for somente leitura. Além disso, o erro XACT_E_ISOLATIONLEVEL ocorrerá se ISOLATIONLEVEL_SNAPSHOT for especificado como o *isoLevel* quando conectado a uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|*isoFlags*[in]|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo retorna um erro para qualquer valor diferente de zero.|  
|*pOtherOptions*[in]|Se não for NULL, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o provedor de OLE DB de cliente nativo solicitará o objeto de opções da interface. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo retorna XACT_E_NOTIMEOUT se o membro *ulTimeout* do objeto de opções não for zero. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo ignora o valor do membro *szDescription* .|  
|*pulTransactionLevel*[saída]|Se não for NULL, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o provedor de OLE DB de cliente nativo retornará o nível aninhado da transação.|  
  
 Para transações locais, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo implementa os parâmetros **ITransaction:: Abort** da seguinte maneira.  
  
|Parâmetro|DESCRIÇÃO|  
|---------------|-----------------|  
|*pboidReason*[in]|Ignorado se definido. Pode ser NULL com segurança.|  
|*fRetaining*[in]|Quando TRUE, uma nova transação é iniciada implicitamente para a sessão. A transação deve ser confirmada ou encerrada pelo consumidor. Quando for falso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o provedor de OLE DB de cliente nativo será revertido para o modo de confirmação automática da sessão.|  
|*fAsync*[in]|O provedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente nativo não dá suporte para anulação assíncrona. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo retornará XACT_E_NOTSUPPORTED se o valor não for false.|  
  
 Para transações locais, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo implementa os parâmetros **ITransaction:: Commit** da seguinte maneira.  
  
|Parâmetro|DESCRIÇÃO|  
|---------------|-----------------|  
|*fRetaining*[in]|Quando TRUE, uma nova transação é iniciada implicitamente para a sessão. A transação deve ser confirmada ou encerrada pelo consumidor. Quando for falso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o provedor de OLE DB de cliente nativo será revertido para o modo de confirmação automática da sessão.|  
|*grfTC*[in]|Os retornos assíncronos e da fase um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são suportados pelo provedor de OLE DB nativo do cliente. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo retorna XACT_E_NOTSUPPORTED para qualquer valor diferente de XACTTC_SYNC.|  
|*grfRM*[in]|Deve ser 0.|  
  
 Os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de linhas do provedor de OLE DB de cliente nativo na sessão são preservados em uma operação de confirmação local ou de anulação com base nos valores das propriedades do conjunto de linhas DBPROP_ABORTPRESERVE e DBPROP_COMMITPRESERVE. Por padrão, essas propriedades são VARIANT_FALSE e todos os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de linhas do provedor de OLE DB do cliente nativo na sessão são perdidos após uma operação de anulação ou confirmação.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo não implementa a interface **ITransactionObject** . Uma tentativa do consumidor de recuperar uma referência na interface retorna E_NOINTERFACE.  
  
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
 [Transações](transactions.md)   
 [Trabalhando com isolamento de instantâneo](../native-client/features/working-with-snapshot-isolation.md)  
  
  
