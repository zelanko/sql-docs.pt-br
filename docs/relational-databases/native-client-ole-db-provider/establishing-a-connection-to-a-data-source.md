---
description: Estabelecer conexão com a fonte de dados (provedor de OLE DB de cliente nativo)
title: Estabelecer conexão com a fonte de dados (provedor de OLE DB de cliente nativo) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [SQL Server Native Client]
- connections [SQL Server Native Client]
- SQL Server Native Client OLE DB provider, data source connections
- CoCreateInstance method
- OLE DB data sources [SQL Server Native Client]
ms.assetid: 7ebd1394-cc8d-4bcf-92f3-c374a26e7ba0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 384d6b0b9db152d1418b009c50345151786875e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490708"
---
# <a name="establishing-a-connection-to-a-sql-server-native-client-data-source"></a>Estabelecendo uma conexão com uma fonte de dados SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Para acessar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo, o consumidor deve primeiro criar uma instância de um objeto de fonte de dados chamando o método **CoCreateInstance** . Um CLSID (identificador de classe) exclusivo identifica cada provedor OLE DB. Para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo, o identificador de classe é CLSID_SQLNCLI10. Você também pode usar o símbolo SQLNCLI_CLSID que será resolvido para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo que é usado no sqlncli. h referenciado.  
  
 O objeto da fonte de dados expõe a interface **IDBProperties**, que é usada pelo consumidor para fornecer informações básicas de autenticação, como o nome do servidor, o nome do banco de dados, a ID de usuário e a senha. O método **IDBProperties::SetProperties** é chamado para definir essas propriedades.  
  
 Se houver várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução no computador, o nome do servidor será especificado como ServerName\InstanceName.  
  
 O objeto da fonte de dados também expõe a interface **IDBInitialize**. Depois que as propriedades são definidas, a conexão com a fonte de dados é estabelecida pela chamada ao método **IDBInitialize::Initialize**. Por exemplo:  
  
```  
CoCreateInstance(CLSID_SQLNCLI10,   
                 NULL,   
                 CLSCTX_INPROC_SERVER,  
                 IID_IDBInitialize,   
                 (void **) &pIDBInitialize)  
```  
  
 Essa chamada para **CoCreateInstance** cria um único objeto da classe associada ao CLSID_SQLNCLI10 (CSLID associado aos dados e ao código que será usado para criar o objeto). IID_IDBInitialize é uma referência ao identificador da interface (**IDBInitialize**) a ser usada para a comunicação com o objeto.  
  
 Segue uma função de exemplo que inicializa e estabelece uma conexão com a fonte de dados.  
  
```  
void InitializeAndEstablishConnection() {  
   // Initialize the COM library.  
   CoInitialize(NULL);  
  
   // Obtain access to the SQL Server Native Client OLE DB provider.  
   hr = CoCreateInstance(CLSID_SQLNCLI10,   
                         NULL,   
                         CLSCTX_INPROC_SERVER,  
                         IID_IDBInitialize,   
                         (void **) &pIDBInitialize);  
   // Initialize property values needed to establish connection.  
   for (i = 0 ; i < 4 ; i++)   
      VariantInit(&InitProperties[i].vValue);  
  
   // Server name.  
   // See DBPROP structure for more information on InitProperties  
   InitProperties[0].dwPropertyID  = DBPROP_INIT_DATASOURCE;  
   InitProperties[0].vValue.vt    = VT_BSTR;  
   InitProperties[0].vValue.bstrVal=   
                     SysAllocString(L"Server");  
   InitProperties[0].dwOptions    = DBPROPOPTIONS_REQUIRED;  
   InitProperties[0].colid       = DB_NULLID;  
  
   // Database.  
   InitProperties[1].dwPropertyID  = DBPROP_INIT_CATALOG;  
   InitProperties[1].vValue.vt    = VT_BSTR;  
   InitProperties[1].vValue.bstrVal= SysAllocString(L"database");  
   InitProperties[1].dwOptions    = DBPROPOPTIONS_REQUIRED;  
   InitProperties[1].colid       = DB_NULLID;  
  
   // Username (login).  
   InitProperties[2].dwPropertyID  = DBPROP_AUTH_INTEGRATED;  
   InitProperties[2].vValue.vt    = VT_BSTR;  
   InitProperties[2].vValue.bstrVal= SysAllocString(L"SSPI");  
   InitProperties[2].dwOptions    = DBPROPOPTIONS_REQUIRED;  
   InitProperties[2].colid       = DB_NULLID;  
   InitProperties[3].dwOptions    = DBPROPOPTIONS_REQUIRED;  
   InitProperties[3].colid       = DB_NULLID;  
  
   // Construct the DBPROPSET structure(rgInitPropSet). The   
   // DBPROPSET structure is used to pass an array of DBPROP   
   // structures (InitProperties) to the SetProperties method.  
   rgInitPropSet[0].guidPropertySet = DBPROPSET_DBINIT;  
   rgInitPropSet[0].cProperties   = 4;  
   rgInitPropSet[0].rgProperties   = InitProperties;  
  
   // Set initialization properties.  
   hr = pIDBInitialize->QueryInterface(IID_IDBProperties,   
                           (void **)&pIDBProperties);  
   hr = pIDBProperties->SetProperties(1, rgInitPropSet);   
   pIDBProperties->Release();  
  
   // Now establish the connection to the data source.  
   pIDBInitialize->Initialize();  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um aplicativo provedor OLE DB do SQL Server Native Client](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
