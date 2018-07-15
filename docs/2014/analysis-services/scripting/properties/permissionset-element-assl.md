---
title: Elemento PermissionSet (ASSL) | Microsoft Docs
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
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 471ef43aea9fadcca7ab8a4a36870a3bdddee22f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263462"
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
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
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
  
  
