---
title: Criando uma estrutura de modelo de mineração de mala direta (Tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a9c67f29-0c47-4a5a-862b-db0f5213c2c9
caps.latest.revision: 54
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c9c760ddd7f5445dfc00cc7c40ef877269940383
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37282232"
---
# <a name="creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial"></a>Criando uma estrutura de modelo de mineração de mala direta (Tutorial de mineração de dados básico)
  A primeira etapa para criar um cenário de correspondência destinada é usar o Assistente de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para criar uma nova estrutura de mineração e um modelo de mineração de árvore de decisão.  
  
 Nesta tarefa você configurar uma nova estrutura de mineração e adicionar um modelo de mineração inicial com base no [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo árvores de decisão. Para criar a estrutura, primeiro você selecionará tabelas e exibições e depois identificará as colunas que serão usadas no treinamento e as que serão usadas para teste.  
  
### <a name="to-create-a-mining-structure-for-the-targeted-mailing-scenario"></a>Para criar uma estrutura de mineração para o cenário de mala direta  
  
1.  No Gerenciador de soluções, clique com botão direito **estruturas de mineração** e selecione **nova estrutura de mineração** para iniciar o Assistente de mineração de dados.  
  
2.  Na página **Bem-vindo ao Assistente de Mineração de Dados** , clique em **Avançar**.  
  
3.  No **Selecionar método de definição** página, verifique **de warehouse existente de banco de dados ou dados relacional** está selecionado e, em seguida, clique em **próxima**.  
  
4.  Sobre o **criar a estrutura de mineração de dados** página, em **qual técnica de mineração de dados você deseja usar?**, selecione **Microsoft Decision Trees**.  
  
    > [!NOTE]  
    >  Se você receber um aviso de que não é possível encontrar nenhum algoritmo de mineração de dados, as propriedades do projeto talvez não sejam configuradas corretamente. Esse aviso ocorre quando o projeto tenta recuperar uma lista de algoritmos de mineração de dados do servidor do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e não consegue encontrá-lo. Por padrão, [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] usará **localhost** como o servidor. Se você estiver usando uma instância diferente ou uma instância nomeada, altere as propriedades do projeto. Para obter mais informações, consulte [criando um projeto do Analysis Services &#40;Tutorial básico de mineração de dados&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md).  
  
5.  Clique em **Avançar**.  
  
6.  No **Selecionar exibição da fonte de dados** página, o **modos de exibição de fonte de dados disponíveis** painel, selecione **mala**. Você pode clicar em **navegue** para exibir as tabelas na exibição da fonte de dados e, em seguida, clique em **fechar** para retornar ao assistente.  
  
7.  Clique em **Avançar**.  
  
8.  Sobre o **especificar tipos de tabela** , marque a caixa de seleção a **caso** coluna para vTargetMail para usá-lo como a tabela de casos e, em seguida, clique em **próxima**. Você usará a tabela ProspectiveBuyer posteriormente para testes; ignore-a por enquanto.  
  
9. Sobre o **especificar os dados de treinamento** página, você identificará pelo menos uma coluna previsível, uma coluna de chave, e uma coluna de entrada para seu modelo. Selecione a caixa de seleção a **previsível** coluna o **BikeBuyer** linha.  
  
    > [!NOTE]  
    >  Observe o aviso na parte inferior da janela. Você não poderá navegar até a próxima página até selecionar pelo menos um **entrada** e uma **previsível** coluna.  
  
10. Clique em **sugerir** para abrir o **sugerir colunas relacionadas** caixa de diálogo.  
  
     O **sugerir** botão fica habilitado sempre que pelo menos um atributo previsível foi selecionado. O **sugerir colunas relacionadas** caixa de diálogo lista as colunas que estão mais intrinsecamente relacionadas à coluna previsível e classifica os atributos pela correlação com o atributo previsível. As colunas com uma correlação significativa (confiança acima de 95%) são selecionadas automaticamente para serem incluídas no modelo.  
  
     Examine as sugestões e, em seguida, clique em **Cancelar** toignore as sugestões.  
  
    > [!NOTE]  
    >  Se você clicar **Okey**, listado todas as sugestões serão marcadas como colunas de entrada no assistente. Se você concordar com apenas algumas das sugestões, deverá alterar os valores manualmente.  
  
11. Verificar se a caixa de seleção de **chave** coluna é selecionada na **CustomerKey** linha.  
  
    > [!NOTE]  
    >  Se a tabela de origem na exibição de fonte de dados indicar uma chave, o Assistente de Mineração de Dados escolherá automaticamente essa coluna como uma chave para o modelo.  
  
12. Marque as caixas de seleção de **entrada** coluna nas linhas a seguir. Você pode marcar várias colunas ao realçar um intervalo de células e pressionar CTRL durante a marcação de uma caixa de seleção.  
  
    -   **Idade**  
  
    -   **CommuteDistance**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **Gênero**  
  
    -   **GeographyKey**  
  
    -   **HouseOwnerFlag**  
  
    -   **MaritalStatus**  
  
    -   **NumberCarsOwned**  
  
    -   **NumberChildrenAtHome**  
  
    -   **Região**  
  
    -   **TotalChildren**  
  
    -   **YearlyIncome**  
  
13. Na coluna mais à esquerda da página, marque as caixas de seleção nas linhas a seguir.  
  
    -   **Linha de endereço1**  
  
    -   **Linha de endereço2**  
  
    -   **DateFirstPurchase**  
  
    -   **EmailAddress**  
  
    -   **FirstName**  
  
    -   **LastName**  
  
     Verifique se essas linhas só possuem marcações na coluna à esquerda. Essas colunas serão adicionadas à sua estrutura mas não serão incluídas no modelo. No entanto, depois que o modelo for criado, elas estarão disponíveis para detalhamento e teste. Para obter mais informações sobre detalhamento, consulte [consultas de detalhamento &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
14. Clique em **Avançar**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Especificando o tipo de dados e o tipo de conteúdo &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Especificar tipos de tabela &#40;Assistente de mineração de dados&#41;](../../2014/analysis-services/specify-table-types-data-mining-wizard.md)   
 [Designer de mineração de dados](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Algoritmo Árvores de Decisão da Microsoft](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md)  
  
  
