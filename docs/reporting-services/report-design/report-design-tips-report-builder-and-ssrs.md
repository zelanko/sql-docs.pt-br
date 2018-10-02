---
title: Dicas de design de relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: c1490ff0-5b8a-43c1-8d22-e459395db4f6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 51983605c640bddafae41463c27843282820041e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47764074"
---
# <a name="report-design-tips-report-builder-and-ssrs"></a>Dicas de design de relatórios (Construtor de Relatórios e SSRS)
  Use as dicas a seguir para ajudar na criação de seus relatórios paginados no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="DesigningReports"></a> Criando relatórios  
  
-   Um relatório criado corretamente transmite informações que resultam em ação. Identifique as perguntas que o relatório ajuda responder. Se lembre dessas perguntas como você cria o relatório.  
  
-   Para criar visualizações de dados efetivas, pense em como exibir informações que sejam fáceis de entender para o usuário do relatório. Escolha uma região de dados que seja uma boa correspondência dos dados que você deseja visualizar. Por exemplo, um gráfico transmite informações resumidas e agregadas efetivamente melhor do que uma tabela que inclui muitas páginas de informações detalhadas. É possível visualizar dados de um conjunto de dados em qualquer região de dados, que inclui gráficos, mapas, indicadores, minigráficos, databars e dados tabulares em vários layouts de grade com base em um tablix.  
  
-   Se você planejar entregar o relatório em um formato de exportação específico, teste o formato de exportação no início do design. Suporte a recursos varia com base no renderizador escolhido.  
  
-   Se você planejar entregar o relatório como uma assinatura, teste a assinatura no início do design. O suporte a parâmetros varia com base na assinatura criada.  
  
-   Ao criar layouts complexos, crie o layout em criar o layout em estágios. Você pode usar retângulos como contêineres para organizar os itens do relatório. Você pode criar regiões de dados diretamente na superfície de design para maximizar a área de trabalho e, em seguida, concluir cada uma e arrastá-la para o contêiner do retângulo. Usando retângulos como contêineres, é possível posicionar todo o conteúdo em uma etapa. Os retângulos também ajudam a controlar a forma como os itens de relatório são renderizados em cada página.  
  
-   Para reduzir a desordem em um relatório, considere o uso de visibilidade condicional para itens específicos do relatório e deixe que o usuário escolha se deseja mostrar os itens. É possível definir a visibilidade com base em um parâmetro ou em uma alternância de caixa de texto. É possível adicionar caixas de texto ocultas condicionalmente para mostrar resultados de expressão intermediários. Quando um relatório exibe dados inesperados, você pode mostrar esses resultados intermediários para ajudar a depurar expressões.  
  
-   Quando você trabalhar com itens aninhados em células de tablix ou retângulos, poderá definir cores do plano de fundo diferentes para o contêiner e para os itens contidos. Por padrão, a cor do plano de fundo é **Sem cor**. Itens com uma cor de plano de fundo específica se destacam entre itens com um conjunto de cores de plano de fundo definido como **Sem cor**. Esta técnica pode lhe ajudar a selecionar o item certo para definir propriedades de vídeo, como a visibilidade de borda em células de tablix.  
  
 Para obter mais informações sobre ideias a serem considerar na criação do seu relatório, consulte [Planejando um relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/report-design/planning-a-report-report-builder.md).  
  
##  <a name="NamingConventions"></a> Convenções de nomenclatura para relatórios, fontes de dados e conjuntos de dados  
  
-   Use convenções de nomenclatura para fontes de dados e conjuntos de dados que documentam a origem dos dados.  
  
    1.  **Fontes de dados.** Se você não quiser usar um servidor ou banco de dados real por questões de segurança, use um alias que indique ao usuário a origem dos dados.  
  
    2.  **Conjuntos de dados.** Use um nome que indique a fonte de dados na qual ele se baseia.  
  
    3.  **Regiões de dados.** Indique o tipo de região de dados e os dados exibidos por ela. Os nomes de região de dados são úteis nos seguintes cenários:  
  
        1.  **Região de dados como uma parte do relatório.** Quando os autores do relatório navegam na Galeria de Partes de Relatório, um nome descritivo ajuda a localizar as partes do relatório que eles estão procurando.  
  
        2.  **Região de dados como um feed de dados.** Com permissões apropriadas, um leitor de relatório pode criar um feed de dados de ATOM de uma região de dados.  
  
-   Use sublinhados em vez de espaços em nomes de relatório. Se você baixar um relatório do portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , os espaços serão substituídos por sublinhados. Se você usar o recurso de download para salvar relatórios localmente e, em seguida, incluí-los no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], o uso de sublinhados manterá as dependências do relatório para sub-relatórios e os links de detalhamento precisos.  
  
##  <a name="Data"></a> Trabalhando com dados  
  
-   Como uma primeira etapa, obtenha todos os dados com os quais você deseja trabalhar para aparecerem no painel de dados do relatório. Ao refinar as perguntas que o relatório deve responder, pense em como limitar ao máximo os dados nos conjuntos de dados do relatório.  
  
-   Em geral, inclua apenas os dados a serem exibidos em um relatório. Use variáveis de consulta em suas consultas de conjunto de dados para permitir que o usuário escolha quais dados deseja ver no relatório. Se estiver criando conjuntos de dados compartilhados, forneça filtros com base em parâmetros de relatório para fornecer a mesma funcionalidade.  
  
-   Se você for um autor de consultas experiente, tenha em mente que, para quantidades intermediárias de dados, talvez seja preferível agrupar os dados no relatório e não na consulta. Se você fizer todos os agrupamentos na consulta, o relatório tenderá a ser uma apresentação do conjunto de resultados da consulta. Por outro lado, para exibir valores agregados para quantidades grandes de dados em um gráfico ou matriz, não é preciso incluir dados detalhados.  
  
-   Dependendo dos seus requisitos, é possível exibir nomes e locais de fontes de dados do relatório, texto de comandos de consultas do conjunto de dados e valores dos parâmetros no relatório. A primeira pergunta de muitos novos usuários é sobre a origem dos dados. Para reduzir a desordem no relatório, você pode ocultar caixas de texto condicionalmente com este tipo de informações e permitir que os usuários escolham se desejam visualizá-las. Tente adicionar essas informações na última página do relatório. Defina a visibilidade da caixa de texto com base em um parâmetro que o usuário pode mudar.  
  
##  <a name="DesignSurface"></a> Interagindo com a superfície de design do relatório  
 A superfície de design do relatório não é o que aparece na tela. Quando você coloca itens do relatório na superfície de design, o local relativo afeta o modo como os itens aparecem na página do relatório renderizado. O espaço em branco é preservado.  
  
-   Use guias de alinhamento e botões de layout para alinhar e organizar itens na superfície de design do relatório. Por exemplo, você pode alinhar as partes superiores ou as bordas de itens selecionados, expandir um item para que corresponda ao tamanho de outro item ou ajustar o espaçamento entre itens.  
  
-   Use teclas de direção para ajustar a posição e o tamanho dos itens selecionados na superfície de design. Por exemplo, as seguintes combinações de teclas são muito úteis:  
  
    -   **Teclas de direção** Movem o item de relatório selecionado.  
  
    -   **CTRL+Teclas de direção** Deslocam o item de relatório selecionado.  
  
    -   **CTRL+SHIFT+Teclas de direção** Aumentam ou diminuem o tamanho do item de relatório selecionado.  
  
-   Para adicionar um item a um retângulo, use a ponta esquerda superior do mouse para apontar para o local inicial do item no contêiner do retângulo. Use atalhos do teclado para ajudar a posicionar objetos selecionados. O retângulo é automaticamente expandido para acomodar o tamanho dos itens contidos.  
  
-   Para adicionar vários itens a uma célula tablix, primeiro adicione um retângulo e, em seguida, adicione os itens.  
  
     Por padrão, cada célula tablix contém uma caixa de texto. Quando você adiciona um retângulo a uma célula, ele substitui a caixa de texto. Por exemplo, posicione indicadores aninhados em um retângulo em uma célula tablix para ajudar a controlar como o tamanho de um gráfico ou indicador é expandido quando você altera a altura da linha na qual a célula se encontra.  
  
-   Use o controle **Zoom** para ajustar a exibição da superfície de design. É possível trabalhar com a página inteira ou com seções menores da página.  
  
-   Para arrastar campos do painel de dados do relatório para o painel Agrupamento, evite arrastar o campo por outros itens do relatório na superfície de design, pois isso seleciona os outros itens e desmarca a região de dados Tablix. Arraste o campo para baixo no painel de dados do relatório e, em seguida, horizontalmente no painel Agrupamento.  
  
###  <a name="Selecting"></a> Selecionando itens  
 Para ajudar a selecionar o objeto que você deseja na superfície de design de relatório, use a tecla ESC, o menu de contexto do botão direito do mouse, o painel Propriedades e o painel Agrupamento.  
  
-   -   Pressione ESC para alternar entre a pilha de itens do relatório que ocupam o mesmo espaço na superfície de design.  
  
    -   Em alguns itens de relatório, tente usar o menu de contexto do botão direito do mouse para selecionar o item de relatório ou a parte do item de relatório desejada.  
  
    -   O painel Propriedades exibe as propriedades da seleção atual.  
  
    -   Para trabalhar com grupos de linhas e grupos de colunas em uma região de dados Tablix, selecione o grupo do painel Agrupamento.  
  
 No Designer de Relatórios do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], você pode selecionar da lista suspensa de objetos na barra de ferramentas do painel Propriedades ou da exibição hierárquica de itens de relatório na janela de Estrutura de Tópicos do Documento. Você pode selecionar itens neste painel e verificar o item selecionado na superfície de design. Para abrir a janela Estrutura de Tópicos do Documento, no menu **Exibir** , aponte para **Outras Janelas**e clique em **Estrutura de Tópicos do Documento**.  
  
##  <a name="ReportItems"></a> Trabalhando com tipos específicos de itens de relatório  
  
###  <a name="Parameters"></a> Trabalhando com parâmetros  
  
-   O objetivo principal dos parâmetros do relatório é filtrar dados na fonte de dados e recuperar apenas o que é necessário para o objetivo do relatório.  
  
-   Para parâmetros de relatório, encontre um equilíbrio entre habilitar interatividade e ajudar um usuário a obter os resultados que deseja. Por exemplo, você pode definir os valores padrão para um parâmetro com valores que você sabe que são populares.  
  
###  <a name="Text"></a> Trabalhando com texto  
  
-   Quando você cola várias linhas em uma caixa de texto, o texto é adicionado com uma sequência de texto. Cada sequência de texto pode ser formatada como uma unidade apenas. Para formatar cada linha independentemente, insira uma nova linha pressionando RETURN no texto conforme necessário. Em seguida, é possível aplicar formatação e estilos a cada linha independente de texto na caixa de texto.  
  
-   Você pode definir propriedades de formato e ações em uma caixa de texto ou no texto do espaço reservado na caixa de texto. Se houver apenas uma linha de texto, é mais eficiente definir as propriedades na caixa de texto do que no texto.  
  
###  <a name="Expressions"></a> Trabalhando com expressões  
  
-   Entenda os formatos de expressões simples e complexas. Você pode digitar um formato de expressão simples diretamente nas caixas de texto, propriedades no painel Propriedade ou em locais em caixas de diálogo que aceitam uma expressão. Para obter mais informações, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
-   Quando você cria uma expressão, ele ajuda a criar independentemente cada parte e verificar seu valor. Então, você pode combinar todas as partes em uma expressão final. Uma técnica útil é adicionar uma caixa de texto em uma célula de matriz, exibir cada parte da expressão e definir a visibilidade condicional na caixa de texto. Para controlar o estilo e a cor da borda quando a caixa de texto é ocultada, primeiro coloque a caixa de texto em um retângulo e, em seguida, defina o estilo e a cor da borda do retângulo para que correspondam aos da matriz.  
  
###  <a name="Indicators"></a> Trabalhando com indicadores  
  
-   Por padrão, um indicador mostra pelo menos três estados. Após adicionar um indicador a um relatório, você poderá configurá-lo adicionando ou removendo estados. Para facilitar a exibição por seus usuários, escolha um indicador que varie de cor e forma.  
  
##  <a name="Rendering"></a> Controlando a renderização de itens de relatório na página de relatório  
  
-   Na superfície de design do relatório, os itens do relatório crescem para acomodar o conteúdo do conjunto de dados, expressão, sub-relatório ou texto associado.  
  
    -   Quando você posiciona um item na página do relatório, a distância entre o item e todos os itens que começam à direita dele torna-se a distância mínima que deve ser mantida conforme um item de relatório cresce horizontalmente. De maneira semelhante, a distância entre um item e o item acima dele torna-se uma distância mínima que deve ser mantida conforme o item superior cresce verticalmente.  
  
    -   Um item em um relatório cresce para acomodar seus dados e empurra itens pares (itens dentro do mesmo contêiner pai) para fora do caminho usando as seguintes regras:  
  
    -   Cada item é movido para baixo para manter o espaço mínimo entre ele mesmo e os itens que terminam acima dele.  
  
    -   Cada item é movido para a direita para manter o espaço mínimo entre ele mesmo e os itens que terminam à sua esquerda. Para sistemas com layouts da direita para a esquerda, cada item é movido para a esquerda para manter o espaço mínimo entre ele mesmo e os itens que terminam à sua direita.  
  
    -   Os contêineres são expandidos para acomodar o crescimento de itens filho. Para um item selecionado, no painel Propriedades, a propriedade Pai identifica o contêiner do item. Também é possível usar o painel Estrutura de Tópicos do Documento para ver a hierarquia de confinamento dos itens do relatório.  
  
    -   A barra de ferramentas **Layout** fornece vários botões para ajudar alinhar bordas, centros e espaçamento para itens de relatório. Para habilitar a barra de ferramentas **Layout** , no menu **Exibir** , aponte para **Barras de Ferramentas**e clique em **Layout**.  
  
-   Se você pretende salvar o relatório como um arquivo .pdf, a largura do relatório deve ser definida explicitamente como um valor que forneça os resultados desejados no formato do arquivo de exportação. Por exemplo, defina a largura da página do relatório como exatamente 7,9375 polegadas e as margens esquerda e direita como 0,5 polegadas.  
  
-   Use **Layout de Impressão** e **Configurar Página** na barra de ferramentas do visualizador de relatórios para renderizar um relatório em uma exibição compatível com impressão. Para ajudar a remover páginas horizontais indesejáveis, proceda da seguinte maneira:  
  
    1.  Remova todo o espaço em branco adicional entre regiões de dados e as bordas do relatório.  
  
    2.  Reduza as margens da página na caixa de diálogo **Propriedades do Relatório** .  
  
    3.  Use **Retângulos** como contêineres para ajudar a controlar a forma como itens do relatório são renderizados.  
  
    4.  Em cabeçalhos de colunas, altere a propriedade da caixa de texto WritingMode para usar texto vertical.  
  
 Esse comportamento, as propriedades de largura e de altura dos itens do relatório, o tamanho do corpo do relatório, a definição da altura e da largura da página, as configurações de margem do relatório pai e o suporte específico à renderização são todos combinados para determinar quais itens do relatório se ajustam em uma página renderizada. Para obter mais informações, consulte [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Construtor de Relatórios no SQL Server 2016](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 [Tutoriais do Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)   
 [Tutoriais do Construtor de Relatórios](../../reporting-services/report-builder-tutorials.md)  
  
  
