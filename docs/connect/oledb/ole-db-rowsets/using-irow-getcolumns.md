---
title: 'Usando IRow:: Getcolumns | Microsoft Docs'
description: 'Usando IRow:: Getcolumns para acessar todas as colunas em uma linha'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [OLE DB Driver for SQL Server]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b18b256d859c85b846d81ae239003fec2aafc010
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="using-irowgetcolumns"></a>Usando IRow::GetColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O **IRow** implementação permite acesso sequencial somente de encaminhamento para as colunas. Você pode acessar todas as colunas na linha com uma única chamada para **IRow:: Getcolumns** ou chame **IRow:: Getcolumns** várias vezes sempre que você acessa várias colunas na linha.  
  
 As várias chamadas para **IRow:: Getcolumns** não devem se sobrepor. Por exemplo, se a primeira chamada para **IRow:: Getcolumns** recupera colunas 1, 2 e 3, a segunda chamada para **IRow:: Getcolumns** deve chamar as colunas 4, 5 e 6. Se chamadas posteriores para **IRow:: Getcolumns** se sobrepõem, o sinalizador de status (campo dwstatus em DBCOLUMNACCESS) é definido como DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Consulte também  
 [Buscando uma única linha com IRow](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
