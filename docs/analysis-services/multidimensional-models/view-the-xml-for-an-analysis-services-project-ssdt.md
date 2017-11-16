---
title: Exibir o XML do Analysis Services (SSDT) do projeto | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- projects [Analysis Services], viewing XML
ms.assetid: dd1a4bc6-57b5-47df-8619-09f921aa6351
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6633f8da10ad176ee86e9bbc61d42b638795a4a2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="view-the-xml-for-an-analysis-services-project-ssdt"></a>Exibir o XML de um projeto do Analysis Services (SSDT)
  Quando você trabalha com um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo de projeto, o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] cria uma definição XML para cada objeto da pasta de projeto. Você pode exibir o conteúdo do arquivo XML de cada objeto do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Pode também editar o arquivo XML diretamente; contudo, isso não é recomendável na maioria das vezes, pois você pode fazer alterações que inviabilizarão a leitura do XML pelo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
> [!NOTE]  
>  Não é possível exibir o código xml do projeto inteiro, mas sim o código de cada objeto, pois existe um arquivo separado para cada um deles. A única maneira de exibir o código para um projeto inteiro é compilar o projeto e exibir o ASSL código o \<nome do projeto >. asdatabase.  
  
### <a name="to-view-the-xml-code-for-an-object"></a>Exibir o código de XML de um objeto  
  
1.  Abra o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no objeto e clique em **Exibir Código**.  
  
     O código XML do objeto aparece no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Criar projetos do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)  
  
  

