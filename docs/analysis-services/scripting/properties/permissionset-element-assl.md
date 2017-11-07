---
title: Elemento PermissionSet (ASSL) | Microsoft Docs
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
- PermissionSet Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- PermissionSet
helpviewer_keywords:
- PermissionSet element
ms.assetid: da5a9175-48e4-4b5e-a780-3e0077939974
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d1448c3db59f149697fa429e6d122d9d20fd403f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Safe*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Safe*|Somente computação interna e acesso a dados local são permitidos. *Safe* é o conjunto de permissões mais restritivo. O código executado por um assembly com as permissões *Safe* não pode acessar recursos externos do sistema, como arquivos, rede, variáveis de ambiente ou Registro.|  
|*ExternalAccess*|*Safe*, com a habilidade adicional para acessar recursos externos do sistema, como arquivos, redes, variáveis de ambiente e registro.|  
|*Irrestrito*|Unrestricted permite aos assemblies acesso irrestrito aos recursos, dentro e fora de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O código executado a partir de um assembly *Unrestricted* pode chamar o código não gerenciado.|  
  
 A enumeração que corresponde aos valores permitidos para **PermissionSet** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.PermissionSet>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados ComAssembly &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)   
 [Elemento assemblies &#40; ASSL &#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [Elemento de banco de dados &#40; ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Elemento Server &#40; ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

