---
description: Método get_OLEDBCommand
title: Método de get_OLEDBCommand | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- get_OLEDBCommand method [ADO]
ms.assetid: 23d551f5-3d5b-434b-ade6-fef15f1710e7
author: rothja
ms.author: jroth
ms.openlocfilehash: f824359fb373b2e2ac1347d10ef5ea32e9bee091
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88972817"
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