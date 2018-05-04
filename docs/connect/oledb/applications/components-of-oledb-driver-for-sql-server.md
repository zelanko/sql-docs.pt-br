---
title: Componentes do Driver do OLE DB para SQL Server | Microsoft Docs
description: Componentes do Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], components
- components [OLE DB Driver for SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 83ac9f1e36172d6af5a7b55909e2a73bee7f81a8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>Componentes do Driver do OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver para SQL Server contém os seguintes componentes:  

|Componente|Description|  
|---------------|-----------------|  
|msoledbsql.dll|O arquivo de biblioteca de vínculo dinâmico (DLL) que contém todos os Driver OLE DB para a funcionalidade do SQL Server.|  
|msoledbsqlr.rll|O arquivo de recurso fornecido para o Driver OLE DB para a biblioteca do SQL Server.|   
|msoledbsql.h|O Driver OLE DB para o arquivo de cabeçalho do SQL Server que contém todas as novas definições necessárias para usar o Driver do OLE DB para SQL Server. Esse arquivo de cabeçalho substitui o arquivo de cabeçalho SQLOLEDB.<br /><br /> Observação: Você pode referenciar msoledbsql.h e SQLOLEDB no mesmo programa desde que SQLOLEDB é definido pela primeira vez.|  
|msoledbsql.lib|O arquivo de biblioteca necessário para chamar diretamente o [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) função que faz parte do Driver OLE DB para SQL Server.<br /><br /> Observação: Se você referenciar o arquivo de msoledbsql.lib no código de programação, você precisa certificar-se de que o arquivo de msoledbsql.dll está no caminho do sistema e no caminho do sistema dos usuários que usam o seu aplicativo.|  

## <a name="see-also"></a>Consulte também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
