---
title: Instruções passo a passo do diagrama (suplementos de mineração de dados) do cluster | Microsoft Docs
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
- Visio shapes, cluster
- diagram, cluster
- shapes, data mining
- shapes, cluster
- data mining layout toolbar
ms.assetid: 761bef6a-37d4-4b19-944e-f2aadc75a242
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a8ab399dcc59873cc507e260eec82582a69f8ba6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120702"
---
# <a name="cluster-diagram-walkthrough-data-mining-add-ins"></a>Passo a passo do diagrama de Cluster (Suplementos de Mineração de Dados)
  Depois de criar um modelo de clustering, você pode importá-lo no Visio usando a **Cluster** forma e, em seguida, continuar a personalizar e aprimorar o layout. O **formas de mineração de dados para Visio** incluem os seguintes controles personalizados para trabalhar com diagramas de mineração de dados:  
  
-   Controles de renderização para o diagrama de cluster  
  
     Essas opções fazem parte do **Assistente de Cluster** que é iniciado quando você solta uma forma no espaço de trabalho do Visio.  
  
-   **Layout de mineração de dados** barra de ferramentas  
  
     Essas opções são adicionadas ao espaço de trabalho do Visio para ajudá-lo a interagir com a forma de mineração de dados. As opções são diferentes dependendo do tipo de modelo de mineração de dados que você está usando.  
  
## <a name="build-a-cluster-diagram"></a>Criar um diagrama de cluster  
 Este passo a passo demonstra como criar e personalizar um diagrama de clustering no Visio.  
  
 Para acompanhar, você já deverá ter um modelo de clustering disponível. Se você não tiver um modelo, use o [Assistente de Cluster &#40;suplementos de mineração de dados para Excel&#41; ](cluster-wizard-data-mining-add-ins-for-excel.md) assistente e criar um modelo usando o conjunto de dados de treinamento na pasta de trabalho de exemplo, usando todos os padrões.  
  
#### <a name="use-the-cluster-visio-shape-wizard"></a>Use o assistente para Criar Formas Cluster do Visio  
  
1.  Se você não vir **formas de mineração de dados do Microsoft** no **formas** lista, clique em **mais formas**, selecione **Abrir estêncil**e abra o modelo do local de instalação padrão.  
  
     \<unidade >: \Program files\Microsoft SQL Server 2012 DM Add-Ins  
  
2.  Arraste o **Cluster** forma até a página.  
  
3.  Na página de boas-vinda do **Assistente do Cluster do Visio forma**, clique em **próximo**.  
  
4.  No **selecionar uma fonte de dados** página do **Assistente de Cluster**, escolha uma conexão para um [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] servidor que contém os modelos de mineração de dados que você deseja visualizar.  
  
5.  Selecione um modelo de mineração apropriado e, em seguida, clique em **próximo**.  
  
     Para certificar-se de que você escolha um modelo de clustering, examine a descrição no **propriedades** painel.  
  
6.  Se a conexão for bem-sucedida, na página, **opções para o diagrama de cluster**, decidir qual tipo de diagrama de cluster para incluir em sua apresentação do Visio:  
  
     **Mostrar formas de cluster somente**  
     Essa opção cria um diagrama de cluster simples, com cada cluster representado por um retângulo ou outra forma que você escolher  
  
     **Mostrar clusters com gráfico de características**  
     Essa opção cria o mesmo gráfico que o anterior, mas dentro das formas estão os histogramas que descrevem as características do cluster.  
  
     ![Exemplo de gráfico de características de cluster no Visio](media/dm13-visio-cluster-samplecharshape.gif "exemplo de gráfico de características de cluster no Visio")  
  
     **Mostrar clusters com gráfico de discriminação**  
     Essa opção cria o mesmo gráfico que o diagrama de cluster, mas lista as características do cluster atual que o distinguem mais fortemente de outros clusters.  
  
     Você pode alternar para outro tipo de gráfico depois que o assistente tiver criado o diagrama, clicando com o botão direito do mouse em um cluster e selecionando um novo tipo de gráfico. Por enquanto, escolha a opção **Mostrar clusters com gráfico de características**.  
  
7.  Deixe a opção **número de linhas no gráfico**, como 5.  
  
     Essa opção não altera o número de clusters no modelo; ela apenas limita o número de atributos que podem ser exibidos como recursos de cada cluster.  
  
     No entanto, a opção age como um filtro nos dados do gráfico e, portanto, você não poderá aumentar o número de itens posteriormente.  
  
8.  Clique em **Avançado**.  
  
     O **opções de Cluster** caixa de diálogo é onde você personaliza a aparência visual das formas usadas no diagrama. Você pode alterar as cores usadas no gráfico e a forma usada para clusters.  
  
     O **variável de sombreamento** controle não funciona no Office 2013.  
  
     ![Clique em Avançado para escolher as cores da forma](media/dm13-visio-clusteroptions-advanced.gif "clique em Avançado para escolher as cores da forma")  
  
     **Dica:** algumas cores podem ser alterados posteriormente usando temas do Visio e controles de edição de formas. No entanto, os temas do Visio também substituirão algumas dessas seleções de cor. Portanto, é recomendável começar com as cores padrão e gradualmente aplicar alterações.  
  
9. Clique em **concluir** para criar o gráfico.  
  
     O assistente recupera informações do modelo de mineração de dados, renderiza as formas e preenche cada cluster com atributos e valores.  
  
     ![uma rede de dependência](media/dm13-visiodepnet-defaultgraph.gif "uma rede de dependência")  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Explorar e modificar o diagrama completo  
 Depois que o diagrama estiver concluído, você poderá continuar a personalizar a aparência usando os controles do Visio, conforme mostrado no exemplo a seguir.  
  
 ![diagrama de cluster personalizado usando Visio](media/dm13-visio-clustercomplete1.gif "diagrama de cluster personalizado usando Visio")  
  
 Todas as formas básicas de cluster são geradas pelo assistente; use as seguintes ferramentas para atualizar e personalizar o diagrama:  
  
1.  Arraste o controle deslizante **opções de Cluster** controle, para filtrar as relações mais fracas e simplificar o diagrama.  
  
2.  Use o Visio **Refazer Layout da página** opção para fazer experiências com diferentes layouts de cluster.  
  
3.  Use o **conectores** opção o **Design** guia para alterar o estilo de conector para impedir que linhas cruzem os clusters.  
  
4.  Clique o **Add-Ins** de faixa de opções e, em seguida, exibir uma das barras de ferramentas personalizadas usadas para trabalhar com diagramas de mineração de dados:  
  
     **Layout**  
     Otimiza a organização dos clusters para caberem na página atual.  
  
     **Redimensionar página**  
     Esse controle foi planejado para versões anteriores do HTML. Use os controles de dimensionamento de página do Visio.  
  
     **Descrição**  
     Se um cluster estiver selecionado, clique nessa opção para exibir detalhes sobre o cluster.  
  
     ![Clique em descrição para obter detalhes sobre o cluster](media/dm13-visio-cluster-description-control.gif "clique em descrição para obter detalhes sobre o cluster")  
  
     **Intensidade da borda**  
     Exibe pontuações de confiança nas linhas que conectam os clusters.  
  
     No entanto, se você aplicar qualquer formatação especial diferente do padrão gerado pelo assistente, inclusive os planos de fundo, esses números poderão não ser visíveis.  
  
     **Controle deslizante**  
     Filtra as linhas entre clusters. Mover o controle deslizante para cima remove tudo exceto as associações mais importantes.  
  
     **Sombreamento**  
     Esse controle não funciona no Office 2013.  
  
5.  Use o **Panorâmica e Zoom** controlar, o **painel de tarefas** área do Visio **exibição** faixa de opções, para focalizar em um conjunto de clusters e navegar em torno do diagrama.  
  
6.  Clique com o botão direito do mouse em qualquer cluster para ver as opções específicas para a forma do cluster:  
  
    -   Altere o estilo do gráfico.  
  
    -   Adicione um gráfico de características do cluster.  
  
    -   Adicione um gráfico de discriminação do cluster.  
  
## <a name="see-also"></a>Consulte também  
 [Solucionando problemas de diagramas de mineração de dados do Visio &#40;suplementos de mineração de dados do SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  