---
title: Assistente de estimativa (suplementos de mineração de dados para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data modeling [data mining]
- estimation
ms.assetid: 7f2b1d5f-c9b3-4939-b35a-34ae099af15f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2706dae37c1dc303aa6708fe1f7387a39835e4d5
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528363"
---
# <a name="estimate-wizard-data-mining-add-ins-for-excel"></a>Assistente de Estimativa (Suplementos de Mineração de Dados para Excel)
  ![Assistente de Estimativa na faixa de opções Mineração de Dados](media/dmc-estimate.gif "Assistente de Estimativa na faixa de opções Mineração de Dados")  
  
 O assistente de **estimativa** ajuda a criar um modelo de estimativa. Um modelo de estimativa extrai padrões dos dados e usa esses padrões para prever os fatores que afetam os resultados.  
  
 A estimativa é usada prever resultados numéricos. Por exemplo, se a coluna de destino contiver taxas de graduação para escolas, com essas taxas de graduação expressas como porcentagens, você poderá analisar os fatores que podem aumentar ou diminuir essas taxas de graduação, como o número de alunos por escola, a proporção aluno-professor e o número de professores.  
  
## <a name="using-the-estimate-data-wizard"></a>Usando o Assistente para Estimar Dados  
  
1.  Na faixa de faixas de **mineração de dados** , clique em **estimativa**.  
  
2.  Na caixa de diálogo **selecionar dados de origem** , selecione os dados de origem a serem usados. Você pode usar dados em uma **tabela**do Excel, um **intervalo de dados**do Excel ou de uma **fonte de dados externa**.  
  
     Se você usar uma fonte de dados externa, poderá criar exibições personalizadas ou as consultas e salvá-las como uma fonte de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  Na caixa de diálogo **estimativa** , selecione a **coluna a ser analisada**.  
  
     A coluna de destino deve conter dados numéricos contínuos.  
  
4.  Selecione as colunas a serem usadas como entrada marcando a caixa de seleção **colunas de entrada** .  
  
     Essas colunas serão usadas para criar os padrões. Você deverá eliminar da análise qualquer coluna que provavelmente não vá ajudar, como números de ID ou colunas que contenham dados irrelevantes.  
  
5.  O assistente de **estimativa** seleciona o algoritmo ideal para seu conjunto de dados. No entanto, você pode clicar em **parâmetros** para abrir a caixa de diálogo **parâmetros de algoritmo** e definir opções avançadas.  
  
6.  Se os dados forem numéricos e você puder usar o método de regressão linear da Microsoft, você poderá marcar a caixa **regressor** para todas as colunas numéricas que você souber (ou fortemente suspeitas) que serão correlacionadas com o valor previsível.  
  
     O algoritmo irá testar os valores nessa coluna para determinar se eles afetam os resultados. Se você não tiver certeza, clique em **sugerir** e o algoritmo testará todas as colunas e detectará automaticamente os melhores valores a serem usados como regressores.  
  
    > [!NOTE]  
    >  Um regressor é necessário para criar uma estimativa. O assistente sempre recomenda o melhor regressor, com base em uma passagem inicial sobre os dados. Assim, caso você não tenha certeza, será melhor aceitar as seleções recomendadas.  
  
7.  Na página **dividir os dados em conjuntos de treinamento e teste** , especifique se deseja criar um pequeno subconjunto dos dados para teste.  
  
8.  Na página **concluir** , forneça nomes para a nova estrutura de mineração e modo de mineração, ou aceite os nomes padrão fornecidos.  
  
9. Defina opções para usar o modelo.  
  
    -   Selecione **procurar** para abrir imediatamente o modelo em um visualizador.  
  
         Esse visualizador gráfico exibe um gráfico de rede de dependências e a árvore de decisão gerada pelo algoritmo. Ao explorar essas informações, você pode entender melhor os fatores que colaboram para os valores estimados.  
  
    -   Selecione **habilitar detalhamento** para permitir que os usuários da sua análise exibam os dados subjacentes.  
  
         Essa opção estará disponível somente se você usar os algoritmos de Árvore de Decisão ou Regressão Linear.  
  
    -   **Use o modelo temporário**. Se você selecionar esta opção, o modelo não será salvo no servidor. Os modelos temporários serão excluídos quando você fechar o Excel.  
  
## <a name="more-about-estimation-models"></a>Mais informações sobre modelos de estimativa  
 O assistente de **estimativa** dá suporte ao uso de qualquer um dos seguintes algoritmos:  
  
-   Algoritmo da árvore de decisão da Microsoft  
  
-   Algoritmo Regressão Linear da Microsoft  
  
-   Algoritmo Regressão Logística da Microsoft  
  
-   Algoritmo rede neural da Microsoft  
  
 Na caixa de diálogo **parâmetros de algoritmo** , você pode definir opções avançadas adicionais, dependendo do algoritmo escolhido. Para obter informações sobre as opções para cada um desses algoritmos, consulte esses tópicos nos Manuais Online do SQL Server:  
  
 [Referência técnica do algoritmo Árvores de Decisão da Microsoft](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Referência Técnica do Algoritmo de Regressão Linear da Microsoft](data-mining/microsoft-linear-regression-algorithm-technical-reference.md)  
  
 [Referência técnica do algoritmo Regressão Logística da Microsoft](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Microsoft Neural Network Algorithm Technical Reference](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>Requisitos  
 Para usar o Assistente para Estimar Dados, você deve estar conectado a um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Para obter informações sobre como criar uma conexão, consulte [conectar-se a dados de origem &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Para usar um algoritmo de estimativa, o resultado que você está tentando prever deve ser expresso como um valor numérico, por exemplo, uma moeda, um valor de vendas, uma data ou uma hora.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um modelo de mineração de dados](creating-a-data-mining-model.md)   
 [Explicação do diagrama de árvore de decisão &#40;suplementos de mineração de dados&#41;](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
  
