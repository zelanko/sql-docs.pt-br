---
title: 'Usando IRow:: Getcolumns | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
ms.assetid: 1f5d2e03-e6fe-4ea1-b71d-55d02b5d59ae
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 16ee88514a1c4caf7b47bb16868636c1028b0685
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43063458"
---
# <a name="using-irowgetcolumns"></a>Usando IRow::GetColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  A implementação de **IRow** permite o acesso sequencial somente de encaminhamento às colunas. Acesse todas as colunas da linha com uma única chamada a **IRow::GetColumns** ou chame **IRow::GetColumns** várias vezes sempre que você acessar várias colunas na linha.  
  
 As várias chamadas a **IRow::GetColumns** não devem se sobrepor. Por exemplo, se a primeira chamada a **IRow::GetColumns** recupera as colunas 1, 2 e 3, a segunda chamada a **IRow::GetColumns** deve chamar as colunas 4, 5 e 6. Caso as chamadas posteriores a **IRow::GetColumns** se sobreponham, um sinalizador de status (campo dwstatus em DBCOLUMNACCESS) será definido como DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Consulte também  
 [Buscando uma única linha com IRow](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
