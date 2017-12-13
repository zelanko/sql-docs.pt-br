---
title: Fazer backup de elemento (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Backup Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Backup
- http://schemas.microsoft.com/analysisservices/2003/engine#Backup
- microsoft.xml.analysis.backup
helpviewer_keywords: Backup command
ms.assetid: 5bcbc14c-9db9-45b2-99de-f3a265bcb0c4
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 26a67121b506f33f69b408fde57aa2e94fa3beed
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="backup-element-xmla"></a>Elemento de backup (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Faz backup de um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados para um arquivo de backup.  
  
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[AllowOverwrite](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md), [ApplyCompression](../../../analysis-services/xmla/xml-elements-properties/applycompression-element-xmla.md), [BackupRemotePartitions](../../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md), [arquivo](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md), [locais](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md), [Objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [senha](../../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md), [segurança](../../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 O **Backup** comando faz backup de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados especificado no [objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) elemento para um arquivo de backup e, opcionalmente, faz backup de partições remotas em arquivos de backup remotos. Se o **objeto** elemento se refere a um objeto diferente de um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] de banco de dados, ocorrerá um erro.  
  
 O que determina quais as informações que terão seu backup feito pelo comando **Backup** será o modo de armazenamento usado por objetos no banco de dados. A tabela a seguir identifica as informações que têm seu backup feito no modo de armazenamento usado.  
  
|Modo de armazenamento|Informações que terão backup|  
|------------------|-----------------------------------|  
|OLAP multidimensional (MOLAP)|Dados de origem, agregações e metadados|  
|OLAP híbrido (HOLAP)|Agregações e metadados|  
|OLAP relacional (ROLAP)|Metadados|  
  
 Durante uma **Backup** de comando, um bloqueio compartilhado é colocado no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados especificado no **objeto** elemento. As versões de bloqueio compartilhado são liberadas depois que o comando **Backup** é completado.  
  
 Vários **Backup** comandos podem ser executados em paralelo, se os comandos forem incluídos no [paralela](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md) coleção de um [lote](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) comando. A coleção **Parallel** permite que um banco de dados tenha backup feito em vários arquivos de backup ao mesmo tempo.  
  
 Para obter mais informações sobre backup e restaurando bancos de dados, consulte [fazendo backup, restauração e sincronizando bancos de dados &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
> [!IMPORTANT]  
>  Para cada arquivo de backup, o usuário que executar o comando de backup deve ter permissão para gravar no local de backup especificado de cada arquivo. Além disso, o usuário deve ter uma das seguintes funções: membro de uma função de servidor para a instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle total (Administrador) no banco de dados cujo backup será feito.  
  
## <a name="see-also"></a>Consulte também  
 [Restaurar o elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [Sincronizar o elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
