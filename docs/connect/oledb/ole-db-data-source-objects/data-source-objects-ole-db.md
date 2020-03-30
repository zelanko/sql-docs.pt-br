---
title: Objetos da fonte de dados (OLE DB) | Microsoft Docs
description: Objetos de fonte de dados (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
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
ms.author: pelopes
ms.openlocfilehash: e0394c5fd3b72c538904c9b8cf946316e76e6650
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015918"
---
# <a name="data-source-objects-ole-db"></a>Objetos de fonte de dados (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O OLE DB Driver for SQL Server usa o termo fonte de dados para o conjunto de interfaces OLE DB usadas para estabelecer um vínculo com um armazenamento de dados, como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A criação de uma instância do objeto de fonte de dados do provedor é a primeira tarefa de um Driver do OLE DB para SQL Server.  
  
 Todo provedor do OLE DB declara um identificador de classe (CLSID) para si mesmo. O CLSID para o Driver do OLE DB para SQL Server é o GUID do C/C++, CLSID_MSOLEDBSQL (o símbolo MSOLEDBSQL_CLSID será resolvido para o ProgID correto no arquivo msoledbsql.h referenciado). Com o CLSID, o consumidor usa a função **CoCreateInstance** do OLE para produzir uma instância do objeto de fonte de dados.  
  
 O Driver do OLE DB para SQL Server é um servidor em processo. As instâncias dos objetos do OLE DB Driver for SQL Server são criadas usando a macro CLSCTX_INPROC_SERVER para indicar o contexto executável.  
  
 O objeto da fonte de dados do OLE DB Driver for SQL Server expõe as interfaces de inicialização do OLE DB que permitem ao consumidor se conectar aos bancos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] existentes.  
  
 Toda conexão estabelecida por meio do Driver do OLE DB para SQL Server define estas opções automaticamente:  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 Este exemplo usa a macro de identificador de classe para criar um objeto de fonte de dados do OLE DB Driver for SQL Server e obter uma referência à sua interface **IDBInitialize**.  
  
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
  
 Com a criação bem-sucedida de uma instância de um objeto de fonte de dados do OLE DB Driver for SQL Server, o aplicativo de consumidor pode continuar inicializando a fonte de dados e criando sessões. As sessões de OLE DB apresentam as interfaces que permitem acesso e manipulação de dados.  
  
 O OLE DB Driver for SQL Server estabelece sua primeira conexão com uma instância especificada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como parte de uma inicialização de fonte de dados bem-sucedida. A conexão é mantida, desde que uma referência seja mantida em qualquer interface de inicialização de fonte de dados, ou até que o método **IDBInitialize::Uninitialize** seja chamado.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Propriedades de fonte de dados &#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [Propriedades de informações da fonte de dados](../../oledb/ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [Propriedades de inicialização e autorização](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [Sessões](../../oledb/ole-db-data-source-objects/sessions.md)  
  
-   [Propriedades de sessão – Driver do OLE DB para SQL Server](../../oledb/ole-db-data-source-objects/session-properties-oledb-driver-for-sql-server.md)  
  
-   [Objetos persistidos da fonte de dados](../../oledb/ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Programação no Driver do OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
