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
ms.openlocfilehash: 2bceacc215a67050142c773675a0af464ff9b9ec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442238"
---
# <a name="row-property-ado"></a>Propriedade Row (ADO)
Obtém ou define um objeto de **linha** de OLE DB de ou em um objeto de [interface ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md) . Quando você usa **put_Row** para definir um objeto de **linha** , uma linha é transformada em um objeto de **registro** ADO.  
  
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
 [Interface ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
