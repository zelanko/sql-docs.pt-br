---
title: Atualizar dados em conjunto de linhas (Driver do OLE DB)
description: Saiba como o Driver do OLE DB para SQL Server atualiza dados do SQL Server quando um consumidor atualiza um conjunto de linhas modificável que contém esses dados.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, updating data
- OLE DB Driver for SQL Server, data updates
- data updates [SQL Server], OLE DB
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 40bb8663cd2d49ceaeda2305797fb42bdacc4324
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88859959"
---
# <a name="updating-data-in-rowsets"></a>Atualizando dados em conjuntos de linhas
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O OLE DB Driver for SQL Server atualiza dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando um consumidor atualiza um conjunto de linhas modificável que contém esses dados. Um conjunto de linhas modificável é criado quando o consumidor solicita suporte para a interface **IRowsetChange** ou **IRowsetUpdate**.  
  
 Todos os conjuntos de linhas modificáveis do Driver do OLE DB para SQL Server usam cursores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para dar suporte ao conjunto de linhas. A propriedade do conjunto de linhas DBPROP_LOCKMODE altera o comportamento de controle da simultaneidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em cursores e determina o comportamento da busca de linhas do conjunto de linhas e da geração de erros de integridade de dados nos conjuntos de linhas atualizáveis.  
  
 O Driver do OLE DB para SQL Server dá suporte a sincronização de linhas antes ou depois de uma atualização.  
  
> [!NOTE]  
>  IRowChange::SetColumns está disponível para definir os valores de uma ou mais colunas nomeadas de um objeto de linha.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Atualizando dados em cursores do SQL Server](../../oledb/ole-db-rowsets/updating-data-in-sql-server-cursors.md)  
  
-   [Ressincronizando linhas](../../oledb/ole-db-rowsets/updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Conjuntos de linhas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
