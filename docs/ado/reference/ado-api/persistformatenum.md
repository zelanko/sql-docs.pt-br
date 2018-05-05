---
title: PersistFormatEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PersistFormatEnum
helpviewer_keywords:
- PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 141590f2755323422f44aacb4617905191d3a154
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="persistformatenum"></a>PersistFormatEnum
Especifica o formato no qual salvar um [registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Value|Description|  
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
