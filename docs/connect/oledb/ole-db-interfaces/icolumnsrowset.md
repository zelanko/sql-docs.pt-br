---
title: IColumnsRowset (driver do OLE DB) | Microsoft Docs
description: A coluna DBCOLUMN_BASETABLEINSTANCE em IColumnsRowset::GetColumnRowset é reservada para uso da Microsoft no Driver do OLE DB para SQL Server.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6de3b4f286f891d611b2b9b874b9101a9490903f
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860193"
---
# <a name="icolumnsrowset"></a>IColumnsRowset
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver do OLE DB para SQL Server acrescenta a coluna DBCOLUMN_BASETABLEINSTANCE a IColumnsRowset::GetColumnRowset. Essa coluna retorna DBTYPE_I2 e é reservada para uso pela Microsoft. As informações nessa coluna estão sujeitas à alteração em versões futuras.  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces do &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
