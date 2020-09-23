---
title: Componentes do OLE DB Driver para SQL Server | Microsoft Docs
description: Saiba mais sobre os componentes do Driver do OLE DB para SQL Server, incluindo a biblioteca que contém a funcionalidade do driver, outras bibliotecas e um arquivo de cabeçalho.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], components
- components [OLE DB Driver for SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fa548f34701565a5fcfd836232544bc0ee1345f4
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862061"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>Componentes do OLE DB Driver for SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver do OLE DB para SQL Server contém os seguintes componentes:  

|Componente|Descrição|  
|---------------|-----------------|  
|msoledbsql.dll|O arquivo de biblioteca de vínculo dinâmico (DLL) que contém toda a funcionalidade do Driver do OLE DB para SQL Server.|  
|msoledbsqlr.rll|O arquivo de recursos que acompanha a biblioteca do Driver do OLE DB para SQL Server.|   
|msoledbsql.h|O arquivo de cabeçalho do Driver do OLE DB para SQL Server que contém todas as novas definições necessárias para usar o Driver do OLE DB para SQL Server. Esse arquivo de cabeçalho substitui o arquivo de cabeçalho sqloledb.h.<br /><br /> Observação: você pode fazer referência a msoledbsql.h e sqloledb.h no mesmo programa, contanto que sqloledb.h seja definido primeiro.|  
|msoledbsql.lib|O arquivo de biblioteca necessário para chamar diretamente a função [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) que faz parte do Driver do OLE DB para SQL Server.<br /><br /> Observação: se você referenciar o arquivo msoledbsql.lib no código de programação, precisará garantir que o arquivo msoledbsql.dll está no caminho do sistema e no caminho do sistema dos usuários que usam o aplicativo.|  

## <a name="see-also"></a>Consulte Também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
