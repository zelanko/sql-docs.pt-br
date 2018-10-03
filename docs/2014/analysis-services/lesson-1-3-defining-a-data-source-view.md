---
title: Definindo dados de um exibição da fonte | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: af00938a-5a06-4fae-b2fc-f3fb0ca3cea5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca6e9661c65098bed1175c7108b18a482b14a542
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48058816"
---
# <a name="defining-a-data-source-view"></a>Definindo uma exibição da fonte de dados
  Depois de definir as fontes de dados que serão usadas em um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], você normalmente define uma exibição da fonte de dados para o projeto. Uma exibição da fonte de dados é uma exibição unificada exclusiva dos metadados das tabelas e exibições especificadas que a fonte de dados define no projeto. Armazenar os metadados na exibição da fonte de dados permite que você trabalhe com os metadados durante o desenvolvimento sem ter uma conexão aberta com qualquer fonte de dados subjacente. Para obter mais informações, consulte [Exibições de fontes de dados em modelos multidimensionais](multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
 Na tarefa a seguir, você define uma exibição da fonte de dados que inclui cinco tabelas da fonte de dados **AdventureWorksDW2012** .  
  
### <a name="to-define-a-new-data-source-view"></a>Para definir uma nova exibição da fonte de dados  
  
1.  No Gerenciador de Soluções (à direita da janela do Microsoft Visual Studio), clique com o botão direito do mouse em **Exibições da Fonte de Dados**e clique em **Nova Exibição da Fonte de Dados**.  
  
2.  Na página **Bem-vindo ao Assistente de Exibição da Fonte de Dados** , clique em **Avançar**. A página **Selecionar uma Fonte de Dados** é exibida.  
  
3.  Em **Fontes de dados relacionais**, a fonte de dados **Adventure Works DW 2012** está selecionada. Clique em **Avançar**.  
  
    > [!NOTE]  
    >  Para criar uma exibição de fonte de dados com base em várias fontes de dados, primeiro defina uma exibição da fonte de dados com base em uma única fonte de dados. Essa fonte de dados é, então, chamada a fonte de dados primária. Depois, você poderá adicionar tabelas e exibições de uma fonte de dados secundária. Ao projetar dimensões que contêm atributos baseados em tabelas relacionadas em várias fontes de dados, talvez seja necessário definir uma fonte de dados do [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como a fonte de dados primária para usar suas funcionalidades de mecanismo de consulta distribuída.  
  
4.  Na página **Selecionar Tabelas e Exibições** , selecione tabelas e exibições na lista de objetos disponíveis da fonte de dados selecionada. Você pode filtrar essa lista para facilitar a seleção de tabelas e exibições.  
  
    > [!NOTE]  
    >  Clique no botão maximizar no canto direito superior para que a janela ocupe toda a tela. Isso facilitará a visualização da lista completa de objetos disponíveis.  
  
     Na lista **Objetos disponíveis** , selecione os objetos a seguir. Você pode selecionar várias tabelas clicando em cada uma enquanto mantém pressionada a tecla CTRL.  
  
    -   **DimCustomer (dbo)**  
  
    -   **DimDate (dbo)**  
  
    -   **DimGeography (dbo)**  
  
    -   **DimProduct (dbo)**  
  
    -   **FactInternetSales (dbo)**  
  
5.  Clique em **>** para adicionar as tabelas selecionadas à lista **Objetos incluídos** .  
  
6.  Clique em **Avançar.**  
  
7.  No campo Nome, garanta que **Adventure Works DW 2012** é exibido e clique em **Concluir**.  
  
     A exibição da fonte de dados **Adventure Works DW 2012** é exibida na pasta **Exibições da Fonte de Dados** do Gerenciador de Soluções. O conteúdo da exibição da fonte de dados também é exibido no Designer de Exibição da Fonte de Dados no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Esse designer contém os seguintes elementos:  
  
    -   Um painel **Diagrama** no qual as tabelas e suas relações são representadas de forma gráfica.  
  
    -   Um painel **Tabelas** no qual as tabelas e seus elementos de esquema são exibidos em um modo de exibição de árvore.  
  
    -   Um painel **Organizador de Diagramas** no qual você pode criar subdiagramas para exibir subconjuntos da exibição da fonte de dados.  
  
    -   Há uma barra de ferramentas específica para o Designer de Exibição da Fonte de Dados.  
  
8.  Para maximizar o ambiente de desenvolvimento do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , clique no botão **Maximizar** .  
  
9. Para exibir as tabelas no painel **Diagrama** a 50%, clique no ícone **Zoom** na barra de ferramentas do Designer de Exibição da Fonte de Dados. Isso ocultará os detalhes da coluna de cada tabela.  
  
10. Para ocultar o Gerenciador de Soluções, clique no botão **Ocultar Automaticamente** , que é o ícone de pino na barra de título. Para exibir o Gerenciador de Soluções novamente, aponte para a guia do Gerenciador de Soluções à direito do ambiente de desenvolvimento. Para exibir o Gerenciador de Soluções novamente, clique no botão **Ocultar Automaticamente** mais uma vez.  
  
11. Se as janelas não estiverem ocultas por padrão, clique em **Ocultar Automaticamente** na barra de título das janelas Propriedades e Gerenciador de Soluções.  
  
     Agora, você pode exibir todas as tabelas e suas relações no painel **Diagrama** . Observe que há três relações entre as tabelas tabelas FactInternetSales e a tabela DimDate. Cada venda tem três datas associadas: uma data de ordem, uma data de vencimento e uma data de remessa. Para exibir os detalhes de qualquer relação, clique duas vezes na seta da relação no painel **Diagrama** .  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Modificando nomes de tabela padrão](lesson-1-4-modifying-default-table-names.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de fontes de dados em modelos multidimensionais](multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
