---
description: IColumnsRowset (provedor de OLE DB de cliente nativo)
title: IColumnsRowset (provedor de OLE DB de cliente nativo) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: e35d37ed-dd9b-4a34-a76a-bc9251f06c4f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cd3af620c9958d510b7a4839d9d511064fb0028a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460329"
---
# <a name="icolumnsrowset-native-client-ole-db-provider"></a>IColumnsRowset (provedor de OLE DB de cliente nativo)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client acrescenta a coluna DBCOLUMN_BASETABLEINSTANCE a IColumnsRowset::GetColumnRowset. Essa coluna retorna DBTYPE_I2 e é reservada para uso pela Microsoft. As informações nessa coluna estão sujeitas à alteração em versões futuras.  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces do &#40;OLE DB&#41;](./sql-server-native-client-ole-db-interfaces.md)  
  
