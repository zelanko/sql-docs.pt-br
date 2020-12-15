---
description: Atualizando dados em conjuntos de linhas no SQL Server Native Client
title: Atualizando dados em conjuntos de linhas (provedor de OLE DB de cliente nativo)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, updating data
- SQL Server Native Client OLE DB provider, data updates
- data updates [SQL Server], OLE DB
ms.assetid: 37769b1c-c480-419a-8c54-5cc420bf73db
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3d3639e0fd6a72df7ea748cc0a2aa4daf79776f9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97476047"
---
# <a name="updating-data-in-rowsets-in-sql-server-native-client"></a>Atualizando dados em conjuntos de linhas no SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo atualiza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os dados quando um consumidor atualiza um conjunto de linhas modificável que contém esses dados. Um conjunto de linhas modificável é criado quando o consumidor solicita suporte para a interface **IRowsetChange** ou **IRowsetUpdate**.  
  
 Todos os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de linhas modificáveis do provedor de OLE DB de clientes nativos usam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores para dar suporte ao conjunto de linhas. A propriedade do conjunto de linhas DBPROP_LOCKMODE altera o comportamento de controle da simultaneidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em cursores e determina o comportamento da busca de linhas do conjunto de linhas e da geração de erros de integridade de dados nos conjuntos de linhas atualizáveis.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte à sincronização de linha antes ou depois de uma atualização.  
  
> [!NOTE]  
>  IRowChange::SetColumns está disponível para definir os valores de uma ou mais colunas nomeadas de um objeto de linha.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Atualizando dados em cursores do SQL Server](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-sql-server-cursors.md)  
  
-   [Ressincronizando linhas](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Conjuntos de linhas](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
