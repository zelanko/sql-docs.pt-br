---
title: PersistFormatEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- PersistFormatEnum
helpviewer_keywords:
- PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1d63a918e63739c59f5fe2d0c7d9e3d7bf694449
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="persistformatenum"></a>PersistFormatEnum
Especifica o formato no qual salvar um [registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adPersistADTG**|0|Indica o formato do Microsoft Advanced dados TableGram (ADTG).|  
|**adPersistADO**|1|Indica que o formato do Extensible Markup Language (XML) do ADO será usado. Esse valor é o mesmo que adPersistXML e é incluído para compatibilidade com versões anteriores.|  
|**adPersistXML**|1|Indica o formato do Extensible Markup Language (XML).|  
|**adPersistProviderSpecific**|2|Indica que o provedor será mantido o **registros** usando seu próprio formato.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC Equivalent  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.PersistFormat.ADTG|  
|AdoEnums.PersistFormat.XML|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método Save](../../../ado/reference/ado-api/save-method.md)
