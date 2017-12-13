---
title: "Detalhamento em modelos de mineração | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f179a467-7d03-4d61-8e9a-6b5afb5fc2d5
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7bed3bba2747522da34c16ad97ec8efcdc080c99
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="drillthrough-on-mining-models"></a>Detalhamento em modelos de mineração
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]*Detalhamento* significa ter a capacidade de consultar um modelo de mineração ou uma estrutura de mineração e obter dados detalhados não exposta no modelo.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oferece duas opções diferentes de detalhamento em dados de caso. Você pode detalhar os casos que foram utilizados para criar dados ou os casos na estrutura de mineração.  
  
## <a name="drillthrough-to-model-cases-vs-drillthrough-to-structure"></a>Detalhar para casos do modelo vs. Detalhar para estrutura  
 O detalhamento para **casos do modelo** é útil para localizar detalhes adicionais sobre regras, padrões ou clusters em um modelo. Por exemplo, você não usaria informações de contato de cliente para análise em um modelo de clustering, mesmo que os dados estivessem disponíveis, usando detalhamento. Você pode obter acesso a essas informações no modelo.  
  
 Em contraste, os dados **detalhamento para estrutura** visam fornecer acesso a informações que não foram disponibilizadas no modelo. Por exemplo, algumas colunas de estrutura podem ter sido excluídas de um modelo porque o tipo de dados era incompatível ou os dados não eram úteis para a análise.  
  
## <a name="enabling-drillthrough-on-a-model"></a>Habilitando o detalhamento em um modelo  
 Para usar o detalhamento em um modelo de mineração, as seguintes condições precisam ser atendidas:  
  
-   É possível configurar o detalhamento somente nos casos de modelo e não na estrutura de mineração, mas não vice-versa.  Em outras palavras, o detalhamento deve estar habilitado no modelo de mineração para permitir detalhamento para a estrutura de mineração.  
  
-   O detalhamento no modelo e na estrutura está desabilitado por padrão. Se você utilizar o Assistente de Mineração de Dados, a opção para habilitar o detalhamento para os casos de modelos estará na página final do assistente.  
  
-   Você pode acrescentar a habilidade de detalhamento em um modelo de mineração existente, mas se fizer isso, o modelo deve ser reprocessado antes da análise dos dados.  
  
-   O detalhamento não funcionará a menos que o cache que foi criado durante o processo de treinamento tenha sido preservado. Para obter mais informações sobre as propriedades que controlam o cache, consulte [Drillthrough em estruturas de mineração](../../analysis-services/data-mining/drillthrough-on-mining-structures.md).  
  
## <a name="models-that-support-drillthrough"></a>Modelos que dão suporte a detalhamento  
 Se um modelo de mineração estiver configurado para permitir os detalhamento e se você tiver as permissões adequadas, quando procurar o modelo, poderá clicar em um nó no visualizador apropriado e recuperar informações detalhadas sobre os casos naquele nó específico.  
  
 Nem todos os modelos dão suporte a detalhamento; depende do algoritmo utilizado para criar o modelo. A tabela a seguir lista os tipos de modelos que não dão suporte a detalhamento ou dão suporte a detalhamento com limitações. Se o tipo de modelo não estiver listado aqui, o detalhamento terá suporte.  
  
|**Nome do algoritmo**|**Suporte para detalhamento**|  
|------------------------|----------------------------------|  
|Algoritmo Microsoft Naïve Bayes|Sem suporte.<br /><br /> Estes algoritmos não atribuem casos a nós específicos no conteúdo.|  
|Algoritmo Rede Neural da Microsoft|Sem suporte.<br /><br /> Estes algoritmos não atribuem casos a nós específicos no conteúdo.|  
|Algoritmo Regressão Logística da Microsoft|Sem suporte.<br /><br /> Estes algoritmos não atribuem casos a nós específicos no conteúdo.|  
|Algoritmo Regressão Linear da Microsoft|Tem suporte.<br /><br /> Porém, como o modelo cria um único nó, **All**, o detalhamento retorna todos os casos de treinamento para o modelo. Se o conjunto de treinamento for grande, o carregamento dos resultados poderá demorar muito tempo.|  
|Algoritmo Microsoft Time Series|Tem suporte.<br /><br /> Porém, você não pode detalhar a estrutura nem os dados de casos utilizando o **Visualizador de Modelo de Mineração** no Designer de Mineração de Dados. Em vez disso, você deve criar uma consulta DMX.<br /><br /> Além disso, você não pode detalhar nós específicos nem gravar uma consulta DMX para recuperar casos em nós específicos do modelo Time Series. Você pode recuperar dados de casos a partir da redução do modelo ou da estrutura utilizando outros critérios, como valores data ou de atributo.<br /><br /> Se você quiser ver detalhes dos nós ARTXP e ARIMA criados pelo algoritmo MTS, poderá ser mais fácil utilizar o [Visualizador de árvore de conteúdo genérica da Microsoft &#40;Data Mining&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).|  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 Consulte os tópicos a seguir para obter mais informações sobre como usar o detalhamento com modelos de mineração.  
  
|Tarefas|Links|  
|-----------|-----------|  
|Usar detalhamento nos visualizadores do modelo de mineração|[Usar detalhamento dos visualizadores do modelo](../../analysis-services/data-mining/use-drillthrough-from-the-model-viewers.md)|  
|Recuperar dados de caso para um modelo usando detalhamento|[Detalhar dados do caso a partir do modelo de mineração](../../analysis-services/data-mining/drill-through-to-case-data-from-a-mining-model.md)|  
|Habilitar o detalhamento em um modelo de mineração existente|[Habilitar o detalhamento para um modelo de mineração](../../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)|  
|Veja exemplos de consultas de detalhamento para tipos de modelo específicos.|[Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md)|  
|Habilitar detalhamento no assistente do modelo de mineração|[Concluindo o assistente &#40;Assistente de Data Mining&#41;](http://msdn.microsoft.com/library/6aef1548-35eb-42fd-ae87-63650a79eda1).|  
  
## <a name="see-also"></a>Consulte também  
 [Drillthrough em estruturas de mineração](../../analysis-services/data-mining/drillthrough-on-mining-structures.md)  
  
  
