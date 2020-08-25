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
ms.openlocfilehash: 2e7a5b667d7735296a338a6a2259b7691f4fbeda
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774855"
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
|[Método GetDataProviderDSO](./getdataproviderdso-method.md)|Recupera o objeto de fonte de dados subjacente OLE DB do provedor de forma.|  
  
## <a name="requirements"></a>Requisitos  
 **Versão:** ADO 2,0 e posterior  
  
 **Biblioteca:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4