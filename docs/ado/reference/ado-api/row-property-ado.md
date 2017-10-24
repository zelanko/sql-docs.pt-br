---
title: Linha de propriedade (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADORecordConstruction::PutRow
- ADORecordConstruction::GetRow
- ADORecordConstruction::get_Row
- ADORecordConstruction::Row
- ADORecordConstruction::put_Row
helpviewer_keywords:
- Row property [ADO]
ms.assetid: 21019d89-2dd1-4a26-ac6f-384b81d66949
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 19b935d43739d1a1ce19f414cae12b00c311b261
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="row-property-ado"></a>Propriedade de linha (ADO)
Obtém ou define um banco de dados OLE **linha** objeto de ou em um [ADORecordConstruction Interface](../../../ado/reference/ado-api/adorecordconstruction-interface.md) objeto. Quando você usa **put_Row** para definir um **linha** do objeto, uma linha será transformada em ADO **registro** objeto.  
  
## <a name="readwritesyntax"></a>Leitura/gravação. Sintaxe  
  
```  
HRESULT get_Row([out, retval] IUnknown** ppRow);  
HRESULT put_Row([in] IUnknown* pRow);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *ppRow*  
 Ponteiro para um banco de dados OLE **linha** objeto.  
  
 *PRow*  
 OLE DB **linha** objeto.  
  
## <a name="return-values"></a>Valores de retorno  
 Esse método de propriedade retorna os valores HRESULT padrão, incluindo S_OK e E_FAIL.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Interface ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)

