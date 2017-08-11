---
title: Usando Assemblies personalizados de nome forte | Microsoft Docs
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
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- AllowPartiallyTrustedCallersAttribute attribute
- strong-named custom assemblies [Reporting Services]
- strong names [Reporting Services]
- assemblies [Reporting Services], strong names
- custom assemblies [Reporting Services], strong-named
ms.assetid: ca9f19d7-6e86-46f2-b9ad-9bf807eaa52e
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: cf8ee5462bd75ab82ea4296a5b71136cb2eb9ee9
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="using-strong-named-custom-assemblies"></a>Usando assemblies de nome forte personalizados
  Um nome forte identifica um assembly e inclui seu nome de texto, o número de versão de quatro partes, informações de cultura (se fornecidas), uma chave pública e uma assinatura digital armazenada no manifesto do assembly. Um nome forte identifica exclusivamente um assembly para o CLR (common language runtime) e garante a integridade binária.  
  
## <a name="using-allowpartiallytrustedcallersattribute"></a>Usando AllowPartiallyTrustedCallersAttribute  
 Para usar assemblies de nome forte com relatórios, você deve permitir que o assembly de nome forte a ser chamado por código parcialmente confiável usando o assembly **AllowPartiallyTrustedCallers** atributo. Você pode usar **AllowPartiallyTrustedCallersAttribute** para permitir que os assemblies de nome forte a ser chamado pelo Designer de relatórios ou o servidor de relatório em expressões de relatório. Para permitir que o código parcialmente confiável chame assemblies de nome forte, adicione o atributo de nível de assembly a seguir ao seu arquivo de atributo de assembly.  
  
```vb  
<assembly:AllowPartiallyTrustedCallers>  
```  
  
```csharp  
[assembly:AllowPartiallyTrustedCallers]  
```  
  
 **AllowPartiallyTrustedCallersAttribute** só será efetivo quando aplicado por um assembly de nome forte ao nível de assembly. Para obter mais informações sobre como aplicar atributos em nível de assembly, consulte "Aplicando atributos" a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] documentação do SDK.  
  
> [!CAUTION]  
>  Quando **AllowPartiallyTrustedCallersAttribute** estiver presente, o padrão **FullTrustLinkDemand** verificações de segurança são impedidas, tornar acessível de qualquer outro assembly parcialmente confiável assembly. Todas as verificações de segurança, incluindo os atributos de segurança declarativos de nível de classe e de nível de método, devem ser declaradas de forma explícita.  
  
## <a name="see-also"></a>Consulte também  
 [Usar assemblies personalizados com relatórios](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
