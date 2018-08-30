---
title: Microsoft OLE DB Driver for SQL Server | Microsoft Docs
description: Componentes do OLE DB Driver for SQL Server
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
- data access [OLE DB Driver for SQL Server], components
- components [OLE DB Driver for SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 2836438e6dc5eb501d67e724397acbdf1a0a956a
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43020665"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>Componentes do OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Driver do OLE DB para SQL Server contém os seguintes componentes:  

|Componente|Descrição|  
|---------------|-----------------|  
|msoledbsql.dll|O arquivo de biblioteca de vínculo dinâmico (DLL) que contém todos os o Driver OLE DB para a funcionalidade do SQL Server.|  
|msoledbsqlr.rll|O arquivo de recurso que acompanha este artigo para o Driver OLE DB para a biblioteca do SQL Server.|   
|msoledbsql.h|O Driver do OLE DB para o arquivo de cabeçalho do SQL Server que contém todas as novas definições necessárias para usar o Driver do OLE DB para SQL Server. Esse arquivo de cabeçalho substitui o arquivo de cabeçalho SQLOLEDB. h.<br /><br /> Observação: Você pode referenciar msoledbsql.h e SQLOLEDB. h no mesmo programa desde que SQLOLEDB. h é definida pela primeira vez.|  
|msoledbsql.lib|O arquivo de biblioteca necessário para chamar diretamente as [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) função que faz parte do que o Driver do OLE DB para SQL Server.<br /><br /> Observação: se você referenciar o arquivo msoledbsql.lib no código de programação, precisará garantir que o arquivo msoledbsql.dll está no caminho do sistema e no caminho do sistema dos usuários que usam o aplicativo.|  

## <a name="see-also"></a>Consulte Também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
