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
ms.openlocfilehash: 562b10fa67b04926e512833248c99ecb7b55a1fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443598"
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
 [IADOCommandConstruction](https://msdn.microsoft.com/d8e54333-00eb-4b72-bf4a-ca92c7ca5f86)
