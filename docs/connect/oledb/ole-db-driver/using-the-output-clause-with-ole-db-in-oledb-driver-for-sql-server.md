---
title: Usando a cláusula OUTPUT com o OLE DB no OLE DB Driver for SQL Server | Microsoft Docs
description: Saiba como usar a cláusula OUTPUT em um comando INSERT, UPDATE, DELETE ou MERGE no Driver do OLE DB para SQL Server.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1374dab2ac4954d173d8d131d59bfa4b39f2ad0a
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861511"
---
# <a name="using-the-output-clause-with-ole-db-in-ole-db-driver-for-sql-server"></a>Usar a cláusula OUTPUT com o OLE DB no OLE DB Driver for SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Se você usar uma cláusula OUTPUT em um comando INSERT, UPDATE, DELETE ou MERGE, a contagem de linhas afetadas não estará disponível. O aplicativo deve contar o número de linhas no conjunto de linhas retornado pela cláusula OUTPUT.  
  
## <a name="see-also"></a>Consulte Também  
 [Criação de aplicativo do Driver do OLE DB para SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md) 
  
  
