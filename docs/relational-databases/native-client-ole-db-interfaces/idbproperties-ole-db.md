---
description: IDBProperties (provedor de OLE DB de cliente nativo)
title: IDBProperties (provedor de OLE DB de cliente nativo) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ed1d47f6de4e0e3dddaac0b100727be95ca056ae
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486690"
---
# <a name="idbproperties-native-client-ole-db-provider"></a>IDBProperties (provedor de OLE DB de cliente nativo)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  A especificação OLE DB padrão permite que os provedores especifiquem VT_EMPTY para **DBPROPINFO::vValues**. Entretanto, o OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client sempre retorna o VT_EMPTY ao chamar **IDBProperties::GetPropertyInfo** com **DBPROPSET_ROWSETALL** para recuperar propriedades de conjuntos de linhas.  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces do &#40;OLE DB&#41;](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
