---
title: Criando previsões (Tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: a8410ed2-bb98-4d51-a9eb-b239be1201c2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0001b04a93c1aacfbf2e7701faada815cb6316ac
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52515457"
---
# <a name="creating-predictions-basic-data-mining-tutorial"></a>Criando previsões (Tutorial de mineração de dados básico)
  Depois de testar a precisão dos modelos de mineração e decidir que está satisfeito com os resultados, você pode, em seguida, gerar previsões usando o construtor de consultas de previsão sobre a **previsão do modelo de mineração** guia na mineração de dados Designer.  
  
 O Construtor de Consultas de Previsão contém três exibições. Com o **Design** e **consulta** modos de exibição, você pode criar e examinar sua consulta. Você pode executar a consulta e exibir os resultados na **resultado** modo de exibição.  
  
 Todas as consultas de previsão usam DMX, que é a abreviação da linguagem Data Mining Extensions. O DMX tem sintaxe semelhante à de T-SQL mas é usado para consultas em objetos de mineração de dados. Embora a sintaxe DMX não seja complicada, usando um construtor de consultas como este ou aquele na [SQL Server Data Mining Add-Ins para o Office](../../2014/analysis-services/data-mining/sql-server-data-mining-add-ins-for-office.md), facilita muito a seleção de entradas e construir expressões, portanto, é altamente recomendável que você aprenda as Noções básicas.  
  
## <a name="creating-the-query"></a>Criando a consulta  
 A primeira etapa na criação de uma consulta de previsão é selecionar um modelo de mineração e tabela de entrada.  
  
#### <a name="to-select-a-model-and-input-table"></a>Para selecionar um modelo e uma tabela de entrada  
  
1.  No **previsão do modelo de mineração** guia do Designer de mineração de dados, no **modelo de mineração** , clique em **Selecionar modelo**.  
  
2.  No **Selecionar modelo de mineração** diálogo caixa, navegue pela árvore até ao **mala** estrutura, expanda a estrutura, selecione `TM_Decision_Tree`e, em seguida, clique em **Okey**.  
  
3.  No **Selecionar tabela (s) de entrada** , clique em **Selecionar tabela de casos**.  
  
4.  No **Selecionar tabela** na caixa de **fonte de dados** , selecione o modo de exibição de fonte de dados [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)].  
  
5.  Na **nome da tabela/exibição**, selecione o **ProspectiveBuyer (dbo)** de tabela e, em seguida, clique em **Okey**.  
  
     O `ProspectiveBuyer` tabela mais parecida com a **vTargetMail** tabela de casos.  
  
## <a name="mapping-the-columns"></a>Mapeando as colunas  
 Depois de selecionar a tabela de entrada, o Construtor de Consultas de Previsão cria um mapeamento padrão entre o modelo de mineração e a tabela de entrada, com base nos nomes das colunas. Pelo menos uma coluna da estrutura deve corresponder a uma coluna nos dados externos.  
  
> [!IMPORTANT]  
>  Os dados que você usa para determinar a precisão dos modelos devem conter uma coluna que possa ser mapeada para a coluna previsível. Se essa coluna não existir, você poderá criar uma com valores vazios, mas ela precisa ter o mesmo tipo de dados que a coluna previsível.  
  
#### <a name="to-map-the-inputs-to-the-model"></a>Para mapear as entradas para o modelo  
  
1.  As linhas que conectam com o botão direito do **modelo de mineração** janela para o **Selecionar tabela de entrada** janela e selecione **modificar conexões**.  
  
     Observe que nem todas as colunas são mapeadas. Adicionaremos mapeamentos para várias **colunas da tabela**. Também geraremos uma nova coluna de data de aniversário com base na coluna de data atual, visando melhorar a correspondência das colunas.  
  
2.  Sob **coluna da tabela**, clique no `Bike Buyer` de célula e selecione Prospectivebuyer no menu suspenso.  
  
     Isso mapeia a coluna previsível, [Comprador de Bicicleta], para uma coluna da tabela de entrada.  
  
3.  Clique em **OK**.  
  
4.  Na **Gerenciador de soluções**, com o botão direito do **mala** exibição da fonte de dados e selecione **View Designer**.  
  
5.  A tabela, ProspectiveBuyer, com o botão direito e selecione **novo cálculo nomeado**.  
  
6.  No **criar cálculo nomeado** caixa de diálogo, para **nome da coluna**, tipo `calcAge`.  
  
7.  Para **descrição**, digite **calcular idade com base na data de nascimento**.  
  
8.  No **expressão** , digite `DATEDIFF(YYYY,[BirthDate],getdate())` e, em seguida, clique em **Okey**.  
  
     Porque a tabela de entrada não tem nenhum **idade** coluna correspondente no modelo, você pode usar essa expressão para calcular a idade do cliente da coluna BirthDate da tabela de entrada. Uma vez que **idade** foi identificado como mais influentes coluna para prever a compra de bicicletas, ele deve existir no modelo e na tabela de entrada.  
  
9. No Designer de mineração de dados, selecione a **previsão de modelo de mineração** guia e abra novamente o **modificar conexões** janela.  
  
10. Sob **coluna da tabela**, clique no **idade** de célula e selecione CalcAge na lista suspensa.  
  
    > [!WARNING]  
    >  Se você não encontrar a coluna na lista, poderá ter que atualizar a definição da exibição da fonte de dados que é carregada no designer. Para fazer isso, a partir de **arquivo** menu, selecione **salvar todos os**e, em seguida, feche e reabra o projeto no designer.  
  
11. Clique em **OK**.  
  
## <a name="designing-the-prediction-query"></a>Criando a consulta de previsão  
  
1.  O primeiro botão na barra de ferramentas do **previsão do modelo de mineração** guia é o **Switch para projetar exibir / alternar para a exibição de resultado / alternar para modo de exibição de consulta** botão. Clique na seta para baixo no botão e selecione **Design**.  
  
2.  Na grade a **previsão de modelo de mineração** guia, clique na célula na primeira linha vazia na **fonte** coluna e, em seguida, selecione **função de previsão**.  
  
3.  No **função de previsão** linha, o **campo** coluna, selecione `PredictProbability`.  
  
     No **Alias** coluna da mesma linha, digite **probabilidade de resultado**.  
  
4.  Dos **modelo de mineração** janela acima, selecione e arraste [comprador de bicicleta] para o **critérios/argumento** célula.  
  
     Quando você soltar o botão, [TM_Decision_Tree]. [Bike Buyer] é exibido na **critérios/argumento** célula.  
  
     Isso especifica a coluna de destino da função `PredictProbability`. Para obter mais informações sobre funções, consulte [extensões de mineração de dados &#40;DMX&#41; referência de função](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
5.  Clique na próxima linha vazia na **fonte** coluna e o modelo de mineração, em seguida, selecione TM_Decision_Tree **.**  
  
6.  No `TM_Decision_Tree` linha, o **campo** coluna, selecione `Bike Buyer`.  
  
7.  No `TM_Decision_Tree` linha, o **critérios/argumento** coluna, digite `=1`.  
  
8.  Clique na próxima linha vazia na **fonte** coluna e, em seguida, selecione **tabela ProspectiveBuyer**.  
  
9. No `ProspectiveBuyer` linha, o **campo** coluna, selecione **ProspectiveBuyerKey**.  
  
     Essa ação adicionará o identificador exclusivo à consulta de previsão para que você possa identificar a probabilidade de alguém comprar ou não uma bicicleta.  
  
10. Adicione mais cinco linhas à grade. Para cada linha, selecione **tabela ProspectiveBuyer** como o **fonte** e, em seguida, adicione as seguintes colunas no **campo** células:  
  
    -   calcAge  
  
    -   LastName  
  
    -   FirstName  
  
    -   AddressLine1  
  
    -   AddressLine2  
  
 Por fim, execute a consulta e navegue pelos resultados.  
  
 O **construtor de consultas de previsão** também inclui esses controles:  
  
-   **Mostrar** caixa de seleção  
  
     Permite remover as cláusulas de consulta sem precisar excluí-las do designer. Essa opção pode ser útil quando você está trabalhando com consultas complexas e deseja preservar a sintaxe sem precisar copiar e colar a linguagem DMX na janela.  
  
-   **Agrupar**  
  
     insere um parênteses de abertura (à esquerda) no início da linha selecionada, ou insere um parêntese de fechamento (à direita) no final da linha atual.  
  
-   **E/OU**  
  
     insere o operador `AND` ou o operador `OR` logo após a função ou coluna atual.  
  
#### <a name="to-run-the-query-and-view-results"></a>Para executar a consulta e exibir resultados  
  
1.  No **previsão de modelo de mineração** guia, selecione o **resultado** botão.  
  
2.  Depois que a consulta for executada e os resultados exibidos, você poderá revisá-los.  
  
     O **previsão de modelo de mineração** guia exibe informações de contato para clientes potenciais que provavelmente serão os compradores de bicicleta. O **probabilidade do resultado** coluna indica a probabilidade da previsão estar correta. Você poderá usar esses resultados para determinar para quais clientes em potencial a mala direta deverá ser direcionada.  
  
3.  Neste momento, você pode salvar os resultados. Você tem três opções:  
  
    -   Uma linha de dados nos resultados com o botão direito e selecione **cópia** para salvar apenas esse valor (e o título de coluna) na área de transferência.  
  
    -   Qualquer linha nos resultados com o botão direito e selecione **copiar tudo** para copiar o conjunto de resultados inteiro, inclusive os títulos de coluna, na área de transferência.  
  
    -   Clique em **Salvar resultado da consulta** para salvar os resultados diretamente para um banco de dados da seguinte maneira:  
  
        1.  No **Salvar resultado mineração de dados consulta** caixa de diálogo, selecione uma fonte de dados ou definir uma nova fonte de dados.  
  
        2.  Digite um nome para a tabela que conterá os resultados da consulta.  
  
        3.  Use a opção **adicione à DSV**, para criar a tabela e adicioná-lo para uma exibição da fonte de dados existente. Isso é útil se você quiser manter todas as tabelas relacionadas para um modelo, como dados de treinamento, dados de origem de previsão e consulta os resultados-na mesma exibição da fonte de dados.  
  
        4.  Use a opção **substituir se existir**, para atualizar uma tabela existente com os resultados mais recentes.  
  
             Use a opção para substituir a tabela se você adicionou alguma coluna à consulta de previsão, alterou os nomes ou tipos de dados de alguma coluna na consulta de previsão, ou se executou alguma instrução ALTER na tabela de destino.  
  
             Além disso, se várias colunas tiverem o mesmo nome (por exemplo, o nome da coluna padrão **expressão**) você deve criar um alias para as colunas com nomes duplicados ou um erro será gerado quando o designer tentar salvar os resultados para o SQL Servidor. A razão é que o SQL Server não permite que várias colunas tenham o mesmo nome.  
  
             Para obter mais informações, consulte [salvar dados mineração consulta resultado da caixa de diálogo &#40;exibição da previsão do modelo de mineração&#41;](../../2014/analysis-services/save-data-mining-query-result-dialog-box-mining-model-prediction-view.md).  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Usando o detalhamento em dados da estrutura &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/using-drillthrough-on-structure-data-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma consulta de previsão usando o Construtor de Consultas de previsão](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
