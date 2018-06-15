---
title: Usando a cláusula OUTPUT com OLE DB em Driver do OLE DB para SQL Server | Microsoft Docs
description: Usando a cláusula OUTPUT com OLE DB em Driver OLE DB para SQL Server
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
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 8cf2e08b76636ab8509ab07fd1f3d60a102fa76d
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2018
ms.locfileid: "35665326"
---
# <a name="using-the-output-clause-with-ole-db-in-ole-db-driver-for-sql-server"></a>Usando a cláusula OUTPUT com OLE DB em Driver do OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Se você usar uma cláusula OUTPUT em um comando INSERT, UPDATE, DELETE ou MERGE, a contagem de linhas afetadas não estará disponível. O aplicativo deve contar o número de linhas no conjunto de linhas retornado pela cláusula OUTPUT.  
  
## <a name="see-also"></a>Consulte também  
 [Criação de aplicativo do Driver do OLE DB para SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md) 
  
  
