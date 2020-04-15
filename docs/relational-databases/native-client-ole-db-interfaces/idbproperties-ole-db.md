---
title: IDBProperties (OLE DB) | Microsoft Docs
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
ms.openlocfilehash: b6e7fb08bfde514a578481674b01bba9d0e417a2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307248"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A especificação OLE DB padrão permite que os provedores especifiquem VT_EMPTY para **DBPROPINFO::vValues**. Entretanto, o OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client sempre retorna o VT_EMPTY ao chamar **IDBProperties::GetPropertyInfo** com **DBPROPSET_ROWSETALL** para recuperar propriedades de conjuntos de linhas.  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces &#40;OLE DB&#41;](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
