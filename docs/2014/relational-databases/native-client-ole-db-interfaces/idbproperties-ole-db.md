---
title: IDBProperties (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b6dada26e15fc83d890b270ad553eb051bb08fa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62692188"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
  A especificação OLE DB padrão permite que os provedores especifiquem VT_EMPTY para `DBPROPINFO::vValues`. No entanto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Native Client OLE DB sempre retorna VT_EMPTY `IDBProperties::GetPropertyInfo` quando `DBPROPSET_ROWSETALL` você chama with para recuperar as propriedades do conjunto de linhas.  
  
## <a name="see-also"></a>Consulte Também  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
