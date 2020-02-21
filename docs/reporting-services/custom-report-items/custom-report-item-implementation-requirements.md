---
title: Requisitos de implementação de item de relatório personalizado | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-report-items
ms.topic: reference
helpviewer_keywords:
- custom report items
ms.assetid: cfacd816-00d6-4a3d-be72-1bba6f7f6886
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e25938d690d6e1046d1d0e75ae5a4952b05d4615
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73594517"
---
# <a name="custom-report-item-implementation-requirements"></a>Requisitos de implementação de item de relatório personalizado
  Este tópico descreverá os pré-requisitos para desenvolver e implantar itens de relatório personalizados.  
  
## <a name="development-and-deployment-requirements"></a>Desenvolvimento e implantação de requisitos  
 O desenvolvimento de um item de relatório personalizado para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] exige o seguinte:  
  
-   Acesso administrativo a um servidor que executa o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
-   [!INCLUDE[vsprvsext](../../includes/vsprvsext-md.md)] ou posterior com o SDK (Software Development Kit) do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] instalado.  
  
-   Acesso à documentação do SDK do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] .  
  
-   Familiaridade com a criação de componente e namespaces do modelo do componente no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
## <a name="language-and-namespace-requirements"></a>Requisitos de idioma e namespace  
 Os itens de relatório personalizados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dão suporte total ao [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Você pode desenvolver itens de relatório personalizados usando a sua opção de idiomas em conformidade com .NET.  
  
 O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] oferece ao desenvolvedor muitas ferramentas e recursos para simplificar e acelerar os ciclos iterativos de codificação, depuração e teste, e para facilitar a implantação. O [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK inclui o [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] e, os compiladores C# e ferramentas relacionadas.  
  
-   Os itens de relatório personalizados usam os namespaces **Microsoft.ReportDesigner** e <xref:Microsoft.ReportingServices.Interfaces>. Eles são armazenados no Microsoft.ReportingServices.Designer.DLL e Microsoft.ReportingServices.Interfaces.DLL assembly que são instalados como parte do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Os componentes de tempo de design do item de relatório personalizado precisa implementar interfaces do namespace do <xref:System.ComponentModel> no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. O <xref:System.ComponentModel> é documentado na documentação do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]SDK.  

## <a name="see-also"></a>Consulte Também  
 [Criando um componente de item de relatório personalizado em tempo de execução](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Criando um componente de item de relatório personalizado em tempo de design](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [Como: implantar um item de relatório personalizado](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)   
 [Bibliotecas de classes de itens de relatório personalizados](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)  
  
  
