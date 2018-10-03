---
title: Método get_OLEDBCommand | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72e902c6eb27cadff5f49d5bc385b99917f977eb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47850391"
---
# <a name="getoledbcommand-method"></a>Método get_OLEDBCommand
Retorna o subjacente comando OLE DB, primeiro propagar qualquer informação de parâmetro definido no comando ADO para o comando OLE DB.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT get_OLEDBCommand(  
      IUnknown **ppOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ppOLEDBCommand*  
 [out] Um ponteiro para um local do ponteiro no qual o ponteiro IUnknown para o OLE DB comando subjacente será gravado.  
  
## <a name="applies-to"></a>Aplica-se a  
 [IADOCommandConstruction](http://msdn.microsoft.com/d8e54333-00eb-4b72-bf4a-ca92c7ca5f86)
