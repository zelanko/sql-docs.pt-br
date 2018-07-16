---
title: Exibir o XML do Analysis Services (SSDT) do projeto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- projects [Analysis Services], viewing XML
ms.assetid: dd1a4bc6-57b5-47df-8619-09f921aa6351
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: df5f976c08f6c16b73628ce96b459f6fd8b0fc5b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187223"
---
# <a name="view-the-xml-for-an-analysis-services-project-ssdt"></a>Exibir o XML de um projeto do Analysis Services (SSDT)
  Quando você trabalha com um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo de projeto, o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] cria uma definição XML para cada objeto da pasta de projeto. Você pode exibir o conteúdo do arquivo XML de cada objeto do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Pode também editar o arquivo XML diretamente; contudo, isso não é recomendável na maioria das vezes, pois você pode fazer alterações que inviabilizarão a leitura do XML pelo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
> [!NOTE]  
>  Não é possível exibir o código xml do projeto inteiro, mas sim o código de cada objeto, pois existe um arquivo separado para cada um deles. A única maneira de exibir o código para um projeto inteiro é compilar o projeto e exibir o ASSL código no \<nome do projeto >. asdatabase.  
  
### <a name="to-view-the-xml-code-for-an-object"></a>Exibir o código de XML de um objeto  
  
1.  Abra o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no objeto e clique em **Exibir Código**.  
  
     O código XML do objeto aparece no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Criar projetos do Analysis Services &#40;SSDT&#41;](build-analysis-services-projects-ssdt.md)  
  
  
