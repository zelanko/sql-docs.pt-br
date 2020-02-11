---
title: Cenário de hipóteses (ferramentas de análise de tabela para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- what if scenario
- scenario analysis
ms.assetid: 4df5a5c5-1983-4009-a7c5-cd340649fd2f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fef8ca20bd3e137d21b5121f42a0d7fee82ae4a7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66065386"
---
# <a name="what-if-scenario-table-analysis-tools-for-excel"></a>Cenário E-Se (Ferramentas de Análise de Tabela para Excel)
  ![Botão Cenário E-Se em Ferramentas de Análise de Tabela](media/tat-whatif.gif "Botão Cenário E-Se em Ferramentas de Análise de Tabela")  
  
 A ferramenta de cenário de **hipóteses** analisa padrões em dados existentes e, em seguida, permite que você avalie o efeito que as alterações em uma coluna teriam no valor de uma coluna diferente.  
  
 Por exemplo, você pode explorar o efeito de aumentar o preço de um item em seu total de vendas.  
  
 A ferramenta é flexível em relação ao número de previsões que você pode criar. Após a conclusão da análise inicial, é possível prever alterações para todos os dados da tabela ou inserir um valor de teste de cada vez.  
  
## <a name="using-the-what-if-scenario-tool"></a>Usando a ferramenta de cenário E-Se  
  
1.  Abra uma tabela de dados do Excel.  
  
2.  Clique em **cenários**e, em seguida, selecione **What-If**.  
  
3.  Na caixa **cenário** , selecione a coluna que contém o valor que você irá alterar e especifique a alteração como um valor específico ou como uma porcentagem de alteração (aumentada ou diminuída) nos valores atuais.  
  
4.  Na caixa **o que acontecerá** , especifique a coluna para a qual você deseja avaliar o efeito.  
  
5.  Opcionalmente, clique em **escolher colunas a serem usadas para análise** para selecionar colunas que provavelmente serão úteis para fazer a previsão. Também é possível desmarcar as colunas que provavelmente serão pouco úteis na detecção de padrões, como IDs ou nomes de linhas.  
  
6.  Na caixa **especificar linha ou tabela** , escolha se deseja que o impacto seja avaliado apenas para a linha selecionada no momento ou para o conjunto completo de dados na tabela.  
  
7.  Se você selecionar **nessa linha**, a ferramenta exibirá o resultado na caixa de diálogo. Enquanto a caixa de diálogo permanece aberta, você pode modificar as seleções para testar outros cenários.  
  
8.  Se você selecionar **tabela inteira**, a ferramenta exibirá uma mensagem de status na caixa de diálogo e adicionará duas novas colunas à tabela de dados original. Clique em **fechar** para exibir os resultados completos na planilha.  
  
### <a name="requirements"></a>Requisitos  
 Essa ferramenta usa o algoritmo Regressão Logística da Microsoft, que dá suporte para previsão de valores numéricos ou discretos. No entanto, para obter os melhores resultados, sugerimos as seguintes práticas recomendadas:  
  
-   Selecione colunas para análise que contenham informações úteis.  
  
-   Se você incluir poucas colunas, talvez seja difícil obter um resultado.  
  
-   Se você usar a opção **para valor** , deverá digitar um valor na caixa ou selecionar um valor na lista.  
  
-   Se você usar a opção **percentual** , defina a alteração como uma porcentagem de aumento ou diminuição. O padrão é 120%, significando um aumento de 20% sobre o valor atual.  
  
> [!NOTE]  
>  Se você não definir um valor, talvez receba um erro.  
  
## <a name="understanding-the-results-of-what-if-analysis"></a>Compreendendo os resultados da análise E-Se  
 Quando você cria um cenário de **hipóteses** , a ferramenta faz três coisas:  
  
-   Cria uma estrutura de mineração de dados que armazena os fatos principais sobre os dados na tabela.  
  
-   Cria um modelo de mineração de regressão logística com base nos dados.  
  
-   Cria uma consulta de previsão para cada um dos valores especificados.  
  
 Você pode gerar todas as previsões de uma vez especificando a **tabela inteira**. A ferramenta cria duas colunas novas na tabela de dados original.  
  
 As colunas adicionadas à tabela contêm dois tipos de informações: o valor previsto atribuído à alteração e sua confiança. Confiança significa a probabilidade de a previsão estar correta.  
  
 Também é possível inserir um valor de alteração de cada vez na caixa de diálogo e exibir as previsões de modo interativo. Isso é o mesmo que criar uma *consulta de Previsão Singleton*. Os resultados da consulta de previsão são incluídos na saída com as seguintes informações: o sucesso ou a falha da previsão, o valor previsto e o nível de confiança. O nível de confiança é mostrado como uma barra que contém uma linha pontilhada. Quanto maior a linha pontilhada, maior a confiança no resultado.  
  
 Por exemplo, se você estiver tentando determinar o efeito de aumentar a idade do cliente na disposição do cliente para comprar e aumentar a idade do cliente para 25, a ferramenta **What-If** consultará o modelo de data mining e retornará o seguinte resultado:  
  
 **Análise E-Se para Compras de Bicicletas encontrou uma solução.**  
  
 **'Compras de Bicicletas' = sim**  
  
 **Confiança: Razoável**  
  
 Como esse resultado se baseia em uma linha existente na tabela de dados, isso significa que, para um determinado cliente, se todos os dados referentes ao cliente permanecerem iguais, mas a idade do cliente aumentar para 25, ele provavelmente comprará uma bicicleta.  
  
 Incluir na saída as previsões para a tabela de dados original talvez facilite determinar se elas são úteis.  
  
## <a name="related-tools"></a>Ferramentas relacionadas  
 O Cliente de Mineração de Dados para Excel, um suplemento separado que fornece mais funções avançadas de mineração de dados, contém assistentes para criação de modelos de mineração de dados que preveem comportamento. Para obter mais informações, consulte [criando um modelo de mineração de dados](creating-a-data-mining-model.md).  
  
 Para obter mais informações sobre o algoritmo usado pela ferramenta de cenário de **hipóteses** , consulte o tópico "algoritmo de regressão logística da Microsoft" em manuais online do SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
 [Ferramentas de Análise de Tabela para Excel](table-analysis-tools-for-excel.md)  
  
  
