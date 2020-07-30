---
title: Usar IRow::GetColumns | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
ms.assetid: 1f5d2e03-e6fe-4ea1-b71d-55d02b5d59ae
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8984b5d883229dfed1219463adcb0b02292d036b
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246795"
---
# <a name="using-irowgetcolumns-in-sql-server-native-client"></a>Usando IRow:: GetColumns no SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  A implementação de **IRow** permite o acesso sequencial somente de encaminhamento às colunas. Acesse todas as colunas da linha com uma única chamada a **IRow::GetColumns** ou chame **IRow::GetColumns** várias vezes sempre que você acessar várias colunas na linha.  
  
 As várias chamadas a **IRow::GetColumns** não devem se sobrepor. Por exemplo, se a primeira chamada a **IRow::GetColumns** recupera as colunas 1, 2 e 3, a segunda chamada a **IRow::GetColumns** deve chamar as colunas 4, 5 e 6. Caso as chamadas posteriores a **IRow::GetColumns** se sobreponham, um sinalizador de status (campo dwstatus em DBCOLUMNACCESS) será definido como DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Consulte Também  
 [Buscando uma única linha com IRow](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
