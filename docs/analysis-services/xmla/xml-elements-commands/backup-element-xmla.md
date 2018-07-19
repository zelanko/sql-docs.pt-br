---
title: Fazer backup de elemento (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4e00a4991226779a91e16806dbe15973d946ec69
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38007146"
---
# <a name="backup-element-xmla"></a>Elemento de backup (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Faz backup de um banco de dados do Analysis Services em um arquivo de backup.  
  
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
|Elementos pai|[Comando](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[AllowOverwrite](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md), [ApplyCompression](../../../analysis-services/xmla/xml-elements-properties/applycompression-element-xmla.md), [BackupRemotePartitions](../../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md), [arquivo](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md), [locais](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md), [ Objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [senha](../../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md), [segurança](../../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O **Backup** comando faz backup de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados especificado no [objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) elemento para um arquivo de backup e, opcionalmente, faz backup de partições remotas em arquivos de backup remotos. Se o **objeto** elemento se refere a um objeto diferente de um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] de banco de dados, ocorrerá um erro.  
  
 O que determina quais as informações que terão seu backup feito pelo comando **Backup** será o modo de armazenamento usado por objetos no banco de dados. A tabela a seguir identifica as informações que têm seu backup feito no modo de armazenamento usado.  
  
|Modo de armazenamento|Informações que terão backup|  
|------------------|-----------------------------------|  
|OLAP multidimensional (MOLAP)|Dados de origem, agregações e metadados|  
|OLAP híbrido (HOLAP)|Agregações e metadados|  
|OLAP relacional (ROLAP)|Metadados|  
  
 Durante um **Backup** de comando, um bloqueio compartilhado é colocado na [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados especificado no **objeto** elemento. As versões de bloqueio compartilhado são liberadas depois que o comando **Backup** é completado.  
  
 Vários **Backup** comandos podem ser executados em paralelo, se os comandos forem incluídos na [paralela](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md) coleção de um [lote](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) comando. A coleção **Parallel** permite que um banco de dados tenha backup feito em vários arquivos de backup ao mesmo tempo.  
  
 Para obter mais informações sobre backup e restaurando bancos de dados, consulte [fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
> [!IMPORTANT]  
>  Para cada arquivo de backup, o usuário que executar o comando de backup deve ter permissão para gravar no local de backup especificado de cada arquivo. Além disso, o usuário deve ter uma das seguintes funções: membro de uma função de servidor para a instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle total (Administrador) no banco de dados cujo backup será feito.  
  
## <a name="see-also"></a>Confira também
 [Restaurar o elemento &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [Elemento Synchronize &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
