---
title: Usando a cláusula OUTPUT com o OLE DB no OLE DB Driver for SQL Server | Microsoft Docs
description: Usando a cláusula OUTPUT com o OLE DB no OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 2beec79ba9bb8800b1e87742cc9bed91ad784f26
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798118"
---
# <a name="using-the-output-clause-with-ole-db-in-ole-db-driver-for-sql-server"></a>Usar a cláusula OUTPUT com o OLE DB no OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Se você usar uma cláusula OUTPUT em um comando INSERT, UPDATE, DELETE ou MERGE, a contagem de linhas afetadas não estará disponível. O aplicativo deve contar o número de linhas no conjunto de linhas retornado pela cláusula OUTPUT.  
  
## <a name="see-also"></a>Consulte Também  
 [Criação de aplicativo do Driver do OLE DB para SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md) 
  
  
