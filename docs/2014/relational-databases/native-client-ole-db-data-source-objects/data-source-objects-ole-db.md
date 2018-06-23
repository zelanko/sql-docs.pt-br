---
title: Fonte de dados de objetos (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], data source objects
- SQL Server Native Client, data source objects
- SQLNCLI, data source objects
- SQL Server Native Client OLE DB provider, data source objects
- OLE DB data source objects [SQL Server Native Client]
- data source objects [OLE DB]
- CLSID
ms.assetid: c1d4ed20-ad3b-4e33-a26b-38d7517237b7
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9f89825aaca32b542a6788fc9ef849975695f275
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115892"
---
# <a name="data-source-objects-ole-db"></a>Objetos de fonte de dados (OLE DB)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client usa a termo fonte de dados para o conjunto de interfaces de OLE DB usado para estabelecer um link para um repositório de dados, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A criação de uma instância do objeto de fonte de dados do provedor é a primeira tarefa de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor Native Client.  
  
 Todo provedor do OLE DB declara um identificador de classe (CLSID) para si mesmo. O CLSID para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider for o C/C++ GUID CLSID_SQLNCLI10 (o símbolo SQLNCLI_CLSID será resolvido para o correto progid no arquivo SQLNCLI. h que você faz referência). Com o CLSID, o consumidor usa o OLE **CoCreateInstance** função para produzir uma instância do objeto de fonte de dados.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client é um servidor em processo. Instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos do provedor OLE DB Native Client são criados usando a macro CLSCTX_INPROC_SERVER para indicar o contexto executável.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de fonte de dados do provedor OLE DB Native Client expõe as interfaces de inicialização do OLE DB que permitem ao consumidor para se conectar ao existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados.  
  
 Cada conexão feita por meio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client define estas opções automaticamente:  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 Este exemplo usa a macro de identificador de classe para criar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de fonte de dados do provedor OLE DB Native Client e obter uma referência ao seu **IDBInitialize** interface.  
  
```  
IDBInitialize*   pIDBInitialize;  
HRESULT          hr;  
  
hr = CoCreateInstance(CLSID_SQLNCLI10, NULL, CLSCTX_INPROC_SERVER,  
    IID_IDBInitialize, (void**) &pIDBInitialize);  
  
if (SUCCEEDED(hr))  
{  
    //  Perform necessary processing with the interface.  
    pIDBInitialize->Uninitialize();  
    pIDBInitialize->Release();  
}  
else  
{  
    // Display error from CoCreateInstance.  
}  
```  
  
 Com a criação bem-sucedida de uma instância de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de fonte de dados do provedor de OLE DB Native Client, o aplicativo de consumidor pode continuar Inicializando a fonte de dados e Criando sessões. As sessões de OLE DB apresentam as interfaces que permitem acesso e manipulação de dados.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB Native Client torna sua primeira conexão com uma instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como parte de uma inicialização de fonte de dados com êxito. A conexão é mantida como uma referência seja mantida em qualquer interface de inicialização de fonte de dados, ou até que o **IDBInitialize:: Uninitialize** método é chamado.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Propriedades da fonte de dados &#40;OLE DB&#41;](data-source-properties-ole-db.md)  
  
-   [Propriedades de informações da fonte de dados](data-source-information-properties.md)  
  
-   [Propriedades de inicialização e autorização](initialization-and-authorization-properties.md)  
  
-   [Sessões](sessions.md)  
  
-   [Propriedades da sessão](session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [Objetos persistidos da fonte de dados](persisted-data-source-objects.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  