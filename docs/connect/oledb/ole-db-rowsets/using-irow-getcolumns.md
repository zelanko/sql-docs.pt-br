---
title: Usar IRow::GetColumns | Microsoft Docs
description: Usar IRow::GetColumns para acessar todas as colunas em uma linha
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [OLE DB Driver for SQL Server]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: ddec5950f9dd8acc55c8bf1b6fe751bd0f34ac1f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015333"
---
# <a name="using-irowgetcolumns"></a>Usando IRow::GetColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  A implementação de **IRow** permite o acesso sequencial somente de encaminhamento às colunas. Acesse todas as colunas da linha com uma única chamada a **IRow::GetColumns** ou chame **IRow::GetColumns** várias vezes sempre que você acessar várias colunas na linha.  
  
 As várias chamadas a **IRow::GetColumns** não devem se sobrepor. Por exemplo, se a primeira chamada a **IRow::GetColumns** recupera as colunas 1, 2 e 3, a segunda chamada a **IRow::GetColumns** deve chamar as colunas 4, 5 e 6. Caso as chamadas posteriores a **IRow::GetColumns** se sobreponham, um sinalizador de status (campo dwstatus em DBCOLUMNACCESS) será definido como DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Consulte Também  
 [Buscando uma única linha com IRow](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
