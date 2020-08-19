---
description: Método GetDataProviderDSO
title: Método GetDataProviderDSO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
author: rothja
ms.author: jroth
ms.openlocfilehash: 1a45d78960b8b6b1ba2534e39f080a6c94fc0655
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443568"
---
# <a name="getdataproviderdso-method"></a>Método GetDataProviderDSO
Recupera o objeto de fonte de dados subjacente OLE DB do provedor de forma.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ppDataProviderDSOIUnknown*  
 fora  Um ponteiro para um ponteiro que retorna o IUnknown do objeto de fonte de dados subjacente OLE DB.  
  
## <a name="remarks"></a>Comentários  
 Esse método não AddRef o ponteiro de interface. Se o chamador planeja manter o ponteiro, o chamador deve fazer o AddRef e a versão necessários.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Interface IDSOShapeExtensions](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
