---
title: Impacto sobre a caixa de diálogo de análise (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.process.impactanalysisdialog.f1
ms.assetid: 208268eb-4e14-44db-9c64-6f74b776adb6
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 02b5ee9613672762c466ba023ccabf1fa90d5892
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299376"
---
# <a name="impact-analysis-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Análise de Impacto (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Análise de Impacto** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para identificar e opcionalmente processar objetos dependentes que sejam afetados se os objetos listados na caixa de diálogo **Processo** forem processados. É possível exibir a caixa de diálogo **Análise de Impacto** clicando em **Análise de Impacto** na caixa de diálogo **Processar** .  
  
> [!NOTE]  
>  Um objeto aparecerá mais de uma vez se for afetado de mais de uma maneira.  
  
## <a name="options"></a>Opções  
 **Lista de objetos**  
 Exibe uma lista de objetos dependentes em uma grade. A grade contém as seguintes colunas:  
  
 **Object Name**  
 Exibe o nome do objeto dependente que pode precisar ser processado. O ícone à esquerda do nome indica o tipo do objeto.  
  
 **Tipo**  
 Exibe o tipo do objeto dependente que pode precisar ser processado.  
  
 **Tipo de impacto**  
 Exibe o efeito que o processamento dos objetos na caixa de diálogo **Processar** tem sobre o objeto dependente. A tabela a seguir lista os efeitos possíveis do processamento e indica se cada um deles resulta em um aviso ou erro.  
  
|Impacto|Mensagem|  
|------------|-------------|  
|O objeto será limpo (não processado)|Aviso|  
|O objeto será inválido|Erro|  
|A agregação será cancelada|Aviso|  
|A agregação flexível será cancelada|Aviso|  
|Os índices serão cancelados|Aviso|  
|O objeto não filho será processado|Aviso|  
  
 **Objeto de processo**  
 Selecione os objetos dependentes que você quer processar com a operação de processamento. Objetos dependentes que não estão selecionados devem ser processados após a conclusão da operação de processamento. Caso contrário, eles não podem ser usados.  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Processar caixa de diálogo &#40;Analysis Services - dados multidimensionais&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  
