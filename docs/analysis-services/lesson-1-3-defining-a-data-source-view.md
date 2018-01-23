---
title: "Definindo dados de um exibição da fonte | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: af00938a-5a06-4fae-b2fc-f3fb0ca3cea5
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: b4cc8514f957d0b9337d8466b5cd130c852b334c
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2018
---
# <a name="lesson-1-3---defining-a-data-source-view"></a>Lição 1-3-definir uma exibição da fonte de dados
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

Depois de definir as fontes de dados que serão usadas em um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], você normalmente define uma exibição da fonte de dados para o projeto. Uma exibição da fonte de dados é uma exibição unificada exclusiva dos metadados das tabelas e exibições especificadas que a fonte de dados define no projeto. Armazenar os metadados na exibição da fonte de dados permite que você trabalhe com os metadados durante o desenvolvimento sem ter uma conexão aberta com qualquer fonte de dados subjacente. Para obter mais informações, consulte [Exibições de fontes de dados em modelos multidimensionais](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
Na tarefa a seguir, você define uma exibição da fonte de dados que inclui cinco tabelas da fonte de dados **AdventureWorksDW2012** .  
  
### <a name="to-define-a-new-data-source-view"></a>Para definir uma nova exibição da fonte de dados  
  
1.  No Gerenciador de Soluções (à direita da janela do Microsoft Visual Studio), clique com o botão direito do mouse em **Exibições da Fonte de Dados**e clique em **Nova Exibição da Fonte de Dados**.  
  
2.  Na página **Bem-vindo ao Assistente de Exibição da Fonte de Dados** , clique em **Avançar**. A página **Selecionar uma Fonte de Dados** é exibida.  
  
3.  Em **Fontes de dados relacionais**, a fonte de dados **Adventure Works DW 2012** está selecionada. Clique em **Avançar**.  
  
    > [!NOTE]  
    > Para criar uma exibição de fonte de dados com base em várias fontes de dados, primeiro defina uma exibição da fonte de dados com base em uma única fonte de dados. Essa fonte de dados é, então, chamada a fonte de dados primária. Depois, você poderá adicionar tabelas e exibições de uma fonte de dados secundária. Ao projetar dimensões que contenham atributos com base em tabelas relacionadas em várias fontes de dados, talvez seja necessário definir um [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fonte de dados como fonte de dados primário para usar os recursos do mecanismo de consulta distribuída.  
  
4.  Na página **Selecionar Tabelas e Exibições** , selecione tabelas e exibições na lista de objetos disponíveis da fonte de dados selecionada. Você pode filtrar essa lista para facilitar a seleção de tabelas e exibições.  
  
    > [!NOTE]  
    > Clique no botão maximizar no canto direito superior para que a janela ocupe toda a tela. Isso facilitará a visualização da lista completa de objetos disponíveis.  
  
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
[Modificando nomes de tabela padrão](../analysis-services/lesson-1-4-modifying-default-table-names.md)  
  
## <a name="see-also"></a>Consulte também  
[Exibições da fonte de dados em modelos multidimensionais](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
  
