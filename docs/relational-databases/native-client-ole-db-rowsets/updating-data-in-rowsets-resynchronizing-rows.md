---
description: Atualizando dados em conjuntos de linhas – ressincronizando filas no SQL Server Native Client
title: Ressincronizando linhas (provedor de OLE DB de cliente nativo)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
ms.assetid: d2d30505-a878-4aa9-b821-53d8118a45a5
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1d513e16d477d96c6592515b9ad61eda657c1bc1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97476057"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows-in-sql-server-native-client"></a>Atualizando dados em conjuntos de linhas – ressincronizando filas no SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte a **IRowsetResynch** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] somente em conjuntos de linhas com suporte para o cursor. **IRowsetResynch** não está disponível sob demanda. O consumidor deve solicitar a interface antes de abrir o conjunto de linhas.  
  
## <a name="see-also"></a>Consulte Também  
 [Atualizando dados em conjuntos de linhas](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
