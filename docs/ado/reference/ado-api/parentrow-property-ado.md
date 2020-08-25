---
description: Propriedade ParentRow (ADO)
title: Propriedade ParentRow (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::put_ParentRow
- ADORecordConstruction::ParentRow
- ADORecordConstruction::putParentRow
helpviewer_keywords:
- ParentRow property [ADO]
ms.assetid: 5ea8029b-eda4-490b-ae84-2ad036fb582f
author: rothja
ms.author: jroth
ms.openlocfilehash: d7924a27a8b04e430eb1d9d68d5de6e4d19c51a8
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773265"
---
# <a name="parentrow-property-ado"></a>Propriedade ParentRow (ADO)
Define o contêiner de um objeto de **linha** de OLE DB em um objeto **ADORecordConstruction** , para que o pai da linha seja transformado em um objeto de **registro** ADO.  
  
 Somente gravação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT put_ParentRow([in] IUnknown* pParent);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *pParent*  
 Um contêiner de uma linha.  
  
## <a name="return-values"></a>Valores de retorno  
 Esse método de propriedade retorna os valores de HRESULT padrão, incluindo S_OK e E_FAIL.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Interface ADORecordConstruction](./adorecordconstruction-interface.md)