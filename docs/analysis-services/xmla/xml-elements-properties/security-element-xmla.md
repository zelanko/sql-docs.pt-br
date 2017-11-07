---
title: Elemento Security (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Security Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.security
- urn:schemas-microsoft-com:xml-analysis#Security
- http://schemas.microsoft.com/analysisservices/2003/engine#Security
helpviewer_keywords:
- Security element
ms.assetid: 0b601f69-d16d-4d10-9361-b8afaa6ed357
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cd1a4c292c1ac722fd91836b364724a0f59f8168
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="security-element-xmla"></a>Elemento Security (XMLA)
  Especifica como fazer backup ou restaurar definições de segurança, como funções e permissões, durante um [Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) ou [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <Security>...</Security>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*SkipMembership*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O **segurança** elemento determina se as definições de segurança, como funções e permissões, definidas em uma [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados são copiados ou restaurados durante, respectivamente, um **Backup** ou **restaurar** comando. Esse elemento também determina se as contas de usuário e os grupos do Windows definidos como membros das definições de segurança estão incluídos como parte do comando **Backup** ou **Restore** .  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*SkipMembership*|Inclui definições de segurança, mas exclui informações de associação, durante comandos **Backup** ou **Restore** .|  
|*CopyAll*|Inclui definições de segurança e informações de associação durante comandos **Backup** ou **Restore** .|  
|*IgnoreSecurity*|Exclui definições de segurança durante comandos **Backup** ou **Restore** .|  
  
## <a name="see-also"></a>Consulte também  
 [Elemento SynchronizeSecurity &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/synchronizesecurity-element-xmla.md)   
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

