---
title: Implantar projetos do Analysis Services (SSDT) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deploy [Analysis Services]
- projects [Analysis Services], deploying
- Business Intelligence Development Studio, deploying projects [Analysis Services]
ms.assetid: 29490a5b-1573-4a35-9277-10c6a6e4ef0e
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dbfe19ac5da2fee064dd19d06aa1bf7992c3429b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="deploy-analysis-services-projects-ssdt"></a>Implantar projetos do Analysis Services (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Durante o desenvolvimento de um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] project no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], frequentemente você implanta o projeto em um servidor de desenvolvimento para criar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados definido pelo projeto. Isso é necessário para testar o projeto; por exemplo, procurar células no cubo, procurar membros da dimensão ou verificar as fórmulas dos KPIs (indicadores chave de desempenho).  
  
## <a name="deploying-a-project"></a>Implantando um projeto  
 É possível implantar um projeto independentemente ou todos os projetos da solução. Quando você implanta um projeto, ocorre uma sequência de fatos. Primeiro, o projeto é criado. Essa etapa cria os arquivos de saída que definem o banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e seus objetos constituintes. Em seguida, o servidor de destino é validado. Por fim, são criados o banco de dados de destino e seus objetos no servidor de destino. Durante a implantação, o mecanismo de implantação substitui completamente todos os bancos de dados preexistentes pelo conteúdo do projeto, exceto se esses objetos foram criados pelo projeto em uma implantação anterior.  
  
 Depois de uma implantação inicial, um arquivo IncrementalSnapshot.xml é gerado no \<nome do projeto > \obj pasta. Ele é usado para determinar se o banco de dados e seus objetos no servidor de destino sofreram alterações fora do projeto. Em caso positivo, será solicitado que você substitua todos os objetos do banco de dados de destino. Se todas as alterações foram feitas dentro do projeto e ele estiver configurado para implantação incremental, somente as alterações serão implantadas no servidor de destino.  
  
 A configuração de projeto e suas configurações associadas determinam as propriedades de implantação que serão usadas para implantar o projeto. No caso de projeto compartilhado, cada desenvolvedor pode usar sua própria configuração com suas próprias opções de configuração de projeto. Por exemplo, cada desenvolvedor pode especificar um servidor de teste diferente para trabalhar isoladamente dos outros desenvolvedores.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um projeto do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)  
  
  
