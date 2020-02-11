---
title: PersistFormatEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PersistFormatEnum
helpviewer_keywords:
- PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a26fd370e80cb288ee62b0fc53ed6670300172e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917613"
---
# <a name="persistformatenum"></a>PersistFormatEnum
Especifica o formato no qual salvar um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|**adPersistADTG**|0|Indica o formato ADTG (Microsoft Advanced data TableGram).|  
|**adPersistADO**|1|Indica que o formato do próprio linguagem XML (XML) do ADO será usado. Esse valor é o mesmo que adPersistXML e é incluído para compatibilidade com versões anteriores.|  
|**adPersistXML**|1|Indica o formato linguagem XML (XML).|  
|**adPersistProviderSpecific**|2|Indica que o provedor irá persistir o **conjunto de registros** usando seu próprio formato.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.PersistFormat.ADTG|  
|AdoEnums.PersistFormat.XML|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método Save](../../../ado/reference/ado-api/save-method.md)
