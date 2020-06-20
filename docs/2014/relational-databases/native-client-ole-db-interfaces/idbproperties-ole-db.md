---
title: IDBProperties (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
author: rothja
ms.author: jroth
ms.openlocfilehash: f42ab47de2471fc413e4c6acf0d6c61cb2b6d77c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056191"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
  A especificação OLE DB padrão permite que os provedores especifiquem VT_EMPTY para `DBPROPINFO::vValues`. No entanto, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB sempre retorna VT_EMPTY quando você chama `IDBProperties::GetPropertyInfo` with `DBPROPSET_ROWSETALL` para recuperar as propriedades do conjunto de linhas.  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
