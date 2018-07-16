---
title: Requisitos de implementação de item de relatório personalizado | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- custom report items
ms.assetid: cfacd816-00d6-4a3d-be72-1bba6f7f6886
caps.latest.revision: 22
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: fb91618c5fb39795b3b55bb92d1741509b3d4169
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37221046"
---
# <a name="custom-report-item-implementation-requirements"></a>Requisitos de implementação de item de relatório personalizado
  Este tópico descreverá os pré-requisitos para desenvolver e implantar itens de relatório personalizados.  
  
## <a name="development-and-deployment-requirements"></a>Desenvolvimento e implantação de requisitos  
 O desenvolvimento de um item de relatório personalizado para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] exige o seguinte:  
  
-   Acesso administrativo a um servidor que executa o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
-   [!INCLUDE[vsprvsext](../../includes/vsprvsext-md.md)] ou superior com o SDK (Software Development Kit) do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] instalado.  
  
-   Acesso à documentação do SDK do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
-   Familiaridade com a criação de componente e namespaces do modelo do componente no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Para obter mais informações, consulte "Criação de componente" e "Namespaces do Modelo de Componente no Visual Studio" no msdn.microsoft.com.  
  
## <a name="language-and-namespace-requirements"></a>Requisitos de idioma e namespace  
 Os itens de relatório personalizados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dão suporte total ao [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Você pode desenvolver itens de relatório personalizados usando a sua opção de idiomas em conformidade com .NET.  
  
 O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] oferece ao desenvolvedor muitas ferramentas e recursos para simplificar e acelerar os ciclos iterativos de codificação, depuração e teste, e para facilitar a implantação. O [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK inclui o [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] e, os compiladores C# e ferramentas relacionadas.  
  
-   Os itens de relatório personalizados usam o `Microsoft.ReportDesigner` e os namespaces do <xref:Microsoft.ReportingServices.Interfaces>. Eles são armazenados no Microsoft.ReportingServices.Designer.DLL e Microsoft.ReportingServices.Interfaces.DLL assembly que são instalados como parte do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Os componentes de tempo de design do item de relatório personalizado precisa implementar interfaces do namespace do <xref:System.ComponentModel> no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. O <xref:System.ComponentModel> é documentado na documentação do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]SDK.  
  
> [!IMPORTANT]  
>  Por padrão, o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] é instalado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas não com o SDK de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  A menos que o SDK esteja instalado no computador e a documentação do SDK esteja incluída na coleção de manuais online, os links para o conteúdo do SDK desta seção não funcionarão. Depois de instalar o SDK do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], você pode adicionar a documentação do SDK à coleção de Manuais Online e ao sumário seguindo as instruções fornecidas em [Adicionar ou remover a documentação do produto do SQL Server](../../2014-toc/books-online-for-sql-server-2014.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criando um componente de item de relatório personalizado em tempo de execução](creating-a-custom-report-item-run-time-component.md)   
 [Criando um componente de item de relatório personalizado em tempo de design](creating-a-custom-report-item-design-time-component.md)   
 [Como implantar um item de relatório personalizado](how-to-deploy-a-custom-report-item.md)   
 [Bibliotecas de classes de itens de relatório personalizados](custom-report-item-class-libraries.md)  
  
  
