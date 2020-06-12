---
title: Instruções do diagrama de cluster (suplementos de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Visio shapes, cluster
- diagram, cluster
- shapes, data mining
- shapes, cluster
- data mining layout toolbar
ms.assetid: 761bef6a-37d4-4b19-944e-f2aadc75a242
author: minewiskan
ms.author: owend
ms.openlocfilehash: 578b5b8e55fd3ae660db985eed2e608667dc768b
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527482"
---
# <a name="cluster-diagram-walkthrough-data-mining-add-ins"></a>Passo a passo do diagrama de Cluster (Suplementos de Mineração de Dados)
  Depois de criar um modelo de clustering, você pode importá-lo para o Visio usando a forma de **cluster** e, em seguida, continuar a personalizar e aprimorar o layout. As **formas de mineração de dados para o Visio** incluem os seguintes controles personalizados para trabalhar com diagramas de Data Mining:  
  
-   Controles de renderização para o diagrama de cluster  
  
     Essas opções fazem parte do **Assistente de cluster** que é iniciado quando você solta uma forma no espaço de trabalho do Visio.  
  
-   Barra de ferramentas **layout de mineração de dados**  
  
     Essas opções são adicionadas ao workspace do Visio para ajudá-lo a interagir com a forma de mineração de dados. As opções são diferentes dependendo do tipo de modelo de mineração de dados que você está usando.  
  
## <a name="build-a-cluster-diagram"></a>Criar um diagrama de cluster  
 Este passo a passo demonstra como criar e personalizar um diagrama de clustering no Visio.  
  
 Para acompanhar, você já deverá ter um modelo de clustering disponível. Se você não tiver um modelo, use o [Assistente de Cluster &#40;suplementos de mineração de dados para o assistente de&#41;do Excel](cluster-wizard-data-mining-add-ins-for-excel.md) e crie um modelo usando o conjunto de dados de treinamento na pasta de trabalho de exemplo, usando todos os padrões.  
  
#### <a name="use-the-cluster-visio-shape-wizard"></a>Use o assistente para Criar Formas Cluster do Visio  
  
1.  Se você não vir **as formas de mineração de dados da Microsoft** na lista **formas** , clique em **mais formas**, selecione **Abrir Estêncil**e abra o modelo no local de instalação padrão.  
  
     \<drive>: \Program files\Microsoft SQL Server 2012 DM Add-ins  
  
2.  Arraste a forma de **cluster** para a página.  
  
3.  Na página inicial do assistente de **forma do Visio do cluster**, clique em **Avançar**.  
  
4.  Na página **selecionar uma fonte de dados** do **Assistente de cluster**, escolha uma conexão com um [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] servidor que contenha os modelos de Data Mining que você deseja visualizar.  
  
5.  Selecione um modelo de mineração apropriado e clique em **Avançar**.  
  
     Para ter certeza de escolher um modelo de clustering, examine a descrição no painel **Propriedades** .  
  
6.  Se a conexão for bem-sucedida, na página **Opções do diagrama de cluster**, você decide qual tipo de diagrama de cluster deve ser incluído na apresentação do Visio:  
  
     **Mostrar formas de cluster somente**  
     Essa opção cria um diagrama de cluster simples, com cada cluster representado por um retângulo ou outra forma que você escolher  
  
     **Mostrar clusters com gráfico de características**  
     Essa opção cria o mesmo gráfico que o anterior, mas dentro das formas estão os histogramas que descrevem as características do cluster.  
  
     ![Exemplo de gráfico de características de cluster no Visio](media/dm13-visio-cluster-samplecharshape.gif "Exemplo de gráfico de características de cluster no Visio")  
  
     **Mostrar clusters com gráfico de discriminação**  
     Essa opção cria o mesmo gráfico que o diagrama de cluster, mas lista as características do cluster atual que o distinguem mais fortemente de outros clusters.  
  
     Você pode alternar para outro tipo de gráfico depois que o assistente tiver criado o diagrama, clicando com o botão direito do mouse em um cluster e selecionando um novo tipo de gráfico. Por enquanto, escolha a opção **Mostrar clusters com o gráfico de características**.  
  
7.  Deixe a opção **número de linhas no gráfico**, como 5.  
  
     Essa opção não altera o número de clusters no modelo; Ele simplesmente limita o número de atributos que podem ser exibidos como recursos de cada cluster.  
  
     No entanto, a opção atua como um filtro nos dados do gráfico, portanto, você não pode aumentar o número de itens posteriormente.  
  
8.  Clique em **Avançado**.  
  
     A caixa de diálogo **Opções de cluster** é onde você personaliza a aparência visual das formas usadas no diagrama. Você pode alterar as cores usadas no gráfico e a forma usada para clusters.  
  
     O controle de **variável de sombreamento** não funciona no Office 2013.  
  
     ![clique em Avançado para escolher as cores da forma](media/dm13-visio-clusteroptions-advanced.gif "clique em Avançado para escolher as cores da forma")  
  
     **Dica:** Algumas cores podem ser alteradas mais tarde usando temas do Visio e controles de edição de formas. No entanto, os temas do Visio também substituirão algumas dessas seleções de cor. Portanto, é recomendável começar com as cores padrão e gradualmente aplicar alterações.  
  
9. Clique em **concluir** para criar o grafo.  
  
     O assistente recupera informações do modelo de mineração de dados, renderiza as formas e preenche cada cluster com atributos e valores.  
  
     ![uma rede de dependências](media/dm13-visiodepnet-defaultgraph.gif "uma rede de dependências")  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Explorar e modificar o diagrama completo  
 Depois que o diagrama estiver concluído, você poderá continuar a personalizar a aparência usando os controles do Visio, conforme mostrado no exemplo a seguir.  
  
 ![diagrama de cluster personalizando usando Visio](media/dm13-visio-clustercomplete1.gif "diagrama de cluster personalizando usando Visio")  
  
 Todas as formas básicas de cluster são geradas pelo assistente; use as seguintes ferramentas para atualizar e personalizar o diagrama:  
  
1.  Arraste o controle deslizante no controle de **Opções de cluster** para filtrar relações mais fracas e simplificar o diagrama.  
  
2.  Use a opção de **página Refazer layout** do Visio para fazer experiências com layouts de cluster diferentes.  
  
3.  Use a opção **conectores** na guia **design** para alterar o estilo do conector para manter as linhas do cruzamento em clusters.  
  
4.  Clique na faixa de **bits suplementos** e, em seguida, exiba uma das barras de ferramentas personalizadas usadas para trabalhar com diagramas de Data Mining:  
  
     **Layout**  
     Otimiza a organização dos clusters para caberem na página atual.  
  
     **Redimensionar Página**  
     Esse controle foi planejado para versões anteriores do HTML. Use os controles de dimensionamento de página do Visio.  
  
     **Descrição**  
     Se um cluster estiver selecionado, clique nessa opção para exibir detalhes sobre o cluster.  
  
     ![clique em Descrição para obter informações sobre o cluster](media/dm13-visio-cluster-description-control.gif "clique em Descrição para obter informações sobre o cluster")  
  
     **Intensidade da Borda**  
     Exibe pontuações de confiança nas linhas que conectam os clusters.  
  
     No entanto, se você aplicar qualquer formatação especial diferente do padrão gerado pelo assistente, inclusive os planos de fundo, esses números poderão não ser visíveis.  
  
     **Controle deslizante**  
     Filtra as linhas entre clusters. Mover o controle deslizante para cima remove tudo exceto as associações mais importantes.  
  
     **Sombreamento**  
     Esse controle não funciona no Office 2013.  
  
5.  Use o controle de **panorâmica e zoom** , na área do **painel de tarefas** da faixa de visão do Visio **View** , para se concentrar em um conjunto de clusters e movê-lo pelo diagrama.  
  
6.  Clique com o botão direito do mouse em qualquer cluster para ver as opções específicas para a forma do cluster:  
  
    -   Altere o estilo do gráfico.  
  
    -   Adicione um gráfico de características do cluster.  
  
    -   Adicione um gráfico de discriminação do cluster.  
  
## <a name="see-also"></a>Consulte Também  
 [Solução de problemas de diagramas de mineração de dados do Visio &#40;SQL Server suplementos de mineração de dados&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
