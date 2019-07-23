---
title: Como usar os arquivos de biblioteca e de cabeçalho do OLE DB Driver para SQL Server | Microsoft Docs
description: Usando os arquivos de biblioteca e de cabeçalho do OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 02/12/2019
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
ms.openlocfilehash: 93b906a0604772fe224b1e63eaf6eed9eb8af983
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989227"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>Usando os arquivos de biblioteca e de cabeçalho do OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O driver de OLE DB para SQL Server cabeçalho e arquivos de biblioteca são instalados quando a opção OLE DB driver for SQL Server SDK é selecionada durante o processo de instalação. Quando você for desenvolver um aplicativo, é importante copiar e instalar todos os arquivos necessários para o desenvolvimento no seu ambiente de desenvolvimento. Para obter mais informações sobre como instalar e redistribuir o driver de OLE DB para SQL Server, consulte Instalando o [Driver de OLE DB para SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md).  
  
 O driver de OLE DB para SQL Server cabeçalho e arquivos de biblioteca são instalados no seguinte local:  
  
 *%ARQUIVOS DE PROGRAMAS%* \Microsoft SQL Server\Client SDK\OLEDB\182\SDK  
  
 O driver de OLE DB para SQL Server arquivo de cabeçalho (msoledbsql. h) pode ser usado para adicionar o driver de OLE DB para SQL Server funcionalidade de acesso a dados aos seus aplicativos personalizados. O arquivo de cabeçalho do OLE DB Driver for SQL Server contém todas as definições, atributos, propriedades e interfaces necessárias para aproveitar os novos recursos introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Além do driver de OLE DB para SQL Server arquivo de cabeçalho, há também um arquivo de biblioteca msoledbsql. lib, que é a biblioteca de exportação para a funcionalidade [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) .  
  
 O arquivo de cabeçalho do OLE DB Driver for SQL Server tem compatibilidade com versões anteriores com o arquivo de cabeçalho sqloledb.h usado com o MDAC (Microsoft Data Access Components), mas não contém os CLSIDs para SQLOLEDB (o Provedor OLE DB para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornecido com o MDAC), nem símbolos para a funcionalidade de XML (para a qual não há suporte no OLE DB Driver for SQL Server).    
  
 OLE DB aplicativos que usam o driver OLE DB para SQL Server precisam apenas fazer referência a msoledbsql. h. Se um aplicativo usar o MDAC (SQLOLEDB) e o OLE DB Driver for SQL Server, ele poderá referenciar sqloledb.h e msoledbsql.h, mas a referência a sqloledb.h precisará vir primeiro.  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>Usando o driver de OLE DB para SQL Server arquivo de cabeçalho  
 Para usar o driver de OLE DB para SQL Server arquivo de cabeçalho, você deve usar uma instrução **include** no códigoC++ C/Programming. As seções a seguir descrevem como fazer isso em OLE DB aplicativos.  
  
> [!NOTE]  
>  O driver de OLE DB para arquivos de cabeçalho e biblioteca do SQL Server só pode ser compilado C++ usando o Visual Studio 2012 ou posterior.  
  
### <a name="ole-db"></a>OLE DB  
 Para usar o driver de OLE DB para SQL Server arquivo de cabeçalho em um aplicativo OLE DB, usando as seguintes linhas de código de programação:  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  Se o aplicativo tiver uma instrução **include** para SQLOLEDB. h, a instrução **include** para msoledbsql. h deverá vir depois dela.  
  
 Ao criar uma conexão com uma fonte de dados por meio do driver OLE DB para SQL Server, use "MSOLEDBSQL" como a cadeia de caracteres do nome do provedor.  

  
## <a name="component-names-and-properties-by-version"></a>Propriedades e nomes de componentes por versão  

|Propriedade|OLE DB Driver for SQL Server|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|Nome do arquivo de cabeçalho OLE DB|msoledbsql.h|Sqloledb.h|  
|DLL do provedor OLE DB|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>Vinculação estática e funções BCP  
 Quando um aplicativo usa funções BCP, é importante que ele especifique na cadeia de conexão o driver da mesma versão que a fornecida com o arquivo de cabeçalho e a biblioteca usada para compilar o aplicativo.  
  
 Para obter mais informações, consulte Executando [operações de cópia em massa](../../oledb/features/performing-bulk-copy-operations.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
