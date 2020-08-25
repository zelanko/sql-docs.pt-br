---
description: Propriedade Row (ADO)
title: Propriedade Row (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3048bf470ed27adb3fb3ceaaef3c7658c1fb93fb
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777625"
---
# <a name="row-property-ado"></a>Propriedade Row (ADO)
Obtém ou define um objeto de **linha** de OLE DB de ou em um objeto de [interface ADORecordConstruction](./adorecordconstruction-interface.md) . Quando você usa **put_Row** para definir um objeto de **linha** , uma linha é transformada em um objeto de **registro** ADO.  
  
## <a name="readwritesyntax"></a>Leitura/gravação. Sintaxe  
  
```  
HRESULT get_Row([out, retval] IUnknown** ppRow);  
HRESULT put_Row([in] IUnknown* pRow);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *ppRow*  
 Ponteiro para um objeto de **linha** de OLE DB.  
  
 *PRow*  
 Um objeto de **linha** OLE DB.  
  
## <a name="return-values"></a>Valores de retorno  
 Esse método de propriedade retorna os valores de HRESULT padrão, incluindo S_OK e E_FAIL.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Interface ADORecordConstruction](./adorecordconstruction-interface.md)