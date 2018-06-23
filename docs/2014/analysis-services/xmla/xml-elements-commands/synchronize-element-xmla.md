---
title: Elemento Synchronize (XMLA) | Microsoft Docs
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
- Synchronize Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.synchronize
- urn:schemas-microsoft-com:xml-analysis#Synchronize
- http://schemas.microsoft.com/analysisservices/2003/engine#Synchronize
helpviewer_keywords:
- Synchronize command
ms.assetid: 9401323c-feff-409a-a9da-94aee47e0563
caps.latest.revision: 15
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 367d237cab7ea63b85e000433742d866466b3f62
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119402"
---
# <a name="synchronize-element-xmla"></a>Elemento Synchronize (XMLA)
  Sincroniza um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados com outro banco de dados existente.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Synchronize>  
      <Source>...</Source>  
      <SynchronizeSecurity>...</SynchronizeSecurity>  
      <ApplyCompression>...</ApplyCompression>  
      <Locations>...</Locations>  
   </Synchronize>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[ApplyCompression](../xml-elements-properties/applycompression-element-xmla.md), [locais](../xml-elements-properties/locations-element-xmla.md), [fonte](../xml-elements-properties/source-element-synchronize-xmla.md), [SynchronizeSecurity](../xml-elements-properties/security-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O comando `Synchronize` sincroniza o banco de dados de destino com uma instância de origem e banco de dados especificado no elemento `Source`. Opcionalmente, o comando `Synchronize` sincroniza partições remotas definidas no banco de dados de origem.  
  
 Dependendo do modo de armazenamento usado por objetos armazenados no arquivo de backup, o comando `Synchronize` sincroniza informações conforme listadas na tabela a seguir.  
  
|Modo de armazenamento|Informações|  
|------------------|-----------------|  
|OLAP multidimensional (MOLAP)|Dados de origem, agregações e metadados|  
|OLAP híbrido (HOLAP)|Agregações e metadados|  
|OLAP relacional (ROLAP)|Metadados|  
  
 Durante um comando `Synchronize`, um bloqueio de leitura é posicionado no banco de dados de origem e um bloqueio contra gravação é posicionado no banco de dados de destino. Ambos os tipos de bloqueio são liberados depois que o comando `Synchronize` é concluído.  
  
 Para obter mais informações sobre a sincronização de bancos de dados, consulte [fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de backup &#40;XMLA&#41;](backup-element-xmla.md)   
 [Elemento de lote &#40;XMLA&#41;](batch-element-xmla.md)   
 [Paralelo elemento &#40;XMLA&#41;](../xml-elements-properties/parallel-element-xmla.md)   
 [Elemento Restore &#40;XMLA&#41;](restore-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  