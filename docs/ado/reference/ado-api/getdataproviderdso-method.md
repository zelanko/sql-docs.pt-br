---
title: "Método GetDataProviderDSO | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 51b64a4e9bb2ea1c600e9f1c04f345c18e486e0b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
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
  
## <a name="remarks"></a>Comentários  
 Esse método não addref não o ponteiro de interface. Se o chamador planos para manter o ponteiro, o chamador deve fazer o addref necessário e versão.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Interface IDSOShapeExtensions](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
