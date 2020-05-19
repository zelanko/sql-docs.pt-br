---
title: Objetos da fonte de dados (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ede861a696ba7782f7cdce962578dc077f799b33
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707432"
---
# <a name="data-source-objects-ole-db"></a>Objetos de fonte de dados (OLE DB)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O Native Client usa a fonte de dados do termo para o conjunto de interfaces OLE DB usadas para estabelecer um link para um armazenamento de dados, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A criação de uma instância do objeto de fonte de dados do provedor é a primeira tarefa de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor cliente nativo.  
  
 Todo provedor do OLE DB declara um identificador de classe (CLSID) para si mesmo. O CLSID para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo é o CLSID_SQLNCLI10 de GUID C/C++ (o símbolo SQLNCLI_CLSID será resolvido para o ProgID correto no arquivo sqlncli. h que você referencia). Com o CLSID, o consumidor usa a função **CoCreateInstance** do OLE para produzir uma instância do objeto de fonte de dados.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O Native Client é um servidor em processo. Instâncias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos do provedor de OLE DB de clientes nativos são criadas usando a macro CLSCTX_INPROC_SERVER para indicar o contexto do executável.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de fonte de dados do provedor de OLE DB de cliente nativo expõe as interfaces de inicialização OLE DB que permitem que o consumidor se conecte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados existentes.  
  
 Todas as conexões feitas por meio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo define essas opções automaticamente:  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 Este exemplo usa a macro identificador de classe para criar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de fonte de dados de provedor de OLE DB de cliente nativo e obter uma referência para sua interface **IDBInitialize** .  
  
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
  
 Com a criação bem-sucedida de uma instância de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de fonte de dados de provedor de OLE DB de cliente nativo, o aplicativo de consumidor pode continuar inicializando a fonte de dados e criando sessões. As sessões de OLE DB apresentam as interfaces que permitem acesso e manipulação de dados.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo faz sua primeira conexão com uma instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como parte de uma inicialização de fonte de dados bem-sucedida. A conexão é mantida, desde que uma referência seja mantida em qualquer interface de inicialização de fonte de dados, ou até que o método **IDBInitialize::Uninitialize** seja chamado.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Propriedades de fonte de dados &#40;OLE DB&#41;](data-source-properties-ole-db.md)  
  
-   [Propriedades de informações da fonte de dados](data-source-information-properties.md)  
  
-   [Propriedades de inicialização e autorização](initialization-and-authorization-properties.md)  
  
-   [Sessões](sessions.md)  
  
-   [Propriedades da sessão](session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [Objetos persistidos da fonte de dados](persisted-data-source-objects.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
