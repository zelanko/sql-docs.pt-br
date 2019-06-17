---
title: Estimar o Assistente (Data Mining Add-ins para Excel) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 9b7ffc1b77d90946a119dc462da2057cf3fe4988
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081253"
---
# <a name="estimate-wizard-data-mining-add-ins-for-excel"></a>Assistente de Estimativa (Suplementos de Mineração de Dados para Excel)
  ![Assistente de estimativa na faixa de opções mineração de dados](media/dmc-estimate.gif "Assistente de estimativa na faixa de opções mineração de dados")  
  
 O **estimativa** assistente o ajuda a criar um modelo de estimativa. Um modelo de estimativa extrai padrões dos dados e usa esses padrões para prever os fatores que afetam os resultados.  
  
 A estimativa é usada prever resultados numéricos. Por exemplo, se a coluna de destino contiver taxas de graduação para escolas, com essas taxas de graduação expressas como porcentagens, você poderá analisar os fatores que podem aumentar ou diminuir essas taxas de graduação, como o número de alunos por escola, a proporção aluno-professor e o número de professores.  
  
## <a name="using-the-estimate-data-wizard"></a>Usando o Assistente para Estimar Dados  
  
1.  Sobre o **Data Mining** faixa de opções, clique em **estimativa**.  
  
2.  No **Selecionar fonte de dados** caixa de diálogo, selecione os dados de origem a serem usados. Você pode usar dados em uma Excel **tabela**, um Excel **intervalo de dados**, ou de um **fonte de dados externa**.  
  
     Se você usar uma fonte de dados externa, poderá criar exibições personalizadas ou as consultas e salvá-las como uma fonte de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  No **estimativa** caixa de diálogo, selecione o **coluna para analisar**.  
  
     A coluna de destino deve conter dados numéricos contínuos.  
  
4.  Selecione as colunas a serem usadas como entrada, verificando o **colunas de entrada** caixa de seleção.  
  
     Essas colunas serão usadas para criar os padrões. Você deverá eliminar da análise qualquer coluna que provavelmente não vá ajudar, como números de ID ou colunas que contenham dados irrelevantes.  
  
5.  O **estimativa** assistente seleciona o algoritmo ideal para seu conjunto de dados. No entanto, você pode clicar em **parâmetros** para abrir o **parâmetros de algoritmo** caixa de diálogo e definir opções avançadas.  
  
6.  Se os dados forem numéricos e você pode usar o método de regressão Linear da Microsoft, você pode verificar a **Regressor** caixa para todas as colunas numéricas que você sabe (ou suspeita) a ser correlacionada com o valor previsível.  
  
     O algoritmo irá testar os valores nessa coluna para determinar se eles afetam os resultados. Se você não tiver certeza, clique em **sugerir** e o algoritmo testará toda a coluna e automaticamente detectará os melhores valores para usar como regressores.  
  
    > [!NOTE]  
    >  Um regressor é necessário para criar uma estimativa. O assistente sempre recomenda o melhor regressor, com base em uma passagem inicial sobre os dados. Assim, caso você não tenha certeza, será melhor aceitar as seleções recomendadas.  
  
7.  Sobre o **dividir dados em conjuntos de teste e treinamento** , especifique se deseja criar um pequeno subconjunto dos dados para teste.  
  
8.  Sobre o **concluir** página, fornecer nomes para a nova estrutura de mineração e o modo de mineração ou aceite os nomes padrão que são fornecidos.  
  
9. Defina opções para usar o modelo.  
  
    -   Selecione **procurar** para abrir imediatamente o modelo em um visualizador.  
  
         Esse visualizador gráfico exibe um gráfico de rede de dependências e a árvore de decisão gerada pelo algoritmo. Ao explorar essas informações, você pode entender melhor os fatores que colaboram para os valores estimados.  
  
    -   Selecione **habilitar o detalhamento** para permitir que os usuários de sua análise exibam os dados subjacentes.  
  
         Essa opção estará disponível somente se você usar os algoritmos de Árvore de Decisão ou Regressão Linear.  
  
    -   **Usar modelo temporário**. Se você selecionar esta opção, o modelo não será salvo no servidor. Os modelos temporários serão excluídos quando você fechar o Excel.  
  
## <a name="more-about-estimation-models"></a>Mais informações sobre modelos de estimativa  
 O **estimativa** assistente oferece suporte ao uso de qualquer um dos seguintes algoritmos:  
  
-   Algoritmo de árvore de decisão da Microsoft  
  
-   Algoritmo Regressão Linear da Microsoft  
  
-   Algoritmo Regressão Logística da Microsoft  
  
-   Algoritmo rede neural da Microsoft  
  
 No **parâmetros de algoritmo** caixa de diálogo, você pode definir opções avançadas adicionais, dependendo do algoritmo escolhido. Para obter informações sobre as opções para cada um desses algoritmos, consulte esses tópicos nos Manuais Online do SQL Server:  
  
 [Referência técnica do algoritmo Árvores de Decisão da Microsoft](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Referência Técnica do Algoritmo de Regressão Linear da Microsoft](data-mining/microsoft-linear-regression-algorithm-technical-reference.md)  
  
 [Referência técnica do algoritmo Regressão Logística da Microsoft](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Referência técnica do algoritmo Rede Neural da Microsoft](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>Requisitos  
 Para usar o Assistente para Estimar Dados, você deve estar conectado a um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Para obter informações sobre como criar uma conexão, consulte [conectar-se a fonte de dados &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Para usar um algoritmo de estimativa, o resultado que você está tentando prever deve ser expresso como um valor numérico, por exemplo, uma moeda, um valor de vendas, uma data ou uma hora.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um modelo de mineração de dados](creating-a-data-mining-model.md)   
 [Passo a passo de diagrama de árvore de decisão &#40;suplementos de mineração de dados&#41;](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
  
