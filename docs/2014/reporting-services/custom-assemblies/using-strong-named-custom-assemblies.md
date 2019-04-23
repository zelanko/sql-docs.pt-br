---
title: Usando assemblies de nome forte personalizados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- AllowPartiallyTrustedCallersAttribute attribute
- strong-named custom assemblies [Reporting Services]
- strong names [Reporting Services]
- assemblies [Reporting Services], strong names
- custom assemblies [Reporting Services], strong-named
ms.assetid: ca9f19d7-6e86-46f2-b9ad-9bf807eaa52e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5e685ecda39e0487eb4b469920820fa6e4a10daa
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60153901"
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
 [Usar assemblies personalizados com relatórios](using-custom-assemblies-with-reports.md)  
  
  
