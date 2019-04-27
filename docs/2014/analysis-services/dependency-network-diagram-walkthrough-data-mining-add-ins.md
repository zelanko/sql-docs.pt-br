---
title: Passo a passo o diagrama de rede de dependências (suplementos de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
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
ms.openlocfilehash: 0f8d69e97aa542d89291d81d60177e520e6a007b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62732172"
---
# <a name="dependency-network-diagram-walkthrough-data-mining-add-ins"></a>Passo a passo do diagrama de rede de dependências (Suplementos de Mineração de Dados)
  Vários tipos diferentes de modelos de mineração de dados usam um gráfico de rede como uma maneira de explorar relações nos dados. Você pode importar esses modelos no Visio usando a **rede de dependências** forma e, em seguida, continuar a personalizar e aprimorar o layout. O **formas de mineração de dados para Visio** incluem os seguintes controles personalizados para trabalhar com diagramas de rede de dependência:  
  
-   Controles de renderização para o gráfico da rede  
  
     Essas opções fazem parte do assistente que é iniciado quando você solta uma forma no workspace do Visio.  
  
-   **Layout de mineração de dados** barra de ferramentas  
  
     Essas opções são adicionadas ao workspace do Visio para ajudá-lo a interagir com o gráfico de rede de dependências.  
  
## <a name="build-a-dependency-network-graph"></a>Criar um gráfico de rede de dependências  
 Você solta uma forma na página do Visio para iniciar o **Assistente de forma do Visio Net dependência** e defina as opções do diagrama.  
  
#### <a name="use-the-dependency-net-visio-shape-wizard"></a>Usar o Assistente para Criar Formas da Rede de Dependências do Visio  
  
1.  Se você não vir **formas de mineração de dados do Microsoft** na **formas** , clique em **mais formas**, selecione **Abrir estêncil**e abra o modelo do local de instalação padrão.  
  
     \<drive>:\Program files (x85)\Microsoft SQL Server 2012 DM Add-Ins  
  
2.  Arraste o **rede de dependências** forma até a página para iniciar o assistente. Clique em **Avançar**.  
  
3.  Na página de boas-vinda a **Assistente para criar dependência rede Visio formas**, clique em **próxima**.  
  
4.  No **selecionar uma fonte de dados** página do **Assistente para criar dependência rede Visio formas**, escolha uma conexão para um [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] server que tem o modelo que você deseja visualizar.  
  
5.  Selecione um modelo de mineração apropriado e, em seguida, clique em **próxima**.  
  
     Para selecionar um modelo apropriado, você pode examinar o nome, descrição, colunas e tipo de dados do **propriedades** painel.  
  
     Essa forma dá suporte a modelos criados usando esses algoritmos:  
  
    -   Naïve Bayes  
  
    -   Árvores de decisão  
  
    -   Regras de associação  
  
6.  Na página de **selecionar nós para renderização**, personalizar o tamanho do gráfico e, opcionalmente, filtrar para incluir apenas alguns nós.  
  
     Com um grande conjunto de dados, um gráfico de dependência pode se tornar grande e conter vários objetos relacionados, representados como *nós*. Ao usar essa caixa de diálogo, você poderá criar um gráfico de rede personalizado que inclui apenas os nós de interesse.  
  
     [espaço reservado para arte]  
  
     **Número de nós da busca**  
     Se o modelo contiver um número de nós inferior ao especificado, essa configuração não terá efeito. Se o modelo contiver mais nós do que o especificado, apenas os nós mais fortes serão exibidos.  
  
     **O nome contém**  
     Deixe esta caixa em branco e clique na seta verde para recuperar todos os nós no modelo.  
  
     Ou digite uma cadeia de caracteres e clique na seta verde para retornar apenas os nós que contêm a cadeia de caracteres especificada.  
  
     A maioria dos modelos que você pode criar com os dados de exemplo não são grandes. Portanto, para este exemplo, aumente o número de nós para 10 e clique na seta verde para executar uma consulta e obter a lista de todos os nós.  
  
7.  Clique em **avançado** para definir opções de sombreamento e forma para o gráfico.  
  
8.  Clique em **feche** para sair de **avançado** caixa de diálogo Opções e clique **concluir** para criar o gráfico.  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Explorar e modificar o diagrama completo  
 Depois que o Visio criou o grafo de rede de dependências, você poderá continuar a modificar e aumentar o grafo usando os recursos no Visio.  
  
 O gráfico a seguir mostra o layout padrão de um gráfico de rede de dependências.  
  
 [espaço reservado para arte]  
  
1.  Use o **Panorâmica e Zoom** controlar, o **painel de tarefas** área do Visio **exibição** faixa de opções, para focalizar em uma seção do gráfico e navegar em torno do diagrama.  
  
2.  Teste com diferentes layouts de gráfico fornecidos pelo Visio **Refazer Layout da página** opção.  
  
3.  Clique o **Add-Ins** faixa de opções e, em seguida, exiba uma das barras de ferramentas personalizadas usadas para trabalhar com diagramas de mineração de dados:  
  
     **Layout**  
     Otimiza o layout dos nós na página e altera a exibição para que todos os nós fiquem visíveis.  
  
     **Redimensionar página**  
     Altera o tamanho da página para que todos os nós fiquem visíveis.  
  
     **Edge Strength**  
     Alterna a exibição da intensidade da borda para todo o gráfico. Uma borda é uma conexão entre dois nós. Você pode usar o controle deslizante para filtrar as conexões que não são intensas.  
  
     **Slider**  
     O **controle deslizante** ajuda a controlar a intensidade das relações que são exibidos no diagrama de rede de dependência.  
  
     Cada nó exibido no gráfico representa um estado. Uma seta representa uma transição entre dois estados e a probabilidade associada a ela. Para reduzir o número de nós no gráfico, mova a barra de controle deslizante para cima.  
  
     Para aumentar o número de nós no gráfico, mova a barra de controle deslizante para baixo.  
  
     **Adicionar itens**  
     Abre o **selecionar nós para renderização** caixa de diálogo para que você possa selecionar novos nós para adicionar ao gráfico.  
  
4.  Você pode fazer gráficos simples ou elaborados como quiser e adicionar anotações, enquanto permanece conectado ao modelo.  
  
     [espaço reservado para arte]  
  
> [!WARNING]  
>  O realce de nós dependentes e outras opções do menu de atalho que estavam disponíveis em versões anteriores dos Suplementos não funcionam no Office 2013.  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas de diagramas de mineração de dados do Visio &#40;suplementos de mineração de dados do SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
