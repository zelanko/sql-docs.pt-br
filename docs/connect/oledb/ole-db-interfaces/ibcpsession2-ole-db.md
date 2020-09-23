---
title: IBCPSession2 (driver do OLE DB) | Microsoft Docs
description: Saiba mais sobre a interface IBCPSession2 no Driver do OLE DB para SQL Server, que fornece BCPSetBulkMode, uma alternativa a IBCPSession::BCPColFmt por coluna.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- IBCPSession2 interface
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 50cc43cec2e51162a887801bc52dcf34d4df26fa
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862320"
---
# <a name="ibcpsession2-ole-db"></a>IBCPSession2 (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  A interface IBCPSession2 é uma extensão de IBCPSession que fornece uma função de membro que é uma alternativa à chamada de IBCPSession::BCPColFmt para cada coluna.  IBCPSession2 herda de IBCPSession e adiciona um novo método: [IBCPSession2::BCPSetBulkMode](../../oledb/ole-db-interfaces/ibcpsession2-bcpsetbulkmode.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces do &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)
  
  
