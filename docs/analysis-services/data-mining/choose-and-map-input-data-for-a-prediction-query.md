---
title: Escolher e mapear dados de entrada para uma consulta de previsão | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0781c35dfe7bcc1ea99be3d68fcbb839d5f9374b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724852"
---
# <a name="choose-and-map-input-data-for-a-prediction-query"></a>Escolher e mapear dados de entrada para uma consulta de previsão
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Quando você cria previsões de um modelo de mineração, geralmente o faz alimentando novos dados no modelo. (A exceção são modelos de série temporal, que só podem fazer previsões com base em dados históricos.) Para oferecer novos dados ao modelo, verifique se os dados estão disponíveis como parte de uma exibição da fonte de dados. Se souber antecipadamente os dados que serão usados na previsão, você poderá incluí-los na exibição de fonte de dados usada para criar o modelo. Caso contrário, talvez precise criar uma nova exibição da fonte de dados. Para obter mais informações, consulte [Exibições de fontes de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
 Às vezes, os dados de que você precisa podem estar contidos em mais de uma tabela em uma junção um-para-muitos. Este é o caso de dados usados em modelos de associação ou modelos de clustering de sequência, que usam uma tabela de casos vinculada a uma tabela aninhada que contém detalhes do produto ou da transação. Se o seu modelo usa uma estrutura de tabela aninhada de caso, os dados usados para previsão também precisam ter uma estrutura de tabela aninhada de caso.  
  
> [!WARNING]  
>  Não é possível adicionar colunas novas ou mapear colunas que estão em uma exibição de fonte de dados diferente. A exibição da fonte de dados selecionada deve conter todas as colunas que você precisa para a consulta de previsão.  
  
 Após identificar as tabelas que contêm os dados a serem usados em previsões, mapeie as colunas nos dados externos para as colunas do modelo de mineração. Por exemplo, se seu modelo prever o comportamento de compra do cliente com base em demografia e em respostas de pesquisa, seus dados de entrada deverão conter informações que geralmente correspondem ao que está no modelo. Você não precisa ter dados correspondentes para cada coluna única, mas quanto maior for o número de colunas com correspondência, melhor. Se você tentar mapear colunas com tipos de dados diferentes, poderá obter um erro. Nesse caso, você pode definir um cálculo nomeado na exibição da fonte de dados para converter os novos dados de coluna no tipo de dados solicitado pelo modelo. Para obter mais informações, consulte [Definir cálculos nomeados em uma exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md).  
  
 Quando você escolher os dados a serem usados para previsão, talvez algumas colunas na fonte de dados selecionada sejam mapeadas automaticamente para as colunas de modelo de mineração, com base na semelhança de nome e no tipo de dados correspondente. Você pode usar a caixa de diálogo **Modificar Mapeamento** na **Previsão de Modelo de Mineração** para alterar as colunas que são mapeadas, excluir mapeamentos impróprios ou criar novos mapeamentos para colunas existentes. A superfície de design **Previsão de Modelo de Mineração** também dá suporte ao recurso de edição do tipo “arrastar e soltar” de conexões.  
  
-   Para criar uma nova conexão, basta selecionar uma coluna na tabela **Modelo de Mineração** e arrastá-la até a coluna correspondente na tabela **Selecionar Tabela(s) de Entrada** .  
  
-   Para remover uma conexão, selecione a linha da conexão e pressione a tecla DELETE.  
  
 O procedimento a seguir descreve como você pode modificar as junções criadas entre a tabela de casos e uma tabela aninhada usadas como entradas para uma consulta de previsão, usando a caixa de diálogo **Especificar Junção Aninhada** .  
  
### <a name="select-an-input-table"></a>Selecionar uma tabela de entrada  
  
1.  Na tabela **Selecionar Tabela(s) de Entrada** da guia **Gráfico de Precisão de Mineração** do Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique em **Selecionar Tabela de Casos**.  
  
     A caixa de diálogo **Selecionar Tabela** é exibida, na qual você pode selecionar a tabela que contém os dados nos quais deseja que as suas consultas se baseiem.  
  
2.  Na caixa de diálogo **Selecionar Tabela** , selecione uma fonte de dados na lista **Fonte de Dados** .  
  
3.  Em **Nome de Tabela/Exibição**, selecione a tabela que contém os dados você quer usar para testar os modelos.  
  
4.  Clique em **OK**.  
  
     As colunas na estrutura de mineração são mapeadas automaticamente para colunas que tenham o mesmo nome na tabela de entrada.  
  
### <a name="change-the-way-that-input-data-is-mapped-to-the-model"></a>Altere a maneira como os dados de entrada são mapeados para o modelo  
  
1.  No Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], selecione a guia **Previsão de Modelo de Mineração** .  
  
2.  No menu **Modelo de Mineração** , selecione **Modificar Conexões**.  
  
     A caixa de diálogo **Modificar Mapeamento** abre. Nesta caixa de diálogo, a coluna **Coluna do Modelo de Mineração** lista as colunas na estrutura de mineração selecionada. A **Coluna da Tabela** lista as colunas na fonte de dados externa que você escolheu na caixa de diálogo **Selecionar Tabela(s) de Entrada** . As colunas na fonte de dados externa são mapeadas para colunas no modelo de mineração.  
  
3.  Em **Coluna da Tabela**, selecione a linha que corresponde à coluna de modelo de mineração para a qual você deseja mapear.  
  
4.  Selecione uma coluna nova na lista de colunas disponíveis na fonte de dados externa. Selecione o item em branco na lista para excluir o mapeamento de coluna.  
  
5.  Clique em **OK**.  
  
     Os novos mapeamentos de coluna são exibidos no designer.  
  
### <a name="remove-a-relationship-between-input-tables"></a>Remover uma relação entre tabelas de entrada  
  
1.  Na tabela **Selecionar Tabela(s) de Entrada** da guia **Previsão do Modelo de Mineração** do Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique em **Modificar Junção**.  
  
     A caixa de diálogo **Especificar Junção Aninhada** é aberta.  
  
2.  Selecione uma relação.  
  
3.  Clique em **Remover Relação**.  
  
4.  Clique em **OK**.  
  
     A relação entre a tabela de casos e a tabela aninhada foi removida.  
  
### <a name="create-a-new-relationship-between-input-tables"></a>Criar uma nova relação entre tabelas de entrada  
  
1.  Na tabela **Selecionar Tabela(s) de Entrada** da guia **Previsão do Modelo de Mineração** do Designer de Mineração de Dados, clique em **Modificar Junção**.  
  
     A caixa de diálogo **Especificar Junção Aninhada** é aberta.  
  
2.  Clique em **Adicionar Relação**.  
  
     A caixa de diálogo **Criar Relação** é aberta.  
  
3.  Selecione a chave da tabela aninhada em **Colunas de Origem**.  
  
4.  Selecione a chave da tabela de casos em **Colunas de Destino**.  
  
5.  Clique em **OK** na caixa de diálogo **Criar Relação** .  
  
6.  Clique em **OK** na caixa de diálogo **Especificar Junção Aninhada** .  
  
     Uma nova relação foi criada entre a tabela de casos e a tabela aninhada.  
  
### <a name="add-a-nested-table-to-the-input-tables-of-a-prediction-query"></a>Adicionar uma tabela aninhada às tabelas de entrada de uma consulta de previsão  
  
1.  Na guia **Previsão de Modelo de Mineração** do Designer de Mineração de Dados, clique em **Selecionar Tabela de Casos** para abrir a caixa de diálogo **Selecionar Tabela** .  
  
    > [!NOTE]  
    >  Não é possível adicionar uma tabela aninhada às entradas, a menos que você tenha especificado uma tabela de casos. O uso de uma tabela aninhada exige que o modelo de mineração usado na previsão também utilize uma tabela aninhada.  
  
2.  Na caixa de diálogo **Selecionar Tabela** , selecione uma fonte de dados da lista **Fonte de Dados** e selecione a tabela na exibição de fonte de dados que contém os dados de caso. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Clique em **Selecionar Tabela Aninhada** para abrir a caixa de diálogo **Selecionar Tabela** .  
  
4.  Na caixa de diálogo **Selecionar Tabela** , selecione uma fonte de dados da lista **Fonte de Dados** e selecione a tabela na exibição de fonte de dados que contém os dados aninhados. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Se já existir uma relação, as colunas no modelo de mineração serão mapeados automaticamente para as colunas que possuem o mesmo nome na tabela de entrada. É possível modificar a relação entre a tabela aninhada e a tabela de casos clicando em **Modificar Junção**, que abre a caixa de diálogo **Criar Relação** .  
  
## <a name="see-also"></a>Consulte também  
 [Consultas de previsão &#40;Mineração de dados&#41;](../../analysis-services/data-mining/prediction-queries-data-mining.md)  
  
  
