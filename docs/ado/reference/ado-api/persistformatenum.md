---
description: PersistFormatEnum
title: PersistFormatEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c8c4f917b9c2874e945a3ff523c0d6593386a619
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990077"
---
# <a name="persistformatenum"></a>PersistFormatEnum
Especifica o formato no qual salvar um [conjunto de registros](./recordset-object-ado.md).  
  
|Constante|Valor|Descrição|  
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
 [Método Save](./save-method.md)