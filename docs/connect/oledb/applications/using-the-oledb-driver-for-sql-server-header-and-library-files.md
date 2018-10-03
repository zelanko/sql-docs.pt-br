---
title: Usando os arquivos de biblioteca e de cabeçalho do OLE DB Driver for SQL Server | Microsoft Docs
description: Usando os arquivos de biblioteca e de cabeçalho do OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- header files [OLE DB Driver for SQL Server]
- MSOLEDBSQL, header files
- OLE DB, header files
- library files [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, header files
- data access [OLE DB Driver for SQL Server], header files
- data access [OLE DB Driver for SQL Server], library files
- OLE DB Driver for SQL Server, library files
- MSOLEDBSQL, library files
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 9cd6a50bec611b7068b3f79f3867f9e2a6242a70
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47816034"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>Usar os arquivos de biblioteca e de cabeçalho do OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver OLE DB para arquivos de biblioteca e cabeçalho do SQL Server são instalados quando o Driver do OLE DB para a opção de SDK do SQL Server é selecionado durante o processo de instalação. Quando você for desenvolver um aplicativo, é importante copiar e instalar todos os arquivos necessários para o desenvolvimento no seu ambiente de desenvolvimento. Para obter mais informações sobre como instalar e redistribuir o Driver do OLE DB para SQL Server, consulte [instalar o Driver do OLE DB para SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md).  
  
 O Driver OLE DB para arquivos de biblioteca e cabeçalho do SQL Server são instalados no seguinte local:  
  
 *% ARQUIVOS de programas %* \Microsoft SQL Server\Client SDK\OLEDB\181\SDK  
  
 O Driver OLE DB para o arquivo de cabeçalho do SQL Server (msoledbsql.h) pode ser usado para adicionar o Driver do OLE DB para a funcionalidade de acesso de dados do SQL Server para seus aplicativos personalizados. O arquivo de cabeçalho do OLE DB Driver for SQL Server contém todas as definições, atributos, propriedades e interfaces necessárias para aproveitar os novos recursos introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Além do Driver do OLE DB para o arquivo de cabeçalho do SQL Server, também há um arquivo de biblioteca msoledbsql.lib que é a biblioteca de exportação para [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) funcionalidade.  
  
 O arquivo de cabeçalho do OLE DB Driver for SQL Server tem compatibilidade com versões anteriores com o arquivo de cabeçalho sqloledb.h usado com o MDAC (Microsoft Data Access Components), mas não contém os CLSIDs para SQLOLEDB (o Provedor OLE DB para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornecido com o MDAC), nem símbolos para a funcionalidade de XML (para a qual não há suporte no OLE DB Driver for SQL Server).    
  
 Aplicativos OLE DB que usam o Driver do OLE DB para SQL Server só precisam fazer referência msoledbsql.h. Se um aplicativo usar o MDAC (SQLOLEDB) e o OLE DB Driver for SQL Server, ele poderá referenciar sqloledb.h e msoledbsql.h, mas a referência a sqloledb.h precisará vir primeiro.  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>Usando o Driver do OLE DB para o arquivo de cabeçalho do SQL Server  
 Para usar o Driver do OLE DB para o arquivo de cabeçalho do SQL Server, você deve usar um **incluem** instrução dentro do seu código de programação do C/C++. As seções a seguir descrevem como fazer essa aplicativos OLE DB.  
  
> [!NOTE]  
>  O Driver OLE DB para arquivos de biblioteca e cabeçalho do SQL Server só pode ser compilado usando o Visual Studio C++ 2012 ou posterior.  
  
### <a name="ole-db"></a>OLE DB  
 Para usar o Driver do OLE DB para o arquivo de cabeçalho do SQL Server em um aplicativo OLE DB, usando as seguintes linhas de código de programação:  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  Se o aplicativo tem um **incluem** instrução para SQLOLEDB. h, o **incluem** instrução para msoledbsql.h deve vir depois dela.  
  
 Ao criar uma conexão a uma fonte de dados por meio do Driver do OLE DB para SQL Server, use "MSOLEDBSQL" como a cadeia de caracteres de nome do provedor.  

  
## <a name="component-names-and-properties-by-version"></a>Propriedades e nomes de componentes por versão  

|Propriedade|OLE DB Driver for SQL Server|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|Nome do arquivo de cabeçalho OLE DB|msoledbsql.h|Sqloledb.h|  
|DLL do provedor OLE DB|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>Vinculação estática e funções BCP  
 Quando um aplicativo usa funções BCP, é importante que ele especifique na cadeia de conexão o driver da mesma versão que a fornecida com o arquivo de cabeçalho e a biblioteca usada para compilar o aplicativo.  
  
 Para obter mais informações, consulte executando [executando operações de cópia em massa](../../oledb/features/performing-bulk-copy-operations.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
