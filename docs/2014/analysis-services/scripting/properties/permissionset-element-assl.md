---
title: Elemento PermissionSet (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- PermissionSet Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PermissionSet
helpviewer_keywords:
- PermissionSet element
ms.assetid: da5a9175-48e4-4b5e-a780-3e0077939974
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 590dbc9ae62340fd3d4cf08d06f8a593bcf520f5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049297"
---
# <a name="permissionset-element-assl"></a>Elemento PermissionSet (ASSL)
  Identifica o conjunto de permissões associado com um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] assembly do .NET Framework.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ClrAssembly>  
   ...  
   <PermissionSet>...</PermissionSet>  
  
</ClrAssembly>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Safe*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ClrAssembly](../data-type/assembly-data-type-assl.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Safe*|Somente computação interna e acesso a dados local são permitidos. *Safe* é o conjunto de permissões mais restritivo. O código executado por um assembly com as permissões *Safe* não pode acessar recursos externos do sistema, como arquivos, rede, variáveis de ambiente ou Registro.|  
|*ExternalAccess*|*Safe*, com a habilidade adicional para acessar recursos externos do sistema, como arquivos, redes, variáveis de ambiente e registro.|  
|*Sem restrições*|Unrestricted permite aos assemblies acesso irrestrito aos recursos, tanto dentro quanto fora [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O código executado a partir de um assembly *Unrestricted* pode chamar o código não gerenciado.|  
  
 A enumeração que corresponde aos valores permitidos para `PermissionSet` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.PermissionSet>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados ComAssembly &#40;ASSL&#41;](../data-type/comassembly-data-type-assl.md)   
 [Elemento assemblies &#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [Elemento de banco de dados &#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Elemento de servidor &#40;ASSL&#41;](../objects/server-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  
