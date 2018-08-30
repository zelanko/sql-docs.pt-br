---
title: Suporte a colunas esparsas no OLE DB Driver for SQL Server | Microsoft Docs
description: Suporte ao UTF-16 no OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: a5bd68ec8035e9a0f52300ac486ad6942384325b
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43025147"
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>Suporte ao UTF-16 no OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] em diante, se você fornecer um buffer de comprimento fixo ao associar um resultado de coluna ou um parâmetro de saída e se o caractere **wchar** gravado no buffer antes do caractere de terminação for um ponto de código alternativo alto de um par alternativo e, se o próximo caractere **wchar** for um ponto de código alternativo baixo, o OLE DB Driver for SQL Server não adicionará o ponto de código alternativo alto ao buffer.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
