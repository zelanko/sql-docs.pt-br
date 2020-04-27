---
title: Caixa de diálogo análise de impacto (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.process.impactanalysisdialog.f1
ms.assetid: 208268eb-4e14-44db-9c64-6f74b776adb6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0c08690cd2f5b77471392cab3aad1587b4cb0f9a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080747"
---
# <a name="impact-analysis-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Análise de Impacto (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Análise de Impacto** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para identificar e opcionalmente processar objetos dependentes que sejam afetados se os objetos listados na caixa de diálogo **Processo** forem processados. É possível exibir a caixa de diálogo **Análise de Impacto** clicando em **Análise de Impacto** na caixa de diálogo **Processar** .  
  
> [!NOTE]  
>  Um objeto aparecerá mais de uma vez se for afetado de mais de uma maneira.  
  
## <a name="options"></a>Opções  
 **Lista de objetos**  
 Exibe uma lista de objetos dependentes em uma grade. A grade contém as seguintes colunas:  
  
 **Nome do objeto**  
 Exibe o nome do objeto dependente que pode precisar ser processado. O ícone à esquerda do nome indica o tipo do objeto.  
  
 **Tipo**  
 Exibe o tipo do objeto dependente que pode precisar ser processado.  
  
 **Tipo de Impacto**  
 Exibe o efeito que o processamento dos objetos na caixa de diálogo **Processar** tem sobre o objeto dependente. A tabela a seguir lista os efeitos possíveis do processamento e indica se cada um deles resulta em um aviso ou erro.  
  
|Impacto|Mensagem|  
|------------|-------------|  
|O objeto será limpo (não processado)|Aviso|  
|O objeto será inválido|Erro|  
|A agregação será cancelada|Aviso|  
|A agregação flexível será cancelada|Aviso|  
|Os índices serão cancelados|Aviso|  
|O objeto não filho será processado|Aviso|  
  
 **Objeto de Processo**  
 Selecione os objetos dependentes que você quer processar com a operação de processamento. Objetos dependentes que não estão selecionados devem ser processados após a conclusão da operação de processamento. Caso contrário, eles não podem ser usados.  
  
## <a name="see-also"></a>Consulte Também  
 [Analysis Services designers e caixas de diálogo &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Caixa de diálogo processo &#40;Analysis Services de dados multidimensionais&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  
