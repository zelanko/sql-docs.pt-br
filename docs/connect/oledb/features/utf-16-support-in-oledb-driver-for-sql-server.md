---
title: Compatibilidade de UTF-16 com OLE DB Driver para SQL Server| Microsoft Docs
description: Suporte ao UTF-16 no OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 0ae8a83de24341b7f9672296a9bfe713ae882dfe
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67988765"
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>Suporte ao UTF-16 no OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] em diante, se você fornecer um buffer de comprimento fixo ao associar um resultado de coluna ou um parâmetro de saída e se o caractere **wchar** gravado no buffer antes do caractere de terminação for um ponto de código alternativo alto de um par alternativo e, se o próximo caractere **wchar** for um ponto de código alternativo baixo, o OLE DB Driver for SQL Server não adicionará o ponto de código alternativo alto ao buffer.  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
