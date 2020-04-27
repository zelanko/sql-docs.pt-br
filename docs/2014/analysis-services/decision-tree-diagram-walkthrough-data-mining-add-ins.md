---
title: Explicação do diagrama de árvore de decisão (suplementos de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- shapes, data mining
- diagram, decision tree
- Visio shapes, decision tree
- decision tree [data mining]
ms.assetid: 9566f6a2-c750-4125-ba5e-42c7251a78c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ef951825144f381ab37a83526ec96321fe43cfec
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66082277"
---
# <a name="decision-tree-diagram-walkthrough--data-mining-add-ins"></a>Explicação do diagrama de árvore de decisão (suplementos de mineração de dados)
  Se você criou um modelo de árvore de decisão, pode criar um diagrama personalizado no Visio usando a forma da Árvore de Decisão ou a forma de Rede de Dependências. Este tópico descreve as personalizações que você pode executar usando a forma de **árvore de decisão** e esses controles:  
  
-   Controles de renderização para o diagrama de árvore de decisão  
  
     Essas opções fazem parte do **Assistente de árvore de decisão** que é iniciado quando você solta uma forma no espaço de trabalho do Visio.  
  
-   Barra de ferramentas **layout de mineração de dados**  
  
     Essas opções são adicionadas ao workspace do Visio para ajudá-lo a interagir com a forma.  
  
## <a name="build-a-decision-tree-diagram"></a>Criar um diagrama de árvore de decisão  
 Descartar a forma da árvore de decisão na página do Visio para iniciar o **Assistente de forma da árvore de decisão do Visio** e definir opções de diagrama.  
  
#### <a name="use-the-decision-tree-wizard"></a>Use o Assistente de Árvore de Decisão  
  
1.  Se você não vir **as formas de mineração de dados da Microsoft** na lista **formas** , clique em **mais formas**, selecione **Abrir Estêncil**e abra o modelo no local de instalação padrão.  
  
     \<unidade>: \Program Files (x85) \Microsoft SQL Server 2012 DM Add-ins  
  
2.  Arraste a forma **árvore de decisão** para a página.  
  
3.  Na página inicial do assistente de **forma da árvore de decisão do Visio**, clique em **Avançar**.  
  
4.  Na página **selecionar uma fonte de dados** do **Assistente de cluster**, escolha uma conexão com um [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] servidor que tenha o modelo que você deseja visualizar.  
  
5.  Selecione um modelo de mineração apropriado e clique em **Avançar**.  
  
     Esse tipo de diagrama dá suporte a modelos criados usando as árvores de decisão ou o algoritmo de regressão linear.  
  
6.  Na página **selecionar árvore de decisão** , escolha uma árvore individual a ser exibida.  
  
     Uma árvore modela as interações que levam a um determinado resultado que você modelou; Portanto, mesmo que seu modelo contenha vários resultados, você poderá exibir apenas uma árvore por vez.  
  
7.  Na caixa de diálogo **selecionar árvore de decisão** , você também pode definir estas opções de renderização:  
  
     **Profundidade de renderização máxima**  
     Use esta opção para controlar quantos nós são exibidos.  
  
     Uma árvore de decisão pode ser muito profunda, criando um diagrama que não caiba na página. Use este controle para focalizar nos nós mais à esquerda, que são mais importantes.  
  
     O padrão é três níveis de nós.  
  
     **Selecionar cor e exibir o texto para os valores**  
     Escolher a cor que representará cada um dos resultados. Se você não especificar cores, elas serão geradas automaticamente usando as cores de tema do vídeo atual.  
  
8.  Clique em **avançado** para personalizar as seguintes opções para cada um dos nós no diagrama de árvore de decisão.  
  
     Variável e **estado** de **sombreamento**  
     Escolha o resultado pretendido que você deseja exibir no diagrama da árvore.  
  
     **Mostrar Histograma**  
     Adiciona um gráfico para cada nó que mostra as regras que definem esse nó.  
  
     **Mostrar Rótulo**  
     Adiciona nomes de coluna ao histograma.  
  
     **Mostrar Probabilidade**  
     Exibe a probabilidade de cada valor.  
  
     **Mostrar Suporte**  
     Exibe o suporte para cada valor.  
  
     **Mostrar Rodapé**  
     Adiciona um rodapé que soma todos os valores exibidos.  
  
     **Mostrar Cabeçalho**  
     Adiciona títulos de coluna.  
  
     **Mostrar estados sem nenhum suporte**  
     Permite que você exiba valores ausentes.  
  
9. Clique em **concluir** para criar o grafo.  
  
    > [!WARNING]  
    >  Em alguns ambientes, os conectores no gráfico podem não ser renderizados no Office 2013.  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Explorar e modificar o diagrama completo  
 Depois de concluir o **Assistente de forma da árvore de decisão do Visio**, o Visio cria um diagrama de árvore na página que exibe graficamente as regras que levam ao resultado previsto.  
  
 Você pode continuar modificando a forma usando os seguintes controles para diagramas da árvore de decisão:  
  
#### <a name="using-the-decision-tree-option-menus"></a>Usando os menus de opção da árvore de decisão  
  
1.  Clique na faixa de **bits suplementos** e, em seguida, exiba uma das barras de ferramentas personalizadas usadas para trabalhar com diagramas de Data Mining:  
  
     **Layout**  
     Otimiza a organização da árvore para caber na página atual.  
  
     **Redimensionar Página**  
     Esse controle foi planejado para versões anteriores do HTML. Em vez disso, use os controles redimensionamento de página do Visio,  
  
     **Descrição**  
     Quando um nó da árvore é selecionado, clique nessa opção para exibir detalhes sobre os casos no nó.  
  
2.  Use a opção **página Refazer layout** na faixa de opções **design** do Visio para experimentar diferentes layouts de árvore.  
  
3.  Use a opção **conectores** na guia **design** para alterar os conectores usados entre os nós na árvore.  
  
4.  Use o controle de **panorâmica e zoom** , na área do **painel de tarefas** da faixa de **modos do modo de exibição** do Visio, para se concentrar em uma área específica do diagrama.  
  
5.  Clique com o botão direito do mouse em qualquer nó na árvore, e escolha dessas opções de menu de atalho específicas dos diagramas de árvore de decisão:  
  
     **Aperfeiçoar o Layout de Página**  
     Distribui os nós uniformemente na página e ajusta a exibição da página para visualização de todos os nós.  
  
     **Mover Filhos para a Nova Página**  
     Move os filhos do nó selecionado atualmente para uma nova página.  
  
     **Recolher Nós Filho**  
     Oculta os filhos do nó selecionado no momento.  
  
     **Expandir Nós Filho**  
     Exibe os filhos do nó selecionado no momento.  
  
## <a name="see-also"></a>Consulte Também  
 [Solução de problemas de diagramas de mineração de dados do Visio &#40;SQL Server suplementos de mineração de dados&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
