---
title: PersistFormatEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- PersistFormatEnum
helpviewer_keywords:
- PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9c981037637b85e23e6b871116291aa8eb607c99
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="persistformatenum"></a>PersistFormatEnum
Especifica o formato no qual salvar um [registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adPersistADTG**|0|Indica o formato do Microsoft Advanced dados TableGram (ADTG).|  
|**adPersistADO**|1|Indica que o formato do Extensible Markup Language (XML) do ADO será usado. Esse valor é o mesmo que adPersistXML e é incluído para compatibilidade com versões anteriores.|  
|**adPersistXML**|1|Indica o formato do Extensible Markup Language (XML).|  
|**adPersistProviderSpecific**|2|Indica que o provedor será mantido o **registros** usando seu próprio formato.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.PersistFormat.ADTG|  
|AdoEnums.PersistFormat.XML|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método Save](../../../ado/reference/ado-api/save-method.md)

