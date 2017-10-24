---
title: Interface IDSOShapeExtensions | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IDSOShapeExtensions interface [ADO]
ms.assetid: ad4ba313-1161-4bc7-b8f6-4083305bc81e
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5168df904df1cfc8f764fe628f8e83382eb86f81
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="idsoshapeextensions-interface"></a>Interface IDSOShapeExtensions
Obtém o objeto OLE DB fonte de dados subjacente para o provedor de forma.  
  
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
  
|||  
|-|-|  
|[Método GetDataProviderDSO](../../../ado/reference/ado-api/getdataproviderdso-method.md)|Recupera o objeto OLE DB fonte de dados subjacente do provedor de forma.|  
  
## <a name="requirements"></a>Requisitos  
 **Versão:** ADO 2.0 e posterior  
  
 **Biblioteca:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4

