---
title: Exibindo modelos de mineração de dados no Visio (suplementos de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- diagram, modifying
- templates [Visio]
- shapes, data mining
- diagram
ms.assetid: 5841adea-6650-4fae-8526-26af33edbede
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 572bbd3b2c3bbcebbd1b5a829ac193ac0bb909a9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115517"
---
# <a name="viewing-data-mining-models-in-visio-data-mining-add-ins"></a>Exibindo modelos de mineração de dados no Visio (suplementos de mineração de dados)
  As formas do Visio para mineração de dados permitem que você se conecte a um servidor e crie um diagrama representando um modelo de mineração de dados existente. Os diagramas podem ser então personalizados usando controles do Visio, mas você também pode detalhar os dados, expor algumas das estatísticas subjacentes e trabalhar com o modelo subjacente.  
  
## <a name="building-a-model-diagram"></a>Criando um diagrama modelo  
 Quando você abrir o arquivo que contém as formas do Visio para mineração de dados, o **formas** painel mostra as formas a seguir.  
  
 Se você não visualizar as formas de mineração de dados quando abrir o Visio, abra o arquivo de modelo da pasta de instalação.  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 Para usar uma forma, arraste-a para a página. Cada uma das formas abre um assistente diferente, que o ajuda a selecionar dados da fonte, definir opções para o tipo de diagrama específico e especificar sombreamento e outras opções de exibição.  
  
 A tabela a seguir lista os tipos de modelos que podem ser usados com cada tipo de diagrama.  
  
|Formas do Visio|Modelos com suporte|  
|-----------------|----------------------|  
|Árvore de Decisão|Use essa forma para modelos baseados na árvore de decisão ou em algoritmos de regressão linear.|  
|Rede de Dependências|Use essa forma para modelos baseados em qualquer um destes algoritmos: Naive Bayes, Árvores de Decisão ou Regras de Associação.|  
|Cluster|Use essa forma para modelos baseados em algoritmos de clustering.|  
  
 Dependendo do tipo de dados no modelo de mineração, o assistente poderá oferecer opções diferentes. Por exemplo, colunas que contêm números contínuos são visualizadas de maneira diferente que variáveis categóricas.  
  
## <a name="working-with-completed-shapes"></a>Trabalhando com formas completas  
 Quando o diagrama estiver concluído, você poderá usá-lo para procurar o modelo de mineração de dados ou aprimorar o diagrama para uso em apresentações.  
  
### <a name="visio-menus"></a>Menus do Visio  
 O Visio fornece uma variedade de controles de renderização, temas e menus de atalho para ajudar a aprimorar um diagrama.  
  
-   Use os temas do Visio para alterar as cores do diagrama.  
  
-   Alterar conectores ou layout do diagrama.  
  
### <a name="data-mining-menus"></a>Menus de mineração de dados  
 Essas barras de ferramentas e itens de menu são fornecidos pelos suplementos que são específicos para cada forma ou tipo de modelo  
  
-   Cada tipo de diagrama tem um menu de atalho para a forma que permita seu acesso a opções especiais. Embora várias opções nesse menu sejam comuns a todas as formas do Visio, algumas são exclusivas dos modelos de mineração de dados  
  
     Por exemplo, em um diagrama de árvore de decisão, você pode clicar em um nó individual e recolher os nós filho para tornar esse diagrama mais simples ou mover os nós filho para outra página.  
  
-   Como a forma está associada aos dados do modelo, você também poderá fazer algumas explorações usando o diagrama:  
  
     Filtre os nós exibidos ou altere o nível da árvore ou a profundidade do grafo.  
  
     Amplie o zoom em seções específicas, pesquise os nós que contenham um determinado atributo, ou filtre um grafo de dependência por suas extremidades (probabilidade).  
  
## <a name="walkthroughs"></a>Passo a passo  
 Por obter exemplos de como trabalhar com um diagrama preenchido e interpretá-lo, consulte estes tópicos:  
  
 [Passo a passo do diagrama de cluster](cluster-diagram-walkthrough-data-mining-add-ins.md)  
  
 [Instruções passo a passo de diagrama de rede de dependência](dependency-network-diagram-walkthrough-data-mining-add-ins.md)  
  
 [Passo a passo do diagrama de árvore de decisão](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
## <a name="see-also"></a>Consulte também  
 [Procurando modelos no Excel &#40;suplementos de mineração de dados do SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  