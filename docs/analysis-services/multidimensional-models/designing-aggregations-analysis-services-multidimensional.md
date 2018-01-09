---
title: "Projetando agregações (Analysis Services - Multidimensional) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
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
- aggregations [Analysis Services], partitions
- partitions [Analysis Services], aggregations
ms.assetid: 3072b7e0-6961-42ad-a287-16f391f2cec4
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 71e50fc874562cceddc91b454a246b29370cf7c7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="designing-aggregations-analysis-services---multidimensional"></a>Projetando agregações (Analysis Services - multidimensional)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]As agregações são resumos pré-calculados de dados de cubo que ajudam a habilitar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para fornecer rápidas respostas de consultas.  
  
 Para definir opções de armazenamento e projetar agregações para uma partição, use o Assistente de Design de Agregação. O assistente opera em uma única partição de um grupo de medidas por vez, de modo que é possível selecionar opções e projetos diferentes para cada partição. O assistente possui etapas que permitem configurar o armazenamento e projetar agregações para uma partição. Para obter mais informações sobre como configurar o armazenamento, consulte.  
  
 Selecione um método para controlar o número de agregações a serem projetadas e deixe o assistente projetá-las.  
  
 O objetivo é projetar o número ideal de agregações. Esse número não só deve fornecer um tempo de resposta satisfatório, mas também deve impedir o aumento excessivo do tamanho da partição. Um número maior de agregações produz tempos de resposta mais rápidos, mas também requer mais espaço de armazenamento e pode demorar mais para ser calculado. Além disso, como o assistente projeta cada vez mais agregações, as agregações mais antigas têm um ganho de desempenho consideravelmente maior do que as agregações mais recentes. A redução nas agregações menos úteis também aumenta o desempenho. É possível controlar o número de agregações projetadas pelo assistente com um dos seguintes métodos disponíveis:  
  
-   Especifique um limite de espaço de armazenamento para as agregações.  
  
-   Especifique um limite de ganho de desempenho.  
  
-   Pare o assistente manualmente quando a curva de desempenho versus tamanho exibida começar a ficar nivelada em um ganho de desempenho aceitável.  
  
-   Opte por não projetar agregações.  
  
 Para projetar o armazenamento, o assistente deve se conectar ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no servidor de destino. O assistente exibirá uma mensagem de erro se o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não estiver em execução no servidor de destino ou se o processo de projeto do armazenamento não conseguir se conectar ao servidor de destino.  
  
 A etapa final do assistente permite processar ou adiar o processamento. O processamento cria as agregações projetadas com o assistente, enquanto o adiamento salva as agregações projetadas para serem processadas posteriormente, permitindo a continuidade das atividades do projeto sem nenhum processamento. Dependendo do tamanho da partição, o processamento pode demorar algum tempo. Se desejar, você pode interromper o processamento de uma partição.  
  
## <a name="see-also"></a>Consulte Também  
 [Agregações e designs de agregação](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
