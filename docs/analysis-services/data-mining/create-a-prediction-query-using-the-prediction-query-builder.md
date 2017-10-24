---
title: "Criar uma consulta de previsão usando o construtor de consultas de previsão | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- prediction queries [Analysis Services]
- Mining Model Prediction [Analysis Services], prediction queries
ms.assetid: e02836e5-dd8c-4c97-a078-840ae79d3660
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3a61c0e05e427ef4d4e693e1594598dafe85f3c2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-prediction-query-using-the-prediction-query-builder"></a>Criar uma consulta de previsão usando o construtor de consultas de previsão
  Você pode criar consultas de previsão enquanto estiver criando uma solução de mineração de dados no BI Development Studio, ou clicar com o botão direito em um modelo de mineração existente no SQL Server Management Studio e, em seguida, escolher a opção **Criar Consulta de Previsão**.  
  
 O **Construtor de Consultas de Previsão** tem os três modos de design a seguir, os quais você pode alternar clicando nos ícones no canto superior esquerdo.  
  
-   **Design**  
  
-   **Consulta**  
  
-   **Resultado**  
  
 O modo de**design** permite criar uma consulta de previsão escolhendo dados de entrada, mapeando os dados para o modelo e adicionando funções de previsão em instruções que você cria usando a grade. A grade de design contém estes blocos de construção:  
  
 **Origem**  
 Escolha a origem da nova coluna. Você pode usar colunas do modelo de mineração, tabelas de entrada incluídas na exibição da fonte de dados, uma função de previsão ou uma expressão personalizada.  
  
 **Campo**  
 Determina a coluna ou função específica associada à seleção na coluna **Origem** .  
  
 **Alias**  
 Determina como a coluna será nomeada no conjunto de resultados.  
  
 **Mostrar**  
 Determina se a seleção na coluna **Origem** é exibida nos resultados.  
  
 **Agrupar**  
 Trabalha com a coluna **E/Ou** para agrupar expressões usando parênteses. Por exemplo, (expr1 ou expr2) e expr3.  
  
 **E/Ou**  
 Cria lógica na consulta. Por exemplo, (expr1 ou expr2) e expr3.  
  
 **Critérios/Argumento**  
 Especifica uma condição ou expressão de usuário que se aplica à coluna. Você pode arrastar colunas das tabelas para a célula.  
  
 O modo de**Consulta** fornece um editor de texto que dá a você acesso direto à linguagem DMX (extensões DMX), junto com uma exibição dos dados de entrada e das colunas de modelo. Quando você seleciona o modo **Consulta** , a grade usada para definir a consulta é substituída por um editor de texto básico. Você pode usar este editor para copiar e salvar consultas que você compôs ou colar em consultas DMX existentes e da Área de transferência e executá-las.  
  
 A exibição de**Resultado** executa a consulta atual e exibe os resultados em uma grade. Se os dados subjacentes forem alterados e você desejar executar novamente a consulta, clique no botão Executar na barra de status  
  
 Você pode criar uma consulta de mineração de dados usando uma combinação das ferramentas visuais e do editor de texto. Se você digita alterações na consulta no editor de texto e volta ao modo de exibição de **Design** , todas as alterações são perdidas, e a consulta é revertida para a consulta original criada pelo Construtor de Consulta de Previsão. Este tópico orienta o uso do construtor de consultas gráficas.  
  
### <a name="to-create-a-prediction-query"></a>Para criar uma consulta de previsão  
  
1.  Clique na guia **Previsão do Modelo de Mineração** do Designer de Mineração de Dados.  
  
2.  Clique em **Selecionar Modelo** na tabela **Modelo de Mineração** .  
  
     A caixa de diálogo **Selecionar Modelo de Mineração** é aberta e mostra todas as estruturas de mineração existentes no projeto atual.  
  
3.  Selecione o modelo no qual você deseja criar uma previsão e clique em **OK**.  
  
4.  Na tabela **Selecionar Tabela(s) de Entrada** , clique em **Selecionar Tabela de Casos**.  
  
     A caixa de diálogo **Selecionar Tabela** é aberta.  
  
5.  Na lista **Fonte de Dados** , selecione a fonte de dados que contém os dados com os quais você deseja criar uma previsão.  
  
6.  Na caixa **Nome da Tabela/Exibição** , selecione a tabela que contém os dados nos quais você deseja criar uma previsão e clique em **OK**.  
  
     Depois de selecionar a tabela de entrada, o Construtor de Consultas de Previsão cria um mapeamento padrão entre o modelo de mineração e a tabela de entrada, com base nos nomes das colunas. Para excluir um mapeamento, clique para selecionar a linha que vincula a coluna da tabela **Modelo de Mineração** à coluna mapeada da tabela **Selecionar Tabela(s) de Entrada** e, em seguida, pressione a tecla DELETE. Você também pode criar mapeamentos manualmente clicando em uma coluna da tabela **Selecionar Tabela(s) de Entrada** e arrastando-a para a coluna correspondente da tabela **Modelo de Mineração** .  
  
7.  Adicione qualquer combinação destes três tipos de informação à grade Construtor de Consultas de Previsão:  
  
    -   Colunas previsíveis na caixa **Modelo de Mineração** .  
  
    -   Qualquer combinação de colunas de entrada na caixa **Selecionar Tabela(s) de Entrada** .  
  
    -   Funções de previsão  
  
8.  Execute a consulta clicando no primeiro botão da barra de ferramentas da guia **Previsão do Modelo de Mineração** e selecione **Resultado**.  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma consulta Singleton no Designer de Mineração de Dados](../../analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer.md)   
 [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md)  
  
  

