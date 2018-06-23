---
title: Elemento Restore (XMLA) | Microsoft Docs
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
- Restore Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Restore
- urn:schemas-microsoft-com:xml-analysis#Restore
- microsoft.xml.analysis.restore
helpviewer_keywords:
- Restore command
ms.assetid: bb5a0c92-3927-4fa4-975b-6e4d79e0a912
caps.latest.revision: 26
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 0e8eca537c61be64de403b4ad08bb0e64040937c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121776"
---
# <a name="restore-element-xmla"></a>Elemento Restore (XMLA)
  Restaura um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados de um arquivo de backup.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Restore>  
      <DatabaseName>...</DatabaseName>  
      <DatabaseID>...</DatabaseID>  
      <File>...</File>  
      <Security>...</Security>  
      <AllowOverwrite>...</AllowOverwrite>  
      <Password>...</Password>  
      <Locations>...</Locations>  
      <DbStorageLocation>...</DbStorageLocation>  
   </Restore>  
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
|Elementos filho|[AllowOverwrite](../xml-elements-properties/allowoverwrite-element-xmla.md), [DatabaseName](../xml-elements-properties/name-element-xmla.md), [DatabaseID](../xml-elements-properties/id-element-xmla.md), [arquivo](../xml-elements-properties/file-element-xmla.md), [locais](../xml-elements-properties/locations-element-xmla.md), [senha](../xml-elements-properties/password-element-xmla.md), [Segurança](../xml-elements-properties/security-element-xmla.md), [DbStorageLocation](../xml-elements-properties/dbstoragelocation-element.md)|  
  
## <a name="remarks"></a>Remarks  
 O `Restore` comando restaura um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados especificado no `DatabaseName` elemento de um arquivo de backup e, opcionalmente, restaura partições remotas de arquivos de backup remotos.  
  
 Dependendo do modo de armazenamento usado por objetos armazenados no arquivo de backup, o `Restore` comando restaura informações conforme listado na tabela a seguir.  
  
|Modo de armazenamento|Informações|  
|------------------|-----------------|  
|OLAP multidimensional (MOLAP)|Dados de origem, agregações e metadados|  
|OLAP híbrido (HOLAP)|Agregações e metadados|  
|OLAP relacional (ROLAP)|Metadados|  
  
 Durante uma `Restore` de comando, um bloqueio exclusivo é colocado no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados especificado no `DatabaseName` elemento. O bloqueio é liberado após o `Restore` comando foi concluído.  
  
 Para obter mais informações sobre backup e restaurando bancos de dados, consulte [fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
> [!IMPORTANT]  
>  Para cada arquivo de backup, o usuário que executar o comando de restauração deve ter permissão para ler no local de backup especificado para cada arquivo. Para restaurar um banco de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que não esteja instalado no servidor, o usuário também deve ser membro da função de servidor dessa instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Para substituir um banco de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , o usuário deve ter uma das seguintes funções: membro da função de servidor da instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle Total (Administrador) no banco de dados a ser restaurado.  
  
> [!NOTE]  
>  Após restaurar um banco de dados existente, o usuário que o restaurou poderá perder o acesso ao banco de dados restaurado. Essa perda de acesso pode ocorrer se, no momento da execução do backup, o usuário não for membro da função de servidor, nem membro da função de banco de dados com permissões de Controle total (Administrador).  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de backup &#40;XMLA&#41;](backup-element-xmla.md)   
 [Elemento de lote &#40;XMLA&#41;](batch-element-xmla.md)   
 [Paralelo elemento &#40;XMLA&#41;](../xml-elements-properties/parallel-element-xmla.md)   
 [Elemento Synchronize &#40;XMLA&#41;](synchronize-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  