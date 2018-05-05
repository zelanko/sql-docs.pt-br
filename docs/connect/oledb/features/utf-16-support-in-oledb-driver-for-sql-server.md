---
title: Suporte a UTF-16 no Driver do OLE DB para SQL Server | Microsoft Docs
description: Suporte a UTF-16 no Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 3882e5b5116af5866410be0b309b54eb48e91902
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>Suporte a UTF-16 no Driver do OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A partir do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], se você fornecer um buffer de comprimento fixo ao associar um coluna de resultados ou parâmetro de saída e se o **wchar** caractere gravado no buffer antes da finalização do caractere é um ponto de código alternativo alto de um substitutos de par e se o próximo **wchar** caractere é um ponto de código alternativo baixo, OLE DB Driver para SQL Server não adicionará o ponto de código alternativo alto ao buffer.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
