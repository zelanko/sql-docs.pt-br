---
title: Passo a passo o diagrama de árvore (suplementos de mineração de dados) de decisão | Microsoft Docs
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
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66082277"
---
# <a name="decision-tree-diagram-walkthrough--data-mining-add-ins"></a>Passo a passo o diagrama de árvore de decisão (suplementos de mineração de dados)
  Se você criou um modelo de árvore de decisão, pode criar um diagrama personalizado no Visio usando a forma da Árvore de Decisão ou a forma de Rede de Dependências. Este tópico descreve as personalizações que você pode executar usando o **árvore de decisão** forma e esses controles:  
  
-   Controles de renderização para o diagrama de árvore de decisão  
  
     Essas opções fazem parte dos **Assistente de árvore de decisão** que é iniciado quando você solta uma forma no espaço de trabalho do Visio.  
  
-   **Layout de mineração de dados** barra de ferramentas  
  
     Essas opções são adicionadas ao workspace do Visio para ajudá-lo a interagir com a forma.  
  
## <a name="build-a-decision-tree-diagram"></a>Criar um diagrama de árvore de decisão  
 Você solta a forma da árvore de decisão na página do Visio para iniciar o **Assistente para criar formas do Visio árvore de decisão** e defina as opções do diagrama.  
  
#### <a name="use-the-decision-tree-wizard"></a>Use o Assistente de Árvore de Decisão  
  
1.  Se você não vir **formas de mineração de dados do Microsoft** na **formas** , clique em **mais formas**, selecione **Abrir estêncil**e abra o modelo do local de instalação padrão.  
  
     \<drive>:\Program files (x85)\Microsoft SQL Server 2012 DM Add-Ins  
  
2.  Arraste o **árvore de decisão** forma na página.  
  
3.  Na página de boas-vinda a **Assistente para criar formas do Visio árvore de decisão**, clique em **próxima**.  
  
4.  No **selecionar uma fonte de dados** página do **Assistente de Cluster**, escolha uma conexão para um [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] server que tem o modelo que você deseja visualizar.  
  
5.  Selecione um modelo de mineração apropriado e, em seguida, clique em **próxima**.  
  
     Esse tipo de diagrama dá suporte a modelos criados usando o algoritmo árvores de decisão ou Regressão Linear.  
  
6.  Sobre o **selecionar árvore de decisão** , escolha uma árvore individual para exibir.  
  
     Uma árvore modela as interações que levam a um resultado específico que você modelou; Portanto, mesmo se seu modelo contiver vários resultados, você pode exibir somente uma única árvore por vez.  
  
7.  No **selecionar árvore de decisão** caixa de diálogo, você também pode definir essas opções de renderização:  
  
     **Profundidade de renderização máxima**  
     Use esta opção para controlar quantos nós são exibidos.  
  
     Uma árvore de decisão pode ser muito profunda, criando um diagrama que não caiba na página. Use este controle para focalizar nos nós mais à esquerda, que são mais importantes.  
  
     O padrão é três níveis de nós.  
  
     **Selecionar cor e exibir o texto para valores**  
     Escolher a cor que representará cada um dos resultados. Se você não especificar cores, elas serão geradas automaticamente usando as cores de tema do vídeo atual.  
  
8.  Clique em **avançado** para personalizar as seguintes opções para cada um de nós no diagrama da árvore de decisão.  
  
     **Variável de sombreamento** e **estado**  
     Escolha o resultado pretendido que você deseja exibir no diagrama da árvore.  
  
     **Mostrar Histograma**  
     Adiciona um gráfico para cada nó que mostra as regras que definem esse nó.  
  
     **Mostrar rótulo**  
     Adiciona nomes de coluna ao histograma.  
  
     **Mostrar probabilidade**  
     Exibe a probabilidade de cada valor.  
  
     **Mostrar suporte**  
     Exibe o suporte para cada valor.  
  
     **Mostrar rodapé**  
     Adiciona um rodapé que soma todos os valores exibidos.  
  
     **Mostrar cabeçalho**  
     Adiciona títulos de coluna.  
  
     **Mostrar estados sem nenhum suporte**  
     Permite que você exiba valores ausentes.  
  
9. Clique em **concluir** para criar o gráfico.  
  
    > [!WARNING]  
    >  Em alguns ambientes, os conectores no gráfico podem não ser renderizados no Office 2013.  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Explorar e modificar o diagrama completo  
 Depois de concluir a **Assistente para criar formas do Visio árvore de decisão**, Visio cria um diagrama de árvore na página que exibe graficamente as regras que levam ao resultado esperado.  
  
 Você pode continuar modificando a forma usando os seguintes controles para diagramas da árvore de decisão:  
  
#### <a name="using-the-decision-tree-option-menus"></a>Usando os menus de opção da árvore de decisão  
  
1.  Clique o **Add-Ins** faixa de opções e, em seguida, exiba uma das barras de ferramentas personalizadas usadas para trabalhar com diagramas de mineração de dados:  
  
     **Layout**  
     Otimiza a organização da árvore para caber na página atual.  
  
     **Redimensionar página**  
     Esse controle foi planejado para versões anteriores do HTML. Use a página do Visio em vez disso, os controles de redimensionamento  
  
     **Descrição**  
     Quando um nó da árvore é selecionado, clique nessa opção para exibir detalhes sobre os casos no nó.  
  
2.  Use o **Refazer Layout da página** opção no Visio **Design** faixa de opções para fazer experiências com diferentes layouts da árvore.  
  
3.  Use o **conectores** opção a **Design** tab para mudar os conectores usados entre os nós na árvore.  
  
4.  Use o **Panorâmica e Zoom** controlar, o **painel de tarefas** área do Visio **exibição** faixa de opções, para se concentrar em uma área específica do diagrama.  
  
5.  Clique com o botão direito do mouse em qualquer nó na árvore, e escolha dessas opções de menu de atalho específicas dos diagramas de árvore de decisão:  
  
     **Melhorar o Layout de página**  
     Distribui os nós uniformemente na página e ajusta a exibição da página para visualização de todos os nós.  
  
     **Mover filhos para a nova página**  
     Move os filhos do nó selecionado atualmente para uma nova página.  
  
     **Recolher nós filho**  
     Oculta os filhos do nó selecionado no momento.  
  
     **Expanda nós filho**  
     Exibe os filhos do nó selecionado no momento.  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas de diagramas de mineração de dados do Visio &#40;suplementos de mineração de dados do SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
