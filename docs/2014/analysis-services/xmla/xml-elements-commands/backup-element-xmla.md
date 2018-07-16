---
title: Fazer backup de elemento (XMLA) | Microsoft Docs
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
- Backup Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Backup
- http://schemas.microsoft.com/analysisservices/2003/engine#Backup
- microsoft.xml.analysis.backup
helpviewer_keywords:
- Backup command
ms.assetid: 5bcbc14c-9db9-45b2-99de-f3a265bcb0c4
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a571681f52fb34e55df238229f659aa883bc84ac
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37215646"
---
# <a name="backup-element-xmla"></a>Elemento de backup (XMLA)
  Faz backup de um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados para um arquivo de backup.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Backup>  
      <Object>...</Object>  
      <File>...</File>  
      <Security>...</Security>  
      <ApplyCompression>...</ApplyCompression>  
      <AllowOverwrite>...</AllowOverwrite>  
      <Password>...</Password>  
      <BackupRemotePartitions>...</BackupRemotePartitions>  
      <Locations>...</Locations>  
   </Backup>  
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
|Elementos filho|[AllowOverwrite](../xml-elements-properties/allowoverwrite-element-xmla.md), [ApplyCompression](../xml-elements-properties/applycompression-element-xmla.md), [BackupRemotePartitions](../xml-elements-properties/backupremotepartitions-element-xmla.md), [arquivo](../xml-elements-properties/file-element-xmla.md), [locais](../xml-elements-properties/locations-element-xmla.md), [ Objeto](../xml-elements-properties/object-element-xmla.md), [senha](../xml-elements-properties/password-element-xmla.md), [segurança](../xml-elements-properties/security-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O `Backup` comando faz backup de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados especificado no [objeto](../xml-elements-properties/object-element-xmla.md) elemento para um arquivo de backup e, opcionalmente, faz backup de partições remotas em arquivos de backup remotos. Se o elemento `Object` se referir a um objeto diferente de um banco de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], ocorrerá um erro.  
  
 Quais informações o `Backup` comando faz backup depende do modo de armazenamento usado por objetos no banco de dados. A tabela a seguir identifica as informações que têm seu backup feito no modo de armazenamento usado.  
  
|Modo de armazenamento|Informações que terão backup|  
|------------------|-----------------------------------|  
|OLAP multidimensional (MOLAP)|Dados de origem, agregações e metadados|  
|OLAP híbrido (HOLAP)|Agregações e metadados|  
|OLAP relacional (ROLAP)|Metadados|  
  
 Durante um `Backup` de comando, um bloqueio compartilhado é colocado na [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados especificado no `Object` elemento. O bloqueio compartilhado libera após o `Backup` comando foi concluído.  
  
 Vários `Backup` comandos podem ser executados em paralelo, se os comandos forem incluídos na [paralela](../xml-elements-properties/parallel-element-xmla.md) coleção de uma [lote](batch-element-xmla.md) comando. A coleção `Parallel` permite que um banco de dados tenha backup feito em vários arquivos de backup ao mesmo tempo.  
  
 Para obter mais informações sobre backup e restaurando bancos de dados, consulte [fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
> [!IMPORTANT]  
>  Para cada arquivo de backup, o usuário que executar o comando de backup deve ter permissão para gravar no local de backup especificado de cada arquivo. Além disso, o usuário deve ter uma das seguintes funções: membro de uma função de servidor para a instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle total (Administrador) no banco de dados cujo backup será feito.  
  
## <a name="see-also"></a>Consulte também  
 [Restaurar o elemento &#40;XMLA&#41;](restore-element-xmla.md)   
 [Elemento Synchronize &#40;XMLA&#41;](synchronize-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
