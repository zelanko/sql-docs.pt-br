---
title: 'Usando IRow:: Getcolumns | Microsoft Docs'
description: 'Usando IRow:: Getcolumns para acessar todas as colunas em uma linha'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
manager: craigg
ms.openlocfilehash: 6bae3626cace1490110a2402d0f33e6c3924bdd5
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35306345"
---
# <a name="using-irowgetcolumns"></a>Usando IRow::GetColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O **IRow** implementação permite acesso sequencial somente de encaminhamento para as colunas. Você pode acessar todas as colunas na linha com uma única chamada para **IRow:: Getcolumns** ou chame **IRow:: Getcolumns** várias vezes sempre que você acessa várias colunas na linha.  
  
 As várias chamadas para **IRow:: Getcolumns** não devem se sobrepor. Por exemplo, se a primeira chamada para **IRow:: Getcolumns** recupera colunas 1, 2 e 3, a segunda chamada para **IRow:: Getcolumns** deve chamar as colunas 4, 5 e 6. Se chamadas posteriores para **IRow:: Getcolumns** se sobrepõem, o sinalizador de status (campo dwstatus em DBCOLUMNACCESS) é definido como DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Consulte também  
 [Buscando uma única linha com IRow](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
