---
title: Sessões | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 3a980816-675c-4fba-acc9-429297d85bbd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f594ace96fc34a77adca244e79c55551f0ddb8d4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48138246"
---
# <a name="sessions"></a>Sessões
  Um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sessão do provedor OLE DB do Native Client representa uma única conexão a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client exige que as sessões delimitem espaço de transação para uma fonte de dados. Todos os objetos de comando criados de um objeto de sessão específico participam da transação local ou distribuída do objeto de sessão.  
  
 O primeiro objeto de sessão criado na fonte de dados inicializada recebe a conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estabelecida na inicialização. Quando todas as referências nas interfaces do objeto de sessão são liberadas, a conexão com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] torna-se disponível a outro objeto de sessão criado na fonte de dados.  
  
 Um objeto de sessão adicional criado na fonte de dados estabelece sua própria conexão com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conforme especificado pela fonte de dados. A conexão com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é cancelada quando o aplicativo libera todas as referências aos objetos criados naquela sessão.  
  
 O exemplo a seguir demonstra como usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client para se conectar a um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados:  
  
```  
int main()  
{  
    // Interfaces used in the example.  
    IDBInitialize*      pIDBInitialize      = NULL;  
    IDBCreateSession*   pIDBCreateSession   = NULL;  
    IDBCreateCommand*   pICreateCmd1        = NULL;  
    IDBCreateCommand*   pICreateCmd2        = NULL;  
    IDBCreateCommand*   pICreateCmd3        = NULL;  
  
    // Initialize COM.  
    if (FAILED(CoInitialize(NULL)))  
    {  
        // Display error from CoInitialize.  
        return (-1);  
    }  
  
    // Get the memory allocator for this task.  
    if (FAILED(CoGetMalloc(MEMCTX_TASK, &g_pIMalloc)))  
    {  
        // Display error from CoGetMalloc.  
        goto EXIT;  
    }  
  
    // Create an instance of the data source object.  
    if (FAILED(CoCreateInstance(CLSID_SQLNCLI10, NULL,  
        CLSCTX_INPROC_SERVER, IID_IDBInitialize, (void**)  
        &pIDBInitialize)))  
    {  
        // Display error from CoCreateInstance.  
        goto EXIT;  
    }  
  
    // The InitFromPersistedDS function   
    // performs IDBInitialize->Initialize() establishing  
    // the first application connection to the instance of SQL Server.  
    if (FAILED(InitFromPersistedDS(pIDBInitialize, L"MyDataSource",  
        NULL, NULL)))  
    {  
        goto EXIT;  
    }  
  
    // The IDBCreateSession interface is implemented on the data source  
    // object. Maintaining the reference received maintains the   
    // connection of the data source to the instance of SQL Server.  
    if (FAILED(pIDBInitialize->QueryInterface(IID_IDBCreateSession,  
        (void**) &pIDBCreateSession)))  
    {  
        // Display error from pIDBInitialize.  
        goto EXIT;  
    }  
  
    // Releasing this has no effect on the SQL Server connection  
    // of the data source object because of the reference maintained by  
    // pIDBCreateSession.  
    pIDBInitialize->Release();  
    pIDBInitialize = NULL;  
  
    // The session created next receives the SQL Server connection of  
    // the data source object. No new connection is established.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd1)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
    // A new connection to the instance of SQL Server is established to support the  
    // next session object created. On successful completion, the  
    // application has two active connections on the SQL Server.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd2)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
    // pICreateCmd1 has the data source connection. Because the  
    // reference on the IDBCreateSession interface of the data source  
    // has not been released, releasing the reference on the session  
    // object does not terminate a connection to the instance of SQL Server.  
    // However, the connection of the data source object is now   
    // available to another session object. After a successful call to   
    // Release, the application still has two active connections to the   
    // instance of SQL Server.  
    pICreateCmd1->Release();  
    pICreateCmd1 = NULL;  
  
    // The next session created gets the SQL Server connection  
    // of the data source object. The application has two active  
    // connections to the instance of SQL Server.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd3)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
EXIT:  
    // Even on error, this does not terminate a SQL Server connection   
    // because pICreateCmd1 has the connection of the data source   
    // object.  
    if (pICreateCmd1 != NULL)  
        pICreateCmd1->Release();  
  
    // Releasing the reference on pICreateCmd2 terminates the SQL  
    // Server connection supporting the session object. The application  
    // now has only a single active connection on the instance of SQL Server.  
    if (pICreateCmd2 != NULL)  
        pICreateCmd2->Release();  
  
    // Even on error, this does not terminate a SQL Server connection   
    // because pICreateCmd3 has the connection of the   
    // data source object.  
    if (pICreateCmd3 != NULL)  
        pICreateCmd3->Release();  
  
    // On release of the last reference on a data source interface, the  
    // connection of the data source object to the instance of SQL Server is broken.  
    // The example application now has no SQL Server connections active.  
    if (pIDBCreateSession != NULL)  
        pIDBCreateSession->Release();  
  
    // Called only if an error occurred while attempting to get a   
    // reference on the IDBCreateSession interface of the data source.  
    // If so, the call to IDBInitialize::Uninitialize terminates the   
    // connection of the data source object to the instance of SQL Server.  
    if (pIDBInitialize != NULL)  
    {  
        if (FAILED(pIDBInitialize->Uninitialize()))  
        {  
            // Uninitialize is not required, but it fails if an  
            // interface has not been released. Use it for  
            // debugging.  
        }  
        pIDBInitialize->Release();  
    }  
  
    if (g_pIMalloc != NULL)  
        g_pIMalloc->Release();  
  
    CoUninitialize();  
  
    return (0);  
}  
```  
  
 Conectando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos de sessão do provedor OLE DB do Native Client a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode gerar uma sobrecarga significativa para aplicativos que criam e liberam objetos de sessão. A sobrecarga pode ser minimizada com o gerenciamento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eficaz dos objetos de sessão do provedor OLE DB do Native Client. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Aplicativos nativos de provedor de dados OLE DB podem manter o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexão de um objeto de sessão ativo, mantendo uma referência pelo menos uma interface do objeto.  
  
 Por exemplo, manter um pool de referências a objeto de criação de comando mantém ativas as conexões a esses objetos de sessão no pool. Como os objetos de sessão são necessários, o código de manutenção do pool passa um ponteiro de interface **IDBCreateCommand** válido para o método de aplicativo que solicita a sessão. Quando o método do aplicativo não necessita mais da sessão, o método retorna o ponteiro de interface para o código de manutenção do pool em vez de liberar a referência do aplicativo ao objeto de criação de comando.  
  
> [!NOTE]  
>  No exemplo anterior, a interface **IDBCreateCommand** é usada porque a interface **ICommand** implementa o método **GetDBSession**, o único método no escopo do comando ou do conjunto de linhas que permite que um objeto determine a sessão na qual ele foi criado. Portanto, um objeto de comando, e somente um objeto de comando, permite que um aplicativo recupere um ponteiro de objeto de fonte de dados a partir do qual outras sessões são criadas.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de fonte de dados &#40;OLE DB&#41;](data-source-objects-ole-db.md)  
  
  
