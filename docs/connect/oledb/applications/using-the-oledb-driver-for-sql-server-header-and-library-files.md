---
title: Usando o Driver do OLE DB para arquivos de biblioteca e cabeçalho do SQL Server | Microsoft Docs
description: Usando o Driver OLE DB para arquivos de biblioteca e cabeçalho do SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: f228442c31d754265769645a640b1eb1285c5897
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612141"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>Usando o Driver do OLE DB para arquivos de biblioteca e cabeçalho do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver OLE DB para arquivos de biblioteca e cabeçalho do SQL Server são instalados quando o Driver OLE DB para a opção de SDK do SQL Server é selecionado durante o processo de instalação. Quando você for desenvolver um aplicativo, é importante copiar e instalar todos os arquivos necessários para o desenvolvimento no seu ambiente de desenvolvimento. Para obter mais informações sobre como instalar e redistribuir o Driver do OLE DB para SQL Server, consulte [instalar o OLE DB Driver para SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md).  
  
 O Driver OLE DB para arquivos de biblioteca e cabeçalho do SQL Server são instalados no seguinte local:  
  
 *% ARQUIVOS de programas %* \Microsoft SQL Server\Client SDK\OLEDB\180\SDK  
  
 O Driver OLE DB para o arquivo de cabeçalho do SQL Server (msoledbsql.h) pode ser usado para adicionar o Driver do OLE DB para a funcionalidade de acesso de dados do SQL Server para seus aplicativos personalizados. O Driver OLE DB para o arquivo de cabeçalho do SQL Server contém todas as definições, atributos, propriedades e interfaces necessárias para tirar proveito dos novos recursos introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Além do OLE DB Driver para o arquivo de cabeçalho do SQL Server, também há um arquivo de biblioteca msoledbsql.lib que é a biblioteca de exportação para [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) funcionalidade.  
  
 O Driver OLE DB para o arquivo de cabeçalho do SQL Server é compatível com o arquivo de cabeçalho SQLOLEDB usado com o Microsoft Data Access Components (MDAC), mas não contém o CLSIDs para SQLOLEDB (o provedor OLE DB para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluído com o MDAC) ou símbolos para Funcionalidade XML (que não é suportada pelo Driver do OLE DB para SQL Server).    
  
 Aplicativos OLE DB que usam o Driver OLE DB para SQL Server só precisam referenciar msoledbsql.h. Se um aplicativo usa MDAC (SQLOLEDB) e o Driver OLE DB para SQL Server, ele pode fazer referência a SQLOLEDB e msoledbsql.h, mas a referência a SQLOLEDB deve vir primeira.  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>Usando o Driver do OLE DB para o arquivo de cabeçalho do SQL Server  
 Para usar o Driver OLE DB para o arquivo de cabeçalho do SQL Server, você deve usar um **incluem** instrução dentro de seu código de programação do C/C++. As seções a seguir descrevem como fazer isto aplicativos OLE DB.  
  
> [!NOTE]  
>  O Driver OLE DB para arquivos de biblioteca e cabeçalho do SQL Server só pode ser compilado usando o Visual Studio C++ 2012 ou posterior.  
  
### <a name="ole-db"></a>OLE DB  
 Para usar o Driver OLE DB para o arquivo de cabeçalho do SQL Server em um aplicativo OLE DB, usando as seguintes linhas de código de programação:  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  Se o aplicativo tiver um **incluem** instrução para SQLOLEDB, o **incluem** instrução para msoledbsql.h deve vir depois dela.  
  
 Ao criar uma conexão a uma fonte de dados por meio do Driver do OLE DB para SQL Server, use "MSOLEDBSQL" como a cadeia de caracteres de nome de provedor.  

  
## <a name="component-names-and-properties-by-version"></a>Propriedades e nomes de componentes por versão  

|Propriedade|Driver do OLE DB para SQL Server|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|Nome do arquivo de cabeçalho OLE DB|msoledbsql.h|Sqloledb.h|  
|DLL do provedor OLE DB|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>Vinculação estática e funções BCP  
 Quando um aplicativo usa funções BCP, é importante que ele especifique na cadeia de conexão o driver da mesma versão que a fornecida com o arquivo de cabeçalho e a biblioteca usada para compilar o aplicativo.  
  
 Para obter mais informações, consulte executando [executando operações de cópia em massa](../../oledb/features/performing-bulk-copy-operations.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
