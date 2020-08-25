---
description: Método get_OLEDBCommand
title: Método de get_OLEDBCommand | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- get_OLEDBCommand method [ADO]
ms.assetid: 23d551f5-3d5b-434b-ade6-fef15f1710e7
author: rothja
ms.author: jroth
ms.openlocfilehash: 56148afcd3c7d3e18e856c6e50a44f35aaa1bc64
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775125"
---
# <a name="get_oledbcommand-method"></a>Método get_OLEDBCommand
Retorna o comando OLE DB subjacente, primeiro propagando todas as informações de parâmetro definidas no comando ADO para o comando OLE DB.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT get_OLEDBCommand(  
      IUnknown **ppOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ppOLEDBCommand*  
 fora Um ponteiro para um local de ponteiro em que o ponteiro IUnknown do comando OLE DB subjacente será gravado.  
  
## <a name="applies-to"></a>Aplica-se A  
 [IADOCommandConstruction](/previous-versions/windows/desktop/aa965677(v=vs.85))