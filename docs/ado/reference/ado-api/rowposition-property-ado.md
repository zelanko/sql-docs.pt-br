---
title: Propriedade RowPosition (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::put_RowPosition
- ADORecordConstruction::PutRowPosition
- ADORecordConstruction::GetRowPosition
- ADORecordConstruction::RowPosition
- ADORecordConstruction::get_RowPosition
helpviewer_keywords:
- RowPosition property [ADO]
ms.assetid: 9d068fed-39bf-4842-afc3-686a2af2145d
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e2ef9ba5408aa41e3deda4c73e40057d916e1b31
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="rowposition-property-ado"></a>Propriedade RowPosition (ADO)
Obtém ou define um banco de dados OLE **RowPosition** objeto de/em uma **ADORecordsetConstruction** objeto. Quando você usa **put_RowPosition** para definir o **RowPosition** objeto resultante **registros** objeto usa o **RowPosition** do objeto para Determine a linha atual.  
  
 Leitura/gravação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT get_RowPosition([out, retval] IUnknown** ppRowPos);  
HRESULT put_RowPosition([in] IUnknown* pRowPos);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *ppRowPos*  
 Ponteiro para um banco de dados OLE **RowPosition** objeto.  
  
 *PRowPos*  
 OLE DB **RowPosition** objeto.  
  
## <a name="return-values"></a>Valores de retorno  
 Esse método de propriedade retorna os valores HRESULT padrão, incluindo S_OK e E_FAIL.  
  
## <a name="remarks"></a>Remarks  
 Quando essa propriedade é definida, se o **linhas** do objeto no **RowPosition** objeto é diferente do **linhas** do objeto no **Recordset**do objeto, o primeiro substitui o último. O mesmo comportamento se aplica a atual **capítulo** do **RowPosition** também.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Interface ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
