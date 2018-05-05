---
title: Fonte de dados de objetos (OLE DB) | Microsoft Docs
description: Objetos de fonte de dados (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], data source objects
- OLE DB Driver for SQL Server, data source objects
- MSOLEDBSQL, data source objects
- OLE DB Driver for SQL Server, data source objects
- OLE DB data source objects [OLE DB Driver for SQL Server]
- data source objects [OLE DB]
- CLSID
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 2eb3583366cf896ecf2382a5d2f36d1298e4c4a4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-objects-ole-db"></a>Objetos de fonte de dados (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB Driver para SQL Server usa a termo fonte de dados para o conjunto de interfaces de OLE DB usado para estabelecer um link para um repositório de dados, como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Criar uma instância do objeto de fonte de dados do provedor é a primeira tarefa de um Driver OLE DB para o consumidor do SQL Server.  
  
 Todo provedor do OLE DB declara um identificador de classe (CLSID) para si mesmo. O CLSID para o Driver OLE DB para SQL Server é o C/C++ GUID CLSID_MSOLEDBSQL (o símbolo MSOLEDBSQL_CLSID será resolvido para o correto progid no arquivo msoledbsql.h referenciado). Com o CLSID, o consumidor usa o OLE **CoCreateInstance** função para produzir uma instância do objeto de fonte de dados.  
  
 OLE DB Driver para SQL Server é um servidor em processo. Instâncias do Driver do OLE DB para objetos do SQL Server são criadas usando a macro CLSCTX_INPROC_SERVER para indicar o contexto executável.  
  
 O Driver OLE DB para o objeto de fonte de dados do SQL Server expõe as interfaces de inicialização do OLE DB que permitem ao consumidor para se conectar ao existente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bancos de dados.  
  
 Cada conexão feita por meio do Driver OLE DB para SQL Server define estas opções automaticamente:  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 Este exemplo usa a macro de identificador de classe para criar um Driver OLE DB para o objeto de fonte de dados do SQL Server e obtém uma referência ao seu **IDBInitialize** interface.  
  
```  
IDBInitialize*   pIDBInitialize;  
HRESULT          hr;  
  
hr = CoCreateInstance(CLSID_MSOLEDBSQL, NULL, CLSCTX_INPROC_SERVER,  
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
  
 Com a criação bem-sucedida de uma instância de um Driver OLE DB para o objeto de fonte de dados do SQL Server, o aplicativo de consumidor pode continuar Inicializando a fonte de dados e Criando sessões. As sessões de OLE DB apresentam as interfaces que permitem acesso e manipulação de dados.  
  
 O Driver OLE DB para SQL Server torna sua primeira conexão com uma instância especificada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como parte de uma inicialização de fonte de dados com êxito. A conexão é mantida como uma referência seja mantida em qualquer interface de inicialização de fonte de dados, ou até que o **IDBInitialize:: Uninitialize** método é chamado.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Propriedades da fonte de dados & #40; OLE DB & #41;](../../oledb/ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [Propriedades de informações de fonte de dados](../../oledb/ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [Propriedades de inicialização e autorização](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [Sessões](../../oledb/ole-db-data-source-objects/sessions.md)  
  
-   [Propriedades de sessão – Driver do OLE DB para SQL Server](../../oledb/ole-db-data-source-objects/session-properties-oledb-driver-for-sql-server.md)  
  
-   [Persistente de objetos de fonte de dados](../../oledb/ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>Consulte também  
 [Programação no Driver do OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
