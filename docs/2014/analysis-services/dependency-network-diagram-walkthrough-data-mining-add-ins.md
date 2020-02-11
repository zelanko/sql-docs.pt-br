---
title: Explicação do diagrama de rede de dependências (suplementos de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Visio shapes, dependency network
- shapes, data mining
- shapes, network
- dependencies
- diagram, dependency network
- data mining layout toolbar
- dependency network
ms.assetid: aac732a8-5262-4649-b7d7-3ccf6f9cfa8b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: db069b243a0d06c142651ab4dcadd68e1e06657f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081966"
---
# <a name="dependency-network-diagram-walkthrough-data-mining-add-ins"></a>Passo a passo do diagrama de rede de dependências (Suplementos de Mineração de Dados)
  Vários tipos diferentes de modelos de mineração de dados usam um gráfico de rede como uma maneira de explorar relações nos dados. Você pode importar esses modelos para o Visio usando a forma de **rede de dependência** e, em seguida, continuar a personalizar e aprimorar o layout. As **formas de mineração de dados para o Visio** incluem os seguintes controles personalizados para trabalhar com diagramas de rede de dependência:  
  
-   Controles de renderização para o gráfico da rede  
  
     Essas opções fazem parte do assistente que é iniciado quando você solta uma forma no workspace do Visio.  
  
-   Barra de ferramentas **layout de mineração de dados**  
  
     Essas opções são adicionadas ao workspace do Visio para ajudá-lo a interagir com o gráfico de rede de dependências.  
  
## <a name="build-a-dependency-network-graph"></a>Criar um gráfico de rede de dependências  
 Você solta uma forma na página do Visio para iniciar o **Assistente de forma de rede de dependência do Visio** e definir opções de diagrama.  
  
#### <a name="use-the-dependency-net-visio-shape-wizard"></a>Usar o Assistente para Criar Formas da Rede de Dependências do Visio  
  
1.  Se você não vir **as formas de mineração de dados da Microsoft** na lista **formas** , clique em **mais formas**, selecione **Abrir Estêncil**e abra o modelo no local de instalação padrão.  
  
     \<unidade>: \Program Files (x85) \Microsoft SQL Server 2012 DM Add-ins  
  
2.  Arraste a forma **rede de dependências** até a página para iniciar o assistente. Clique em **Próximo**.  
  
3.  Na página Bem-vindo do **Assistente de forma da rede de dependência do Visio**, clique em **Avançar**.  
  
4.  Na página **selecionar uma fonte de dados** do **Assistente de forma de rede de dependência do Visio**, escolha uma [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] conexão com um servidor que tenha o modelo que você deseja visualizar.  
  
5.  Selecione um modelo de mineração apropriado e clique em **Avançar**.  
  
     Para selecionar um modelo apropriado, você pode examinar o nome, a descrição, as colunas e o tipo de dados no painel **Propriedades** .  
  
     Essa forma dá suporte a modelos criados usando esses algoritmos:  
  
    -   Naïve Bayes  
  
    -   Árvores de decisão  
  
    -   Regras de associação  
  
6.  Na página, **Selecione os nós a serem renderizados**, personalize o tamanho do grafo e, opcionalmente, filtre para incluir apenas determinados nós.  
  
     Com um grande conjunto de grandes, um grafo de dependência pode se tornar enorme e conter muitos objetos relacionados, representados como *nós*. Ao usar essa caixa de diálogo, você poderá criar um gráfico de rede personalizado que inclui apenas os nós de interesse.  
  
     [espaço reservado de arte]  
  
     **Número de nós da busca**  
     Se o modelo contiver um número de nós inferior ao especificado, essa configuração não terá efeito. Se o modelo contiver mais nós do que o especificado, apenas os nós mais fortes serão exibidos.  
  
     **Nome contém**  
     Deixe esta caixa em branco e clique na seta verde para recuperar todos os nós no modelo.  
  
     Ou digite uma cadeia de caracteres e clique na seta verde para retornar apenas os nós que contêm a cadeia de caracteres especificada.  
  
     A maioria dos modelos que você pode criar com os dados de exemplo não são grandes. Portanto, para este exemplo, aumente o número de nós para 10 e clique na seta verde para executar uma consulta e obter a lista de todos os nós.  
  
7.  Clique em **avançado** para definir as opções de sombreamento e forma para o grafo.  
  
8.  Clique em **fechar** para sair da caixa de diálogo opções **avançadas** e, em seguida, clique em **concluir** para criar o grafo.  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Explorar e modificar o diagrama completo  
 Depois que o Visio criou o grafo de rede de dependências, você poderá continuar a modificar e aumentar o grafo usando os recursos no Visio.  
  
 O gráfico a seguir mostra o layout padrão de um gráfico de rede de dependências.  
  
 [espaço reservado de arte]  
  
1.  Use o controle de **panorâmica e zoom** , na área do **painel de tarefas** da faixa de **modos do modo de exibição** do Visio, para se concentrar em uma seção do grafo e movê-lo pelo diagrama.  
  
2.  Experimente layouts de grafo diferentes fornecidos pela opção de **página Refazer layout** do Visio.  
  
3.  Clique na faixa de **bits suplementos** e, em seguida, exiba uma das barras de ferramentas personalizadas usadas para trabalhar com diagramas de Data Mining:  
  
     **Layout**  
     Otimiza o layout dos nós na página e altera a exibição para que todos os nós fiquem visíveis.  
  
     **Redimensionar Página**  
     Altera o tamanho da página para que todos os nós fiquem visíveis.  
  
     **Intensidade da Borda**  
     Alterna a exibição da intensidade da borda para todo o gráfico. Uma borda é uma conexão entre dois nós. Você pode usar o controle deslizante para filtrar as conexões que não são intensas.  
  
     **Controle deslizante**  
     O **controle deslizante** ajuda a controlar a força das relações que são exibidas no diagrama de rede de dependência.  
  
     Cada nó exibido no gráfico representa um estado. Uma seta representa uma transição entre dois estados e a probabilidade associada a ela. Para reduzir o número de nós no gráfico, mova a barra de controle deslizante para cima.  
  
     Para aumentar o número de nós no gráfico, mova a barra de controle deslizante para baixo.  
  
     **Adicionar itens**  
     Abre a caixa de diálogo **selecionar nós a serem renderizados** para que você possa selecionar novos nós para adicionar ao grafo.  
  
4.  Você pode fazer gráficos simples ou elaborados como quiser e adicionar anotações, enquanto permanece conectado ao modelo.  
  
     [espaço reservado para arte]  
  
> [!WARNING]  
>  O realce de nós dependentes e outras opções do menu de atalho que estavam disponíveis em versões anteriores dos Suplementos não funcionam no Office 2013.  
  
## <a name="see-also"></a>Consulte Também  
 [Solução de problemas de diagramas de mineração de dados do Visio &#40;SQL Server suplementos de mineração de dados&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
