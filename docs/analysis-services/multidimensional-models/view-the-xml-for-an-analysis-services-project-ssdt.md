---
title: Exibir o XML do Analysis Services (SSDT) do projeto | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 414be39dcf2149df28336de61b267a0c60caede2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="view-the-xml-for-an-analysis-services-project-ssdt"></a>Exibir o XML de um projeto do Analysis Services (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Quando você trabalha com um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo de projeto, o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] cria uma definição XML para cada objeto da pasta de projeto. Você pode exibir o conteúdo do arquivo XML de cada objeto do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Pode também editar o arquivo XML diretamente; contudo, isso não é recomendável na maioria das vezes, pois você pode fazer alterações que inviabilizarão a leitura do XML pelo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
> [!NOTE]  
>  Não é possível exibir o código xml do projeto inteiro, mas sim o código de cada objeto, pois existe um arquivo separado para cada um deles. A única maneira de exibir o código para um projeto inteiro é compilar o projeto e exibir o ASSL código o \<nome do projeto >. asdatabase.  
  
### <a name="to-view-the-xml-code-for-an-object"></a>Exibir o código de XML de um objeto  
  
1.  Abra o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no objeto e clique em **Exibir Código**.  
  
     O código XML do objeto aparece no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Criar projetos do Analysis Services & #40; SSDT & #41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)  
  
  
