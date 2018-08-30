---
title: Estabelecer uma Conexão a uma fonte de dados | Microsoft Docs
description: Estabelecer uma conexão a uma fonte de dados usando o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data sources [OLE DB Driver for SQL Server]
- connections [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, data source connections
- CoCreateInstance method
- OLE DB data sources [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: f80f7ad4b52d7783ae5745de88b29bc8f8203eaf
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43037775"
---
# <a name="establishing-a-connection-to-a-data-source"></a>Estabelecendo uma conexão com uma fonte de dados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Para acessar o OLE DB Driver for SQL Server, primeiro, o consumidor precisa criar uma instância de um objeto de fonte de dados chamando o método **CoCreateInstance**. Um CLSID (identificador de classe) exclusivo identifica cada provedor OLE DB. Para o Driver do OLE DB para SQL Server, o identificador de classe é CLSID_MSOLEDBSQL. Você também pode usar o símbolo MSOLEDBSQL_CLSID será resolvido para o Driver do OLE DB para SQL Server que é usado em msoledbsql.h o que você faz referência.  
  
 O objeto da fonte de dados expõe a interface **IDBProperties**, que é usada pelo consumidor para fornecer informações básicas de autenticação, como o nome do servidor, o nome do banco de dados, a ID de usuário e a senha. O método **IDBProperties::SetProperties** é chamado para definir essas propriedades.  
  
 Se houver várias instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em execução no computador, o nome do servidor será especificado como ServerName\InstanceName.  
  
 O objeto da fonte de dados também expõe a interface **IDBInitialize**. Depois que as propriedades são definidas, a conexão com a fonte de dados é estabelecida pela chamada ao método **IDBInitialize::Initialize**. Por exemplo:  
  
```cpp
CoCreateInstance(CLSID_MSOLEDBSQL,   
                 NULL,   
                 CLSCTX_INPROC_SERVER,  
                 IID_IDBInitialize,   
                 (void **) &pIDBInitialize)  
```
  
 Essa chamada a **CoCreateInstance** cria um único objeto da classe associada a CLSID_MSOLEDBSQL (CSLID associado aos dados e ao código que serão usados para criar o objeto). IID_IDBInitialize é uma referência ao identificador da interface (**IDBInitialize**) a ser usada para a comunicação com o objeto.  
  
 O exemplo a seguir mostra como inicializar e estabelecer uma conexão à fonte de dados.
  
```cpp
#include "msoledbsql.h"
#include <stdio.h>

HRESULT InitializeAndEstablishConnection(IDBInitialize *&pIDBInitialize);

void main() {
    IDBInitialize       *pIDBInitialize = nullptr;
    HRESULT             hr = S_OK;

    // Initialize The Component Object Module Library
    CoInitialize(nullptr);

    hr = InitializeAndEstablishConnection(pIDBInitialize);
    if (FAILED(hr)) {
        printf("Failed to establish connection.\r\n");
        goto _ExitMain;
    }

    // Insert code that uses the established connection

_ExitMain:
    // Free Up All Allocated Memory
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
        pIDBInitialize = nullptr;
    }

    // Release The Component Object Module Library
    CoUninitialize();
}

HRESULT InitializeAndEstablishConnection(IDBInitialize *&pIDBInitialize) {
    IDBProperties   *pIDBProperties = nullptr;
    DBPROP          InitProperties[3] = { 0 };
    DBPROPSET       rgInitPropSet[1] = { 0 };
    HRESULT         hr = S_OK;

    // Obtain access to the OLE DB Driver for SQL Server.  
    hr = CoCreateInstance(CLSID_MSOLEDBSQL,
                          NULL,
                          CLSCTX_INPROC_SERVER,
                          IID_IDBInitialize,
                          (void **)&pIDBInitialize);
    if (FAILED(hr)) {
        printf("Failed to obtain access to the OLE DB Driver.\r\n");
        goto _ExitInitialize;
    }
    // Initialize property values needed to establish connection.  
    for (int i = 0; i < 3; i++) {
        VariantInit(&InitProperties[i].vValue);
    }

    // Server name.  
    // See DBPROP structure for more information on InitProperties  
    InitProperties[0].dwPropertyID = DBPROP_INIT_DATASOURCE;
    InitProperties[0].vValue.vt = VT_BSTR;
    InitProperties[0].vValue.bstrVal = SysAllocString(L"Server");
    InitProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;
    InitProperties[0].colid = DB_NULLID;

    // Database.  
    InitProperties[1].dwPropertyID = DBPROP_INIT_CATALOG;
    InitProperties[1].vValue.vt = VT_BSTR;
    InitProperties[1].vValue.bstrVal = SysAllocString(L"database");
    InitProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;
    InitProperties[1].colid = DB_NULLID;

    // Username (login).  
    InitProperties[2].dwPropertyID = DBPROP_AUTH_INTEGRATED;
    InitProperties[2].vValue.vt = VT_BSTR;
    InitProperties[2].vValue.bstrVal = SysAllocString(L"SSPI");
    InitProperties[2].dwOptions = DBPROPOPTIONS_REQUIRED;
    InitProperties[2].colid = DB_NULLID;

    // Construct the DBPROPSET structure(rgInitPropSet). The   
    // DBPROPSET structure is used to pass an array of DBPROP   
    // structures (InitProperties) to the SetProperties method.  
    rgInitPropSet[0].guidPropertySet = DBPROPSET_DBINIT;
    rgInitPropSet[0].cProperties = 3;
    rgInitPropSet[0].rgProperties = InitProperties;

    // Set initialization properties.  
    hr = pIDBInitialize->QueryInterface(IID_IDBProperties,
                                        (void **)&pIDBProperties);
    if (FAILED(hr)) {
        printf("Failed to obtain an IDBProperties interface.\r\n");
        goto _ExitInitialize;
    }
    hr = pIDBProperties->SetProperties(1, rgInitPropSet);
    if (FAILED(hr)) {
        printf("Failed to set initialization properties.\r\n");
        goto _ExitInitialize;
    }

    // Now establish the connection to the data source.  
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr)) {
        printf("Failed to establish connection with the server.\r\n");
        goto _ExitInitialize;
    }

_ExitInitialize:
    if (pIDBProperties)
    {
        pIDBProperties->Release();
        pIDBProperties = nullptr;
    }

    if (FAILED(hr))
    {
        if (pIDBInitialize)
        {
            pIDBInitialize->Release();
            pIDBInitialize = nullptr;
        }
    }

    return hr;
}
```  
  
## <a name="see-also"></a>Consulte Também  
 [Criação de aplicativo do Driver do OLE DB para SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)  
  
  
