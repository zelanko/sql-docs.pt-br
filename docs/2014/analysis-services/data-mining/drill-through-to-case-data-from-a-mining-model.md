---
title: Detalhar os dados de caso de um modelo de mineração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- drillthrough [Analysis Services]
ms.assetid: b4d3f350-e543-4ea9-b3a2-b4f7c0a9ae27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d683c9dc9a201b1f4351ee00d718ad0d7917606
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084607"
---
# <a name="drill-through-to-case-data-from-a-mining-model"></a>Detalhar dados do caso a partir do modelo de mineração
  Se um modelo de mineração foi configurado para permitir que você detalhe os casos de modelo, quando você procurar o modelo, poderá recuperar informações detalhadas sobre os casos usados para criar o modelo. Além do mais, se a estrutura de mineração subjacente tiver sido configurada para permitir o detalhamento para casos de estrutura e você tiver as permissões adequadas, poderá retornar as informações a partir da estrutura de mineração. Isso pode incluir colunas que não foram incluídas no modelo de mineração.  
  
 Se a estrutura de mineração não permitir que você detalhe os dados subjacentes, mas o modelo de mineração permitir, você poderá exibir informações dos casos de modelo e não da estrutura de mineração.  
  
> [!NOTE]  
>  Você pode acrescentar a habilidade de detalhamento em um modelo de mineração existente, configurando a propriedade `AllowDrillthrough` para `True`. Porém, depois que você habilitar o detalhamento, o modelo deverá ser reprocessado antes que você possa ver os dados do caso. Para obter mais informações,consulte [Habilitar drillthrough para um modelo de mineração](enable-drillthrough-for-a-mining-model.md).  
  
 Dependendo do tipo de visualizador utilizado, é possível selecionar o nó a ser detalhado das seguintes formas:  
  
|Nome do visualizador|Painel ou nome da guia|Selecionar nó|  
|-----------------|----------------------|-----------------|  
|**Visualizador de árvore da Microsoft**|Guia **árvore de decisão**|Clique em um nó de árvore.<br /><br /> **Observação** Evite usar o `All` detalhamento no nó, pois pode levar muito tempo para retornar resultados.|  
|**Visualizador de cluster da Microsoft**|**Diagrama de cluster**|Clique em um nó de cluster.|  
|**Visualizador de cluster da Microsoft**|**Perfis de cluster**|Clique em qualquer parte da coluna de cluster.|  
|**Visualizador de associação da Microsoft**|Guia **regras**|Clique em uma linha que contém um conjunto de regras.|  
|**Visualizador de associação da Microsoft**|Guia **conjuntos** de itens|Clique em uma linha que contém um conjunto de itens.|  
|**Visualizador de clustering de sequência da Microsoft**|Guia **regras**|Clique em uma linha que contém um conjunto de regras.|  
|**Visualizador de clustering de sequência da Microsoft**|Guia **conjuntos** de itens|Clique em uma linha que contém um conjunto de itens.|  
  
> [!NOTE]  
>  Alguns modelos não podem usar detalhamento. A capacidade de usar detalhamento depende do algoritmo utilizado para criar o modelo. Para obter uma lista dos tipos de modelo de mineração que dão suporte ao drillthrough, consulte [Consultas de detalhamento &#40;Mineração de dados&#41;](drillthrough-queries-data-mining.md).  
  
### <a name="to-view-drillthrough-data-from-a-mining-model"></a>Para exibir dados de detalhamento de um modelo de mineração  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra a estrutura de mineração que contém o modelo de mineração desejado.  
  
2.  No Designer de Mineração de Dados, clique na guia **Visualizador do Modelo de Mineração** .  
  
3.  Selecione o modelo na lista suspensa **Modelo de Mineração** .  
  
4.  Selecione um visualizador na lista suspensa **Visualizador** e clique com o botão direito do mouse no nó específico.  
  
5.  Selecione **Detalhar**e, em seguida, selecione **Somente Colunas de Modelos**ou **Colunas de Modelo e Estrutura** para abrir a janela **Detalhar** .  
  
6.  Para copiar os dados para a Área de Transferência, clique com o botão direito do mouse na tabela e selecione **Copiar Tudo**.  
  
## <a name="see-also"></a>Consulte Também  
 [Consultas de detalhamento &#40;mineração de dados&#41;](drillthrough-queries-data-mining.md)  
  
  
