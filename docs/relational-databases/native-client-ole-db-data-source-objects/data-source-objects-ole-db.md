---
title: Objetos da fonte de dados (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d8bb984c789f759eb764ad580f971ab71c9fc946
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297616"
---
# <a name="data-source-objects-ole-db"></a>Objetos de fonte de dados (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O Cliente Nativo usa o termo fonte de dados para o conjunto de interfaces [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]OLE DB usadas para estabelecer um link para um armazenamento de dados, como . Criar uma instância do objeto de origem de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do provedor é a primeira tarefa de um consumidor cliente nativo.  
  
 Todo provedor do OLE DB declara um identificador de classe (CLSID) para si mesmo. O CLSID [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o provedor Native Client OLE DB é o c/C++ GUID CLSID_SQLNCLI10 (o símbolo SQLNCLI_CLSID resolverá para o progid correto no arquivo sqlncli.h que você faz referência). Com o CLSID, o consumidor usa a função **CoCreateInstance** do OLE para produzir uma instância do objeto de fonte de dados.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client é um servidor em processo. As [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instâncias dos objetos do provedor Nativo Cliente OLE DB são criadas usando a CLSCTX_INPROC_SERVER macro para indicar o contexto executável.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de origem de dados do provedor Cliente Nativo OLE DB expõe as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces de inicialização do OLE DB que permitem ao consumidor se conectar aos bancos de dados existentes.  
  
 Cada conexão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] feita através do provedor Native Client OLE DB define essas opções automaticamente:  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 Este exemplo usa a macro identificador de classe para criar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de origem de dados do provedor Decliente Nativo OLE DB e obter uma referência à sua interface **IDBInitialize.**  
  
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
  
 Com a criação bem-sucedida de uma instância de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de origem de dados do provedor DeLE DB do Cliente Nativo, o aplicativo do consumidor pode continuar iniciando a fonte de dados e criando sessões. As sessões de OLE DB apresentam as interfaces que permitem acesso e manipulação de dados.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Nativo Cliente OLE DB faz sua [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] primeira conexão a uma instância especificada como parte de uma inicialização de origem de dados bem-sucedida. A conexão é mantida, desde que uma referência seja mantida em qualquer interface de inicialização de fonte de dados, ou até que o método **IDBInitialize::Uninitialize** seja chamado.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Propriedades de fonte de dados &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [Propriedades de informações da fonte de dados](../../relational-databases/native-client-ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [Propriedades de inicialização e autorização](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [Sessões](../../relational-databases/native-client-ole-db-data-source-objects/sessions.md)  
  
-   [Propriedades da sessão – Provedor OLE DB do SQL Server Native Client](../../relational-databases/native-client-ole-db-data-source-objects/session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [Objetos persistidos da fonte de dados](../../relational-databases/native-client-ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
