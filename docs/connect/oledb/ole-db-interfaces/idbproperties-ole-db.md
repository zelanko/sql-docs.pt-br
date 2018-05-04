---
title: IDBProperties (OLE DB) | Microsoft Docs
description: Interface IDBProperties (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 6c373967091794a5621c722c084bac7a086bf5a0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A especificação OLE DB padrão permite que os provedores especifiquem VT_EMPTY para **DBPROPINFO::vValues**. No entanto, OLE DB Driver para OLE DB do SQL Server sempre retorna o VT_EMPTY ao chamar **idbproperties:: Getpropertyinfo** com **DBPROPSET_ROWSETALL** para recuperar as propriedades do conjunto de linhas.  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
