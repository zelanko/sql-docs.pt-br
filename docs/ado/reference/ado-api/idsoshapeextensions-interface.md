---
description: Interface IDSOShapeExtensions
title: Interface IDSOShapeExtensions | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- IDSOShapeExtensions interface [ADO]
ms.assetid: ad4ba313-1161-4bc7-b8f6-4083305bc81e
author: rothja
ms.author: jroth
ms.openlocfilehash: 9c7eeb5999a42cfe8b82e570cc5ada1222f87441
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443468"
---
# <a name="idsoshapeextensions-interface"></a>Interface IDSOShapeExtensions
Obtém o objeto de fonte de dados de OLE DB subjacente para o provedor de forma.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
interface IDSOShapeExtensions: public IUnknown {  
public:  
      HRESULT  GetDataProviderDSO(  
            IUnknown **ppDataProviderDSOIUnknown  
      );  
};  
```  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|-|-|  
|[Método GetDataProviderDSO](../../../ado/reference/ado-api/getdataproviderdso-method.md)|Recupera o objeto de fonte de dados subjacente OLE DB do provedor de forma.|  
  
## <a name="requirements"></a>Requisitos  
 **Versão:** ADO 2,0 e posterior  
  
 **Biblioteca:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4
