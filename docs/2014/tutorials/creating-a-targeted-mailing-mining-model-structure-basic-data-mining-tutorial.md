---
title: Criando uma estrutura de modelo de mineração de endereçamento direcionada (tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a9c67f29-0c47-4a5a-862b-db0f5213c2c9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2bd2e9d0decc730a59b63ee600bec2d080cc85fb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62856160"
---
# <a name="creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial"></a>Criando uma estrutura de modelo de mineração de mala direta (Tutorial de mineração de dados básico)
  A primeira etapa para criar um cenário de correspondência destinada é usar o Assistente de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para criar uma nova estrutura de mineração e um modelo de mineração de árvore de decisão.  
  
 Nesta tarefa, você irá configurar uma nova estrutura de mineração e adicionar um modelo de mineração inicial com base no [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo árvores de decisão. Para criar a estrutura, primeiro você selecionará tabelas e exibições e depois identificará as colunas que serão usadas no treinamento e as que serão usadas para teste.  
  
### <a name="to-create-a-mining-structure-for-the-targeted-mailing-scenario"></a>Para criar uma estrutura de mineração para o cenário de mala direta  
  
1.  Em Gerenciador de Soluções, clique com o botão direito do mouse em **estruturas de mineração** e selecione **nova estrutura de mineração** para iniciar o assistente de mineração de dados.  
  
2.  Na página **Bem-vindo ao Assistente de Mineração de Dados** , clique em **Avançar**.  
  
3.  Na página **selecionar o método de definição** , verifique se a **partir de banco de dados relacional existente ou data warehouse** está selecionada e clique em **Avançar**.  
  
4.  Na página **criar a estrutura de mineração de dados** , sob a **qual data mining técnica você deseja usar?**, selecione **árvores de decisão da Microsoft**.  
  
    > [!NOTE]  
    >  Se você receber um aviso de que não é possível encontrar nenhum algoritmo de mineração de dados, as propriedades do projeto talvez não sejam configuradas corretamente. Esse aviso ocorre quando o projeto tenta recuperar uma lista de algoritmos de mineração de dados do servidor do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e não consegue encontrá-lo. Por padrão, [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] o usará **localhost** como o servidor. Se você estiver usando uma instância diferente ou uma instância nomeada, altere as propriedades do projeto. Para obter mais informações, consulte [criando um projeto de Analysis Services &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md).  
  
5.  Clique em **Avançar**.  
  
6.  Na página **selecionar exibição da fonte de dados** , no painel **exibições da fonte de dados disponíveis** , selecione **endereçamento direcionado**. Você pode clicar em **procurar** para exibir as tabelas na exibição da fonte de dados e, em seguida, clicar em **fechar** para retornar ao assistente.  
  
7.  Clique em **Avançar**.  
  
8.  Na página **especificar tipos de tabela** , marque a caixa de seleção na coluna **caso** de vTargetMail para usá-la como a tabela de casos e clique em **Avançar**. Você usará a tabela ProspectiveBuyer posteriormente para testes; ignore-a por enquanto.  
  
9. Na página **especificar os dados de treinamento** , você identificará pelo menos uma coluna previsível, uma coluna de chave e uma coluna de entrada para o modelo. Marque a caixa de seleção na coluna **previsível** na linha **BikeBuyer** .  
  
    > [!NOTE]  
    >  Observe o aviso na parte inferior da janela. Você não poderá navegar para a próxima página até selecionar pelo menos uma **entrada** e uma coluna **previsível** .  
  
10. Clique em **sugerir** para abrir a caixa de diálogo **sugerir colunas relacionadas** .  
  
     O botão **sugerir** é habilitado sempre que pelo menos um atributo previsível tiver sido selecionado. A caixa de diálogo **sugerir colunas relacionadas** lista as colunas mais próximas à coluna previsível e ordena os atributos por sua correlação com o atributo previsível. As colunas com uma correlação significativa (confiança acima de 95%) são selecionadas automaticamente para serem incluídas no modelo.  
  
     Revise as sugestões e, em seguida, clique em **Cancelar** ignorar as sugestões.  
  
    > [!NOTE]  
    >  Se você clicar em **OK**, todas as sugestões listadas serão marcadas como colunas de entrada no assistente. Se você concordar com apenas algumas das sugestões, deverá alterar os valores manualmente.  
  
11. Verifique se a caixa de seleção na coluna **chave** está selecionada na linha **CustomerKey** .  
  
    > [!NOTE]  
    >  Se a tabela de origem na exibição de fonte de dados indicar uma chave, o Assistente de Mineração de Dados escolherá automaticamente essa coluna como uma chave para o modelo.  
  
12. Marque as caixas de seleção na coluna **entrada** nas linhas a seguir. Você pode marcar várias colunas ao realçar um intervalo de células e pressionar CTRL durante a marcação de uma caixa de seleção.  
  
    -   **Idade**  
  
    -   **CommuteDistance**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **Sexo**  
  
    -   **GeographyKey**  
  
    -   **HouseOwnerFlag**  
  
    -   **MaritalStatus**  
  
    -   **NumberCarsOwned**  
  
    -   **NumberChildrenAtHome**  
  
    -   **Região**  
  
    -   **TotalChildren**  
  
    -   **YearlyIncome**  
  
13. Na coluna mais à esquerda da página, marque as caixas de seleção nas linhas a seguir.  
  
    -   **AddressLine1**  
  
    -   **AddressLine2**  
  
    -   **DateFirstPurchase**  
  
    -   **EmailAddress**  
  
    -   **FirstName**  
  
    -   **LastName**  
  
     Verifique se essas linhas só possuem marcações na coluna à esquerda. Essas colunas serão adicionadas à sua estrutura mas não serão incluídas no modelo. No entanto, depois que o modelo for criado, elas estarão disponíveis para detalhamento e teste. Para obter mais informações sobre detalhamento, consulte [consultas de detalhamento &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
14. Clique em **Avançar**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Especificando o tipo de dados e o tipo de conteúdo &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Especificar tipos de tabela &#40;assistente de mineração de dados&#41;](../../2014/analysis-services/specify-table-types-data-mining-wizard.md)   
 [Designer de mineração de dados](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Algoritmo Árvores de Decisão da Microsoft](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md)  
  
  
