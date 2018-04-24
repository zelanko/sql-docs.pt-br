---
title: Método GetDataProviderDSO | Microsoft Docs
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
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fca773c6db137999da36daf0151a51a1becf79c6
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="getdataproviderdso-method"></a>Método GetDataProviderDSO
Recupera o objeto OLE DB fonte de dados subjacente do provedor de forma.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ppDataProviderDSOIUnknown*  
 [out]  Um ponteiro para um ponteiro que retorna o IUnknown do objeto OLE DB fonte de dados subjacente.  
  
## <a name="remarks"></a>Remarks  
 Esse método não addref não o ponteiro de interface. Se o chamador planos para manter o ponteiro, o chamador deve fazer o addref necessário e versão.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Interface IDSOShapeExtensions](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
