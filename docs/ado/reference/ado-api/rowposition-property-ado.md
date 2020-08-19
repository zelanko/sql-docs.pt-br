---
description: Propriedade RowPosition (ADO)
title: Propriedade de função (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 330c090c9e4eedd6a083d58a55243d470514541f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442458"
---
# <a name="rowposition-property-ado"></a>Propriedade RowPosition (ADO)
Obtém ou define um OLE DB objeto de **função** de/em um objeto **ADORecordsetConstruction** . Quando você usa **put_RowPosition** para definir o **objeto de** rowgroup, o objeto **Recordset** resultante **usa o objeto** rowgroup para determinar a linha atual.  
  
 Leitura/gravação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT get_RowPosition([out, retval] IUnknown** ppRowPos);  
HRESULT put_RowPosition([in] IUnknown* pRowPos);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *ppRowPos*  
 Ponteiro para um objeto de OLE DB de @ **Position** .  
  
 *PRowPos*  
 Um OLE DB objeto de @ **Position** .  
  
## <a name="return-values"></a>Valores de retorno  
 Esse método de propriedade retorna os valores de HRESULT padrão, incluindo S_OK e E_FAIL.  
  
## <a name="remarks"></a>Comentários  
 Quando essa propriedade for definida, se o objeto de **conjunto de linhas** no objeto da **posição** for diferente do objeto **Rowset** no objeto **Recordset** , o primeiro substituirá o último. O mesmo comportamento também se aplica ao **capítulo** atual da sua **posição** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Interface ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
