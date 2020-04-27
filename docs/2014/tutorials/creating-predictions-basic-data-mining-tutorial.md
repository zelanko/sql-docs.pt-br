---
title: Criando previsões (tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a8410ed2-bb98-4d51-a9eb-b239be1201c2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 456aec6c6b9d0d1a5d0ee1d9949507a37577130c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67597524"
---
# <a name="creating-predictions-basic-data-mining-tutorial"></a>Criando previsões (Tutorial de mineração de dados básico)
  Depois de testar a precisão dos seus modelos de mineração e decidir que você está satisfeito com os resultados, você pode gerar previsões usando o Construtor de Consultas de previsão na guia **previsão do modelo de mineração** no designer de mineração de dados.  
  
 O Construtor de Consultas de Previsão contém três exibições. Com as exibições de **design** e **consulta** , você pode criar e examinar sua consulta. Em seguida, você pode executar a consulta e exibir os resultados na exibição de **resultado** .  
  
 Todas as consultas de previsão usam DMX, que é a abreviação da linguagem Data Mining Extensions. O DMX tem sintaxe semelhante à de T-SQL mas é usado para consultas em objetos de mineração de dados. Embora a sintaxe DMX não seja complicada, o uso de um construtor de consultas como este, ou o do [SQL Server suplementos de mineração de dados para Office](../../2014/analysis-services/data-mining/sql-server-data-mining-add-ins-for-office.md), facilita muito a seleção de entradas e a criação de expressões, portanto, é altamente recomendável que você aprenda os conceitos básicos.  
  
## <a name="creating-the-query"></a>Criando a consulta  
 A primeira etapa na criação de uma consulta de previsão é selecionar um modelo de mineração e tabela de entrada.  
  
#### <a name="to-select-a-model-and-input-table"></a>Para selecionar um modelo e uma tabela de entrada  
  
1.  Na guia **previsão do modelo de mineração** do designer de mineração de dados, na caixa **modelo de mineração** , clique em **selecionar modelo**.  
  
2.  Na caixa de diálogo **selecionar modelo de mineração** , navegue pela árvore até a estrutura de **endereçamento direcionada** , expanda a `TM_Decision_Tree`estrutura, selecione e clique em **OK**.  
  
3.  Na caixa **selecionar tabela (s) de entrada** , clique em **selecionar tabela de casos**.  
  
4.  Na caixa de diálogo **selecionar tabela** , na lista **fonte de dados** , selecione a exibição [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]da fonte de dados.  
  
5.  Em **nome da tabela/exibição**, selecione a tabela **ProspectiveBuyer (dbo)** e clique em **OK**.  
  
     A `ProspectiveBuyer` tabela é mais parecida com a tabela de casos **vTargetMail** .  
  
## <a name="mapping-the-columns"></a>Mapeando as colunas  
 Depois de selecionar a tabela de entrada, o Construtor de Consultas de Previsão cria um mapeamento padrão entre o modelo de mineração e a tabela de entrada, com base nos nomes das colunas. Pelo menos uma coluna da estrutura deve corresponder a uma coluna nos dados externos.  
  
> [!IMPORTANT]  
>  Os dados que você usa para determinar a precisão dos modelos devem conter uma coluna que possa ser mapeada para a coluna previsível. Se essa coluna não existir, você poderá criar uma com valores vazios, mas ela precisa ter o mesmo tipo de dados que a coluna previsível.  
  
#### <a name="to-map-the-inputs-to-the-model"></a>Para mapear as entradas para o modelo  
  
1.  Clique com o botão direito do mouse na janela linhas conectando o **modelo de mineração** à janela **selecionar tabela de entrada** e selecione **Modificar Conexões**.  
  
     Observe que nem todas as colunas são mapeadas. Adicionaremos mapeamentos para várias **colunas da tabela**. Também geraremos uma nova coluna de data de aniversário com base na coluna de data atual, visando melhorar a correspondência das colunas.  
  
2.  Em **coluna da tabela**, clique `Bike Buyer` na célula e selecione ProspectiveBuyer. Unknown na lista suspensa.  
  
     Isso mapeia a coluna previsível, [Comprador de Bicicleta], para uma coluna da tabela de entrada.  
  
3.  Clique em **OK**.  
  
4.  Em **Gerenciador de soluções**, clique com o botão direito do mouse na exibição da fonte de dados de **endereçamento direcionada** e selecione **Designer de exibição**.  
  
5.  Clique com o botão direito do mouse na tabela, ProspectiveBuyer e selecione **novo cálculo nomeado**.  
  
6.  Na caixa de diálogo **criar cálculo nomeado** , para **nome da coluna**, `calcAge`digite.  
  
7.  Para **Descrição**, digite **Calculate age com base em DataDeNascimento**.  
  
8.  Na caixa **expressão** , digite `DATEDIFF(YYYY,[BirthDate],getdate())` e clique em **OK**.  
  
     Como a tabela de entrada não tem nenhuma coluna de **idade** correspondente à do modelo, você pode usar essa expressão para calcular a idade do cliente da coluna DataDeNascimento na tabela de entrada. Como a **idade** foi identificada como a coluna mais influente para prever a compra de bicicletas, ela deve existir tanto no modelo quanto na tabela de entrada.  
  
9. No designer de mineração de dados, selecione a guia **previsão do modelo de mineração** e abra novamente a janela **Modificar Conexões** .  
  
10. Em **coluna da tabela**, clique na célula **idade** e selecione ProspectiveBuyer. Calc na lista suspensa.  
  
    > [!WARNING]  
    >  Se você não encontrar a coluna na lista, poderá ter que atualizar a definição da exibição da fonte de dados que é carregada no designer. Para fazer isso, no menu **arquivo** , selecione **salvar tudo**e, em seguida, feche e abra novamente o projeto no designer.  
  
11. Clique em **OK**.  
  
## <a name="designing-the-prediction-query"></a>Criando a consulta de previsão  
  
1.  O primeiro botão na barra de ferramentas da guia **previsão do modelo de mineração** é alternar para modo de exibição de **design/alternar para exibição de resultado/alternar para o botão de exibição de consulta** . Clique na seta para baixo nesse botão e selecione **design**.  
  
2.  Na grade da guia **previsão do modelo de mineração** , clique na célula na primeira linha vazia da coluna **origem** e selecione **função de previsão**.  
  
3.  Na linha **função de previsão** , na coluna **campo** , selecione `PredictProbability`.  
  
     Na coluna **alias** da mesma linha, digite **probabilidade de resultado**.  
  
4.  Na janela **modelo de mineração** acima, selecione e arraste [comprador de bicicleta] para a célula **critérios/argumento** .  
  
     Quando você permitir, acesse [TM_Decision_Tree]. [Comprador de bicicleta] aparece na célula **critérios/argumento** .  
  
     Isso especifica a coluna de destino da função `PredictProbability`. Para obter mais informações sobre o functions, consulte [Data Mining Extensions &#40;DMX&#41; referência de função](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
5.  Clique na próxima linha vazia na coluna **origem** e selecione **TM_Decision_Tree** modelo de mineração.  
  
6.  Na `TM_Decision_Tree` linha, na coluna **campo** , selecione `Bike Buyer`.  
  
7.  Na `TM_Decision_Tree` linha, na coluna **critérios/argumento** , digite `=1`.  
  
8.  Clique na próxima linha vazia na coluna **origem** e selecione **tabela ProspectiveBuyer**.  
  
9. Na `ProspectiveBuyer` linha, na coluna **campo** , selecione **ProspectiveBuyerKey**.  
  
     Essa ação adicionará o identificador exclusivo à consulta de previsão para que você possa identificar a probabilidade de alguém comprar ou não uma bicicleta.  
  
10. Adicione mais cinco linhas à grade. Para cada linha, selecione a **tabela ProspectiveBuyer** como a **origem** e, em seguida, adicione as seguintes colunas nas células do **campo** :  
  
    -   calcAge  
  
    -   LastName  
  
    -   Nome  
  
    -   AddressLine1  
  
    -   AddressLine2  
  
 Por fim, execute a consulta e navegue pelos resultados.  
  
 O **Construtor de consultas de previsão** também inclui estes controles:  
  
-   **Mostrar** caixa de seleção  
  
     Permite remover as cláusulas de consulta sem precisar excluí-las do designer. Essa opção pode ser útil quando você está trabalhando com consultas complexas e deseja preservar a sintaxe sem precisar copiar e colar a linguagem DMX na janela.  
  
-   **Agrupar**  
  
     insere um parênteses de abertura (à esquerda) no início da linha selecionada, ou insere um parêntese de fechamento (à direita) no final da linha atual.  
  
-   **E/OU**  
  
     insere o operador `AND` ou o operador `OR` logo após a função ou coluna atual.  
  
#### <a name="to-run-the-query-and-view-results"></a>Para executar a consulta e exibir resultados  
  
1.  Na guia **previsão do modelo de mineração** , selecione o botão **resultado** .  
  
2.  Depois que a consulta for executada e os resultados exibidos, você poderá revisá-los.  
  
     A guia **previsão do modelo de mineração** exibe informações de contato para clientes potenciais que provavelmente são compradores de bicicletas. A **probabilidade de coluna de resultado** indica a probabilidade de a previsão estar correta. Você poderá usar esses resultados para determinar para quais clientes em potencial a mala direta deverá ser direcionada.  
  
3.  Neste momento, você pode salvar os resultados. Você tem três opções:  
  
    -   Clique com o botão direito do mouse em uma linha de dados nos resultados e selecione **copiar** para salvar apenas esse valor (e o título da coluna) na área de transferência.  
  
    -   Clique com o botão direito do mouse em qualquer linha nos resultados e selecione **copiar tudo** para copiar todo o conjunto de resultados, incluindo títulos de coluna, para a área de transferência.  
  
    -   Clique em **salvar resultado da consulta** para salvar os resultados diretamente em um banco de dados da seguinte maneira:  
  
        1.  Na caixa de diálogo **salvar resultado da consulta de mineração de dados** , selecione uma fonte de dados ou defina uma nova fonte de dados.  
  
        2.  Digite um nome para a tabela que conterá os resultados da consulta.  
  
        3.  Use a opção, **Adicionar ao DSV**, para criar a tabela e adicioná-la a uma exibição da fonte de dados existente. Isso será útil se você quiser manter todas as tabelas relacionadas para um modelo, como dados de treinamento, dados de origem de previsão e resultados da consulta, na mesma exibição da fonte de dados.  
  
        4.  Use a opção **substituir se existir**, para atualizar uma tabela existente com os resultados mais recentes.  
  
             Use a opção para substituir a tabela se você adicionou alguma coluna à consulta de previsão, alterou os nomes ou tipos de dados de alguma coluna na consulta de previsão, ou se executou alguma instrução ALTER na tabela de destino.  
  
             Além disso, se várias colunas tiverem o mesmo nome (por exemplo, a **expressão**de nome de coluna padrão), você deverá criar um alias para as colunas com nomes duplicados ou um erro será gerado quando o designer tentar salvar os resultados em SQL Server. A razão é que o SQL Server não permite que várias colunas tenham o mesmo nome.  
  
             Para obter mais informações, consulte [caixa de diálogo Salvar resultado da consulta de mineração de dados &#40;exibição de previsão do modelo de mineração&#41;](../../2014/analysis-services/save-data-mining-query-result-dialog-box-mining-model-prediction-view.md).  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Usando o detalhamento em dados de estrutura &#40;tutorial de mineração de dados básico&#41;](../../2014/tutorials/using-drillthrough-on-structure-data-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Criar uma consulta de previsão usando o construtor de consultas de previsão](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
