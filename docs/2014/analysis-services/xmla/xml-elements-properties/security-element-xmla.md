---
title: Elemento Security (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Security Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.security
- urn:schemas-microsoft-com:xml-analysis#Security
- http://schemas.microsoft.com/analysisservices/2003/engine#Security
helpviewer_keywords:
- Security element
ms.assetid: 0b601f69-d16d-4d10-9361-b8afaa6ed357
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 138b93043cbfeba51472dfa61816cf9023a3f2c6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37155017"
---
# <a name="security-element-xmla"></a>Elemento Security (XMLA)
  Especifica como fazer backup ou restaurar definições de segurança, como funções e permissões, durante um [Backup](../xml-elements-commands/backup-element-xmla.md) ou [restaurar](../xml-elements-commands/restore-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <Security>...</Security>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*SkipMembership*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Backup](../xml-elements-commands/backup-element-xmla.md), [restaurar](../xml-elements-commands/restore-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O `Security` elemento determina se as definições de segurança, como funções e permissões, definidas em um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados são copiados ou restaurados durante, respectivamente, um `Backup` ou `Restore` comando. Esse elemento também determina se as contas de usuário e os grupos do Windows definidos como membros das definições de segurança estão incluídos como parte do comando `Backup` ou `Restore`.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*SkipMembership*|Inclui definições de segurança, mas exclui informações de associação, durante comandos `Backup` ou `Restore`.|  
|*CopyAll*|Inclui definições de segurança e informações de associação durante comandos `Backup` ou `Restore`.|  
|*IgnoreSecurity*|Exclui definições de segurança durante comandos `Backup` ou `Restore`.|  
  
## <a name="see-also"></a>Consulte também  
 [Elemento SynchronizeSecurity &#40;XMLA&#41;](security-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
