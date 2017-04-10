---
title: "Escolher e mapear dados de testes modelo | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "colunas [mineração de dados], gráficos de precisão de mineração"
  - "Gráfico de Precisão de Mineração [Analysis Services], mapeamentos de colunas"
  - "mapeamento de coluna de entrada [Analysis Services]"
  - "mapeando colunas de entrada [Analysis Services]"
ms.assetid: be0d9f20-40c3-4dac-81da-281cfe724126
caps.latest.revision: 44
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 44
---
# Escolher e mapear dados de testes modelo
  Para criar um gráfico de precisão no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], escolha os dados que serão usados para testar o modelo e mapeie os dados para o modelo.  
  
 Por padrão, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará os dados de teste do modelo de mineração, desde que você tenha criado um conjunto de dados de controle quando criou a estrutura de mineração. A criação de um conjunto de testes de controle é a maneira mais fácil de testar modelos baseados na mesma estrutura de mineração porque os nomes de colunas e os tipos de dados sempre coincidirão com o modelo. Além disso, você tem uma garantia razoável de que a distribuição dos dados é semelhante. Somado a isso, o designer criará automaticamente as relações entre as colunas de entrada e saída.  
  
 Outra alternativa é especificar uma fonte de dados externa. Para dados externos, há alguns requisitos adicionais:  
  
-   O conjunto de dados externos deve ser definido como uma exibição da fonte de dados em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   O conjunto de dados externos deve conter pelo menos uma coluna que possa ser mapeada para a coluna previsível no modelo de mineração. Você pode optar por ignorar algumas colunas.  
  
-   Você não pode adicionar novas colunas nem mapear colunas em uma exibição de fonte de dados diferente. A exibição da fonte de dados selecionada deve conter todas as colunas que você precisa para a consulta de previsão.  
  
-   Se os nomes da coluna externa coincidirem exatamente com os nomes no modelo, o designer irá mapeá-los para você. Se os mapeamentos estiverem errados, você poderá alterá-los, ou excluir e criar novos mapeamentos para colunas existentes.  
  
-   Se você usar uma fonte de dados externa, poderá aplicar filtros para restringir os dados de testes a um subconjunto relevante de casos.  
  
-   Mesmo ao usar o conjunto de testes de controle, lembre-se de que filtros podem causar diferenças entre os dados de testes associados com uma estrutura de mineração e os casos de testes do modelo de mineração.  
  
 Este tópico descreve como escolher e mapear dados de testes:  
  
 [Selecione tabelas de entrada para testar a precisão de um modelo de mineração](#bkmk_SelectInputs)  
  
 [Mapeie colunas modelo para as colunas nos dados de testes](#bkmk_MapColumns)  
  
 [Altere a forma como colunas nos dados de testes são mapeadas para o modelo](#bkmk_ChangeMappings)  
  
##  <a name="bkmk_SelectInputs"></a> Para selecionar tabelas de entrada para testar a exatidão de um modelo de mineração  
  
1.  No Designer de Mineração de Dados do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique duas vezes na estrutura de mineração que contém os modelos com os quais deseja fazer o gráfico.  
  
2.  Selecione a guia **Gráfico de Precisão de Mineração**.  
  
3.  Na **Guia Seleção de Entrada** da exibição **Gráfico de Precisão de Mineração**, selecione uma das seguintes opções:  
  
     **Usar casos de teste do modelo de mineração**  
  
     **Usar casos de teste da estrutura de mineração**  
  
     **Especificar um conjunto de dados diferente**  
  
4.  Se você selecionou **Especificar um conjunto de dados diferente**, opcionalmente, clique em **Abrir Editor de Filtro** para criar condições de filtro no conjunto de dados de entrada. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  Clique na guia **Gráfico de Comparação de Precisão** ou na guia **Matriz de Classificação** para criar automaticamente o gráfico usando os dados de teste recém-especificados.  
  
##  <a name="bkmk_MapColumns"></a> Para mapear colunas modelo para as colunas nos dados de testes  
  
1.  Clique duas vezes na estrutura de mineração que contém os modelos que você deseja incluir no gráfico, para abrir a estrutura e seus modelos no Designer de Mineração de Dados.  
  
2.  Selecione a guia **Gráfico de Precisão da Mineração** e, em seguida, selecione a guia **Seleção de Entrada** .  
  
3.  Na guia **Seleção de Entrada**, em **Selecionar conjunto de dados a ser usado para Gráfico de Precisão**, selecione **Especificar um conjunto de dados diferente**.  
  
4.  Clique no botão Procurar **(...)** para abrir uma caixa de diálogo e criar a definição do conjunto de dados externo.  
  
5.  Na caixa de diálogo **Selecionar Estrutura de Mineração**, selecione a estrutura de mineração que contém os modelos com os quais deseja trabalhar e, em seguida, clique em **OK**.  
  
6.  Na tabela **Selecionar Tabela(s) de Entrada** da guia **Gráfico de Precisão de Mineração**, clique em **Selecionar Tabela de Casos** para abrir a caixa de diálogo **Selecionar Tabela**.  
  
7.  Na caixa de diálogo **Selecionar Tabela** , selecione uma fonte de dados na lista **Fonte de Dados** . Escolha uma tabela que contém os dados que deseja usar nas consultas de previsão para determinar a precisão dos modelos.  
  
8.  Na caixa **Nome de Tabela/Exibição**, selecione a tabela que contém os dados que deseja usar para testar os modelos.  
  
9. Edite os mapeamentos, se necessário. As colunas da estrutura de mineração são mapeadas automaticamente para colunas com o mesmo nome na tabela de entrada. Para criar mapeamentos manualmente, clique em uma coluna na tabela **Selecionar Tabela(s) de Entrada** e arraste-a na coluna correspondente na tabela **Estrutura de Mineração**. Para excluir um mapeamento, clique na linha que vincula a coluna na tabela **Estrutura de Mineração** à coluna mapeada na tabela **Selecionar Tabela(s) de Entrada** e pressione DELETE.  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="bkmk_ChangeMappings"></a> Para modificar a forma como dados de entrada são mapeados para o modelo  
  
1.  No Designer do Data Mining, clique duas vezes na estrutura que contém os modelos com os quais deseja criar o gráfico.  
  
2.  Selecione a guia **Gráfico de Precisão de Mineração**.  
  
3.  Clique na guia **Seleção de Entrada**.  
  
4.  Em **Selecionar conjunto de dados a ser usado para o Gráfico de Precisão**, selecione a opção **Especificar um conjunto de dados diferente**.  
  
5.  Clique no botão Procurar **(...)** para abrir uma caixa de diálogo e criar a definição da fonte de dados externa.  
  
6.  Na caixa de diálogo **Especificar Mapeamento de Coluna**, clique em **Selecionar Tabela de Casos**.  
  
7.  Na caixa de diálogo Selecionar Tabela, selecione uma fonte de dados na lista e a tabela que contém os dados de caso. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  Se a tabela necessária não estiver disponível, feche a caixa de diálogo e crie uma nova exibição da fonte de dados que contenha a tabela. Para obter informações sobre como criar uma exibição de fonte de dados, consulte [Definindo uma exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/defining-a-data-source-view-analysis-services.md).  
  
9. Se o modelo de mineração tiver uma tabela aninhada, clique em **Selecionar Tabela Aninhada** e selecione a tabela aninhada na lista de tabelas na exibição da fonte de dados. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. Selecione a linha de junção do mapeamento que você quer modificar e, depois, **Modificar Conexões**.  
  
     A caixa de diálogo **Modificar Mapeamento** abre. Na tabela nessa caixa de diálogo, **Colunas de Estrutura de Mineração** lista cada coluna que a estrutura de mineração selecionada contém, e **Colunas da tabela** lista as colunas das tabelas de entrada que estão mapeadas para colunas na estrutura de mineração.  
  
11. Em **Coluna da Tabela**, selecione a linha que corresponde à linha em **Colunas de Estrutura de Mineração** para a qual você deseja modificar uma relação. Selecione uma nova coluna ou a entrada em branco na lista para excluir a coluna.  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Os mapeamentos das novas colunas são exibidos na caixa de diálogo **Especificar Mapeamento de Coluna**. Você pode remover um mapeamento selecionando a linha entre as colunas e pressionando a tecla DELETE. Você também pode criar uma nova conexão selecionando uma coluna na tabela **Estrutura de Mineração** e arrastando-a para a coluna correspondente na tabela **Tabelas SelectInput**.  
  
## Consulte também  
 [Tarefas de teste e validação e instruções &#40;Mineração de dados&#41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
  