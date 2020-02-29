---
title: 'Tutorial: Criar um relatório de gráficos rápido offline (Construtor de Relatórios) | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports, creating
- tutorials, getting started
- creating reports
ms.assetid: 6b1db67a-cf75-494c-b70c-09f1e6a8d414
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5cd666ec589737d83717e9b435a260bd2a0d0ef6
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176889"
---
# <a name="tutorial-create-a-quick-chart-report-offline-report-builder"></a>Tutorial: Criar um relatório de gráficos rápido offline (Construtor de Relatórios)
  Neste tutorial, você criará um gráfico de pizza usando um assistente e o modificará um pouco, apenas para ter uma ideia do que é possível. É possível executar este tutorial de duas formas. Ambos os métodos têm o mesmo resultado – um gráfico de pizza como o da ilustração a seguir:

 !["Meu Primeiro Gráfico de pizza" em modo Execução](../media/rs-my1stpierunview.gif "Meu primeiro gráfico de pizza no modo de exibição de execução")

## <a name="prerequisites"></a>Pré-requisitos
 Se você usa dados XML ou uma consulta [!INCLUDE[tsql](../../../includes/tsql-md.md)], precisa ter acesso ao Construtor de Relatórios da [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Você pode executar a versão autônoma ou a versão ClickOnce, disponível no Gerenciador de Relatórios ou em um site do SharePoint. Somente a primeira etapa, como abrir o Construtor de Relatórios, é diferente para versões do ClickOnce. Para obter mais informações, consulte [instalar, desinstalar e Construtor de relatórios suporte](../install-uninstall-and-report-builder-support.md).

##  <a name="TwoWays"></a> Duas formas de executar este tutorial

-   [Criar o gráfico de pizza com dados XML](#CreatePieChartXML)

-   [Criar o gráfico de pizza com uma consulta Transact-SQL que contém dados](#CreatePieQueryData)

### <a name="using-xml-data-for-this-tutorial"></a>Usando dados XML para este tutorial
 Você pode usar os dados XML que copiar deste tópico e colar no assistente. Não é necessário estar conectado a um servidor de relatório ou um servidor de relatório no modo integrado do SharePoint e nem ter acesso a uma instância do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].

 [Criar o gráfico de pizza com dados XML](#CreatePieChartXML)

### <a name="using-a-transact-sql-query-that-contains-data-for-this-tutorial"></a>Usando uma consulta Transact-SQL que contenha dados para este tutorial
 Você pode copiar uma consulta com dados incluídos neste tópico e colá-la no assistente. Você precisará do nome de uma instância do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] e de credenciais suficientes para ter acesso somente leitura a qualquer banco de dados. A consulta de conjuntos de dados nos tutoriais usa dados literais, mas deve ser processada por uma instância do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] para retornar os metadados necessários a um conjunto de dados de relatório.

 A vantagem de usar a consulta [!INCLUDE[tsql](../../../includes/tsql-md.md)] é que todos os outros tutoriais do Construtor de Relatórios usam o mesmo método; portanto, quando você executar os outros tutoriais, já saberá o que fazer.

 A consulta [!INCLUDE[tsql](../../../includes/tsql-md.md)] requer outros pré-requisitos. Para saber mais, veja [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../report-builder-tutorials.md).

 [Criar o gráfico de pizza com uma consulta Transact-SQL que contém dados](#CreatePieQueryData)

## <a name="also-in-this-article"></a>Também neste artigo
 [Depois de executar o assistente](#AfterWizard)

 [O que vem a seguir](#WhatsNext)

##  <a name="CreatePieChartXML"></a>Criando o gráfico de pizza com dados XML

#### <a name="to-create-the-pie-chart-with-xml-data"></a>Para criar o gráfico de pizza com dados XML

1.  Clique em **Iniciar**, aponte para **Programas**, para **Construtor de Relatórios do Microsoft SQL Server 2012**e clique em **Construtor de Relatórios**.

     A caixa de diálogo **Guia de Introdução** é exibida.

    > [!NOTE]
    >  Se a caixa de diálogo **introdução** não for exibida, no botão **Construtor de relatórios** , clique em **novo**.

2.  No painel esquerdo, verifique se **Relatório** está selecionado.

3.  No painel direito, clique em **Assistente de Gráfico**e em **Criar**.

4.  Na página **Escolha um conjunto de dados** , clique em **Criar um conjunto de dados**e em **Avançar**.

5.  Na página **Escolha uma conexão com uma fonte de dados** , clique em **Novo**.

     A caixa de diálogo **Propriedades da Fonte de Dados** é aberta.

6.  Você pode atribuir qualquer nome desejado a uma fonte de dados. Na caixa **Nome** , digite **MyPieChart**.

7.  Na caixa **Selecionar tipo de conexão** , clique em **XML.**

8.  Clique na guia **credenciais** , selecione **usar usuário atual do Windows. A delegação de Kerberos pode ser necessária**e, em seguida, clique em **OK**.

9. Na página **Escolha uma conexão com uma fonte de dados** , clique em **MyPieChart**e em **Avançar**.

10. Copie o texto a seguir e cole-o na caixa grande no centro da página **criar uma consulta** .

    ```
    <Query>
    <ElementPath>Root /S  {@Sales (Integer)} /C {@FullName} </ElementPath>
    <XmlData>
    <Root>
    <S Sales="150">
      <C FullName="Jae Pak" />
    </S>
    <S Sales="350">
      <C FullName="Jillian  Carson" />
    </S>
    <S Sales="250">
      <C FullName="Linda C Mitchell" />
    </S>
    <S Sales="500">
      <C FullName="Michael Blythe" />
    </S>
    <S Sales="450">
      <C FullName="Ranjit Varkey" />
    </S>
    </Root>
    </XmlData>
    </Query>
    ```

11. (Opcional) Clique no botão Executar ( **!** ) para ver os dados em que o gráfico se baseará.

12. Clique em **Próximo**.

13. Na página **Escolha um tipo de gráfico** , clique em **Pizza**e em **Avançar**.

14. Na página **Organizar campos de gráfico**, clique duas vezes no campo **Vendas** na caixa **Campos disponíveis**.

     Observe que ela se transforma automaticamente na caixa **Valores** porque é um valor numérico.

15. Arraste o campo **FullName** da caixa **Campos disponíveis** para a caixa **Categorias** (ou clique duas vezes nela para ir para a caixa **Categorias**) e, em seguida, clique em **Avançar**.

16. Na página **escolher um estilo** , o **oceano** é selecionado por padrão. Clique nos outros estilos para visualizar sua aparência.

17. Clique em **Concluir**.

     Você está olhando agora para seu novo relatório de gráfico de pizza na superfície de design. O que você vê é uma representação. A legenda diz Nome Completo 1, Nome Completo 2 etc., em vez dos nomes dos vendedores, e o tamanho das fatias da pizza não é exato. Isso é apenas para lhe dar uma ideia da aparência que o relatório terá.

18. Para ver seu gráfico de pizza real, clique em **Executar** na guia **Início** da Faixa de Opções.

 ![Ícone de seta usado com o link Voltar ao Início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [Voltar ao Início](#TwoWays)

##  <a name="CreatePieQueryData"></a>Criando o gráfico de pizza com [!INCLUDE[tsql](../../../includes/tsql-md.md)] uma consulta

#### <a name="to-create-the-pie-chart-with-a-tsql-query-that-contains-data"></a>Para criar o gráfico de pizza com uma consulta [!INCLUDE[tsql](../../../includes/tsql-md.md)] que contenha dados

1.  Clique em **Iniciar**, aponte para **Programas**, para **Construtor de Relatórios do Microsoft SQL Server 2012**e clique em **Construtor de Relatórios**.

2.  Na caixa de diálogo **novo relatório ou conjunto de novos** , verifique se o **relatório** está selecionado no painel esquerdo.

3.  No painel direito, clique em **Assistente de Gráfico**e em **Criar**.

4.  Na página **Escolha um conjunto de dados** , clique em **Criar um conjunto de dados**e em **Avançar**.

5.  Na página **Escolha uma conexão com uma fonte de dados** , selecione uma fonte de dados existente ou navegue até o servidor de relatório e selecione uma fonte de dados e clique em **Avançar**. Talvez seja necessário inserir um nome de usuário e uma senha.

    > [!NOTE]
    >  A fonte de dados escolhida não tem importância, contanto que você tenha permissões suficientes. Você não obterá dados da fonte de dados. Para saber mais, veja [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../report-builder-tutorials.md).

6.  Na página **Crie uma Consulta** , clique em **Editar como Texto**.

7.  Cole a seguinte consulta no painel de consulta:

    ```
    SELECT 150 AS Sales, 'Jae Pak' AS FullName 
    UNION SELECT 350 AS Sales, 'Jillian Carson' AS FullName 
    UNION SELECT 250 AS Sales, 'Linda C Mitchell' AS FullName 
    UNION SELECT 500 AS Sales, 'Michael Blythe' AS FullName 
    UNION SELECT 450 AS Sales, 'Ranjit Varkey' AS FullName 
    ```

8.  (Opcional) Clique no botão Executar ( **!** ) para ver os dados em que o gráfico se baseará.

9. Clique em **Próximo**.

10. Na página **Escolha um tipo de gráfico** , clique em **Pizza**e em **Avançar**.

11. Na página **Organizar campos de gráfico**, clique duas vezes no campo **Vendas** na caixa **Campos disponíveis**.

     Observe que ela se transforma automaticamente na caixa **Valores** , porque esse é um valor numérico.

12. Arraste o campo **FullName** da caixa **Campos disponíveis** para a caixa **Categorias** (ou clique duas vezes nela para ir para a caixa **Categorias**) e, em seguida, clique em **Avançar**.

13. Na página **Escolha um estilo** , a opção Oceano é selecionada por padrão. Clique nos outros estilos para visualizar sua aparência.

14. Clique em **Concluir**.

     Você está olhando agora para seu novo relatório de gráfico de pizza na superfície de design. O que você vê é uma representação. A legenda diz Nome Completo 1, Nome Completo 2 etc., em vez dos nomes dos vendedores, e o tamanho das fatias da pizza não é exato. Isso é apenas para lhe dar uma ideia da aparência que o relatório terá.

15. Para ver seu gráfico de pizza real, clique em **Executar** na guia **Início** da Faixa de Opções.

 ![Ícone de seta usado com o link Voltar ao Início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [Voltar ao Início](#TwoWays)

##  <a name="AfterWizard"></a> Depois que você executar o assistente
 Agora que você tem seu relatório de gráfico de pizza, pode brincar com ele. Na guia **Executar** da Faixa de Opções, clique em **Design**, para que você possa continuar modificando-o.

### <a name="make-the-chart-bigger"></a>Aumentar o gráfico
 Você optar por aumentar o tamanho do gráfico de pizza. Clique no gráfico, mas não em qualquer elemento do gráfico, para selecioná-lo e arraste o canto inferior direito para redimensioná-lo.

### <a name="add-a-report-title"></a>Adicionar um título a um relatório
 Selecione as palavras **Título do gráfico** na parte superior do gráfico e digite um título, como **Gráfico de Pizza de Vendas**.

### <a name="add-percentages"></a>Adicionar porcentagens

##### <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>Para exibir valores de porcentagem como rótulos em um gráfico de pizza

1.  Clique com o botão direito do mouse no gráfico de pizza e selecione **Mostrar rótulos de dados**. Os rótulos de dados devem aparecer dentro de cada fatia do gráfico de pizza.

2.  Clique com o botão direito do mouse nos rótulos e selecione **Propriedades do rótulo da série**. A caixa de diálogo **Propriedades do Rótulo de Série** é exibida.

3.  Digite `#PERCENT{P0}` para a opção **rotular dados** .

     O `{P0}` fornece o percentual sem casas decimais. Se você digitar apenas `#PERCENT`, seus números terão duas casas decimais. 
  `#PERCENT` é uma palavra-chave que executa um cálculo ou função para você; há muitos outras.

 Para saber mais sobre como personalizar legendas e rótulos de gráfico, veja [Exibir valores de porcentagem em um gráfico de pizza e &#40;Construtor de Relatórios e SSRS&#41;](../report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md) e [Alterar o texto de um item de legenda &#40;Construtor de Relatórios e SSRS&#41;](../report-design/chart-legend-change-item-text-report-builder.md).

 ![Ícone de seta usado com o link Voltar ao Início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [Voltar ao Início](#TwoWays)

##  <a name="WhatsNext"></a>O que vem a seguir?
 Agora que você criou seu primeiro relatório no Construtor de Relatórios, está pronto tentar os outros tutoriais e começar a criar relatórios com seus próprios dados. Para executar Construtor de Relatórios, você precisa de permissão para acessar suas fontes de dados, como bancos de dado, com uma *cadeia de conexão*que, na verdade, conecta você à fonte de dados. O administrador do sistema terá essas informações e poderá configurá-las.

 Para trabalhar nos outros tutoriais, você precisa do nome de uma instância do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] e de credenciais suficientes para ter acesso somente leitura a qualquer banco de dados. O administrador do sistema também pode definir isso para você.

 Finalmente, para salvar seus relatórios em um servidor de relatório ou site do SharePoint integrado a um servidor de relatório, você precisa da URL e de permissões. Você pode executar qualquer relatório que criar diretamente de seu computador, mas os relatórios têm mais funcionalidade quando executados no servidor de relatório ou site do SharePoint. Você precisa de permissões para executar seus relatórios ou de outras pessoas no servidor de relatório ou site do SharePoint em que eles foram publicados. Fale com o administrador do sistema para obter acesso.

 Talvez seja útil ler sobre alguns dos conceitos e termos antes de começar. Para obter mais informações, consulte [conceitos de criação de relatórios &#40;Construtor de relatórios e SSRS&#41;](../report-design/report-authoring-concepts-report-builder-and-ssrs.md). Além disso, dedique algum tempo ao planejamento, antes de criar seu primeiro relatório. Esse será um tempo bem gasto. Para obter mais informações, consulte [planejando um relatório &#40;Construtor de Relatórios&#41;](../report-design/planning-a-report-report-builder.md).

 ![Ícone de seta usado com o link Voltar ao Início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [Voltar ao Início](#TwoWays)

## <a name="see-also"></a>Consulte Também
 [Tutoriais &#40;Construtor de Relatórios&#41;](../report-builder-tutorials.md) [Construtor de Relatórios no SQL Server 2014](report-builder-in-sql-server-2016.md)


