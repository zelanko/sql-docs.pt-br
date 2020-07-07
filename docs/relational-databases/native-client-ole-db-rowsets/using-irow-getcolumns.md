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
ms.openlocfilehash: 092c573e808aefc0f35f04e73b54e150a62bebac
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86013069"
---
# <a name="using-irowgetcolumns"></a>Usando IRow::GetColumns
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  A implementação de **IRow** permite o acesso sequencial somente de encaminhamento às colunas. Acesse todas as colunas da linha com uma única chamada a **IRow::GetColumns** ou chame **IRow::GetColumns** várias vezes sempre que você acessar várias colunas na linha.  
  
 As várias chamadas a **IRow::GetColumns** não devem se sobrepor. Por exemplo, se a primeira chamada a **IRow::GetColumns** recupera as colunas 1, 2 e 3, a segunda chamada a **IRow::GetColumns** deve chamar as colunas 4, 5 e 6. Caso as chamadas posteriores a **IRow::GetColumns** se sobreponham, um sinalizador de status (campo dwstatus em DBCOLUMNACCESS) será definido como DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Consulte Também  
 [Buscando uma única linha com IRow](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
