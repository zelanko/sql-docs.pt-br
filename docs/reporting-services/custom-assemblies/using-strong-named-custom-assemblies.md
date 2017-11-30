---
title: Usando assemblies de nome forte personalizados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- AllowPartiallyTrustedCallersAttribute attribute
- strong-named custom assemblies [Reporting Services]
- strong names [Reporting Services]
- assemblies [Reporting Services], strong names
- custom assemblies [Reporting Services], strong-named
ms.assetid: ca9f19d7-6e86-46f2-b9ad-9bf807eaa52e
caps.latest.revision: "35"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6aa028091c9076fc3f3d7517344dfaf6f56267da
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="using-strong-named-custom-assemblies"></a>Usando assemblies de nome forte personalizados
  Um nome forte identifica um assembly e inclui seu nome de texto, o número de versão de quatro partes, informações de cultura (se fornecidas), uma chave pública e uma assinatura digital armazenada no manifesto do assembly. Um nome forte identifica exclusivamente um assembly para o CLR (common language runtime) e garante a integridade binária.  
  
## <a name="using-allowpartiallytrustedcallersattribute"></a>Usando AllowPartiallyTrustedCallersAttribute  
 Para usar assemblies de nome forte com relatórios, é necessário permitir que o assembly de nome forte seja chamado por um código parcialmente confiável usando o atributo **AllowPartiallyTrustedCallers** do assembly. Você pode usar **AllowPartiallyTrustedCallersAttribute** para permitir que assemblies de nome forte sejam chamados pelo Designer de Relatórios ou pelo servidor de relatório em expressões de relatório. Para permitir que o código parcialmente confiável chame assemblies de nome forte, adicione o atributo de nível de assembly a seguir ao seu arquivo de atributo de assembly.  
  
```vb  
<assembly:AllowPartiallyTrustedCallers>  
```  
  
```csharp  
[assembly:AllowPartiallyTrustedCallers]  
```  
  
 **AllowPartiallyTrustedCallersAttribute** só será efetivo quando aplicado por um assembly de nome forte no nível de assembly. Para obter mais informações sobre como aplicar atributos no nível de assembly, consulte “Aplicando atributos” na documentação do SDK do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
> [!CAUTION]  
>  Quando **AllowPartiallyTrustedCallersAttribute** estiver presente, as verificações de segurança de **FullTrustLinkDemand** serão impedidas, fazendo com que o assembly possa ser chamado de qualquer outro assembly parcialmente confiável. Todas as verificações de segurança, incluindo os atributos de segurança declarativos de nível de classe e de nível de método, devem ser declaradas de forma explícita.  
  
## <a name="see-also"></a>Consulte também  
 [Usar assemblies personalizados com relatórios](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
