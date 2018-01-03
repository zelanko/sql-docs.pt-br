---
title: Propriedade ParentRow (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADORecordConstruction::put_ParentRow
- ADORecordConstruction::ParentRow
- ADORecordConstruction::putParentRow
helpviewer_keywords: ParentRow property [ADO]
ms.assetid: 5ea8029b-eda4-490b-ae84-2ad036fb582f
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d7aa68b89272bd9a6c39f7ae770898e169a90d8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="parentrow-property-ado"></a>Propriedade ParentRow (ADO)
Define o contêiner do OLE DB **linha** do objeto em um **ADORecordConstruction** do objeto, para que o pai da linha é transformado em ADO **registro** objeto.  
  
 Somente gravação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT put_ParentRow([in] IUnknown* pParent);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *pParent*  
 Um contêiner de uma linha.  
  
## <a name="return-values"></a>Valores de retorno  
 Esse método de propriedade retorna os valores HRESULT padrão, incluindo S_OK e E_FAIL.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Interface ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
