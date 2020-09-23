---
title: Como usar os arquivos de biblioteca e de cabeçalho do OLE DB Driver para SQL Server | Microsoft Docs
description: Saiba como usar os arquivos de cabeçalho e de biblioteca do Driver do OLE DB para SQL Server em seu ambiente de desenvolvimento.
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 66870fbbc20d22067f00a8ced721cb63c331eb2f
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861642"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>Usando os arquivos de biblioteca e de cabeçalho do OLE DB Driver for SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O cabeçalho e os arquivos de biblioteca do Driver do OLE DB para SQL Server são instalados quando a opção de SDK do Driver do OLE DB para SQL Server é selecionada durante o processo de instalação. Quando você for desenvolver um aplicativo, é importante copiar e instalar todos os arquivos necessários para o desenvolvimento no seu ambiente de desenvolvimento. Para obter mais informações sobre como instalar e redistribuir o Driver do OLE DB para SQL Server, confira [Como instalar o Driver do OLE DB para SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md).  
  
 Os arquivos de biblioteca e de cabeçalho do Driver do OLE DB para SQL Server são instalados na seguinte localização:  
  
 *%ARQUIVOS DE PROGRAMAS%* \Microsoft SQL Server\Client SDK\OLEDB\182\SDK  
  
 O arquivo de cabeçalho do Driver do OLE DB para SQL Server (msoledbsql.h) pode ser usado para adicionar a funcionalidade de acesso a dados do Driver do OLE DB para SQL Server aos seus aplicativos personalizados. O arquivo de cabeçalho do OLE DB Driver for SQL Server contém todas as definições, atributos, propriedades e interfaces necessárias para aproveitar os novos recursos introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Além do arquivo de cabeçalho do Driver do OLE DB para SQL Server, há também um arquivo de biblioteca msoledbsql.lib, que é a biblioteca de exportação para a funcionalidade [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md).  
  
 O arquivo de cabeçalho do OLE DB Driver for SQL Server tem compatibilidade com versões anteriores com o arquivo de cabeçalho sqloledb.h usado com o MDAC (Microsoft Data Access Components), mas não contém os CLSIDs para SQLOLEDB (o Provedor OLE DB para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornecido com o MDAC), nem símbolos para a funcionalidade de XML (para a qual não há suporte no OLE DB Driver for SQL Server).    
  
 Aplicativos OLE DB que usam o Driver do OLE DB para SQL Server precisam apenas fazer referência a msoledbsql.h. Se um aplicativo usar o MDAC (SQLOLEDB) e o OLE DB Driver for SQL Server, ele poderá referenciar sqloledb.h e msoledbsql.h, mas a referência a sqloledb.h precisará vir primeiro.  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>Usar o arquivo de cabeçalho do Driver do OLE DB para SQL Server  
 Para usar o arquivo de cabeçalho do Driver do OLE DB para SQL Server, você precisa usar uma instrução **include** no seu código de programação C/C++. As seções a seguir descrevem como fazer isso em aplicativos OLE DB.  
  
> [!NOTE]  
>  Os arquivos de cabeçalho e de biblioteca do Driver do OLE DB para SQL Server podem ser compilados apenas usando o Visual Studio C++ 2012 ou posterior.  
  
### <a name="ole-db"></a>OLE DB  
 Para usar o arquivo de cabeçalho do Driver do OLE DB para SQL Server em um aplicativo OLE DB usando as seguintes linhas do código de programação:  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  Além disso, se o aplicativo tiver uma instrução **include** para sqloledb.h, a instrução **include** para sqlncli.h precisará vir depois dela.  
  
 Ao criar uma conexão com uma fonte de dados por meio do Driver do OLE DB para SQL Server, use "MSOLEDBSQL" como a cadeia de caracteres de nome do provedor.  

  
## <a name="component-names-and-properties-by-version"></a>Propriedades e nomes de componentes por versão  

|Propriedade|OLE DB Driver for SQL Server|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|Nome do arquivo de cabeçalho OLE DB|msoledbsql.h|Sqloledb.h|  
|DLL do provedor OLE DB|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>Vinculação estática e funções BCP  
 Quando um aplicativo usa funções BCP, é importante que ele especifique na cadeia de conexão o driver da mesma versão que a fornecida com o arquivo de cabeçalho e a biblioteca usada para compilar o aplicativo.  
  
 Para obter mais informações, confira [Como realizar operações de cópia em massa](../../oledb/features/performing-bulk-copy-operations.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
