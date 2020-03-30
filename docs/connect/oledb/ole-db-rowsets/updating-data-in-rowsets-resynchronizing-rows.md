---
title: Ressincronizar linhas | Microsoft Docs
description: Ressincronizar linhas usando o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 2f1ea1a563e986914c5fe820740776da129c3b28
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67994167"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>Atualizar dados em conjuntos de linhas – ressincronizar linhas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver do OLE DB para SQL Server dá suporte a **IRowsetResynch** somente em conjuntos de linhas com suporte em cursores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **IRowsetResynch** não está disponível sob demanda. O consumidor deve solicitar a interface antes de abrir o conjunto de linhas.  
  
## <a name="see-also"></a>Consulte Também  
 [Atualizando dados em conjuntos de linhas](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
