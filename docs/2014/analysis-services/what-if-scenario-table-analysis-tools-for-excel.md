---
title: Cenário e-se (ferramentas de análise de tabela para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- what if scenario
- scenario analysis
ms.assetid: 4df5a5c5-1983-4009-a7c5-cd340649fd2f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e8355c828cdc3479b108a693b07b3dfb5a92a289
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140356"
---
# <a name="what-if-scenario-table-analysis-tools-for-excel"></a>Cenário E-Se (Ferramentas de Análise de Tabela para Excel)
  ![Que botão cenário se nas ferramentas de análise de tabela](media/tat-whatif.gif "botão cenário e se nas ferramentas de análise de tabela")  
  
 O **hipotética** cenário ferramenta analisa os padrões nos dados existentes e, em seguida, lhe permite avaliar o efeito que as alterações em uma coluna teriam no valor de uma coluna diferente.  
  
 Por exemplo, você pode explorar o efeito de aumentar o preço de um item em seu total de vendas.  
  
 A ferramenta é flexível em relação ao número de previsões que você pode criar. Após a conclusão da análise inicial, é possível prever alterações para todos os dados da tabela ou inserir um valor de teste de cada vez.  
  
## <a name="using-the-what-if-scenario-tool"></a>Usando a ferramenta de cenário E-Se  
  
1.  Abra uma tabela de dados do Excel.  
  
2.  Clique em **cenários**e, em seguida, selecione **hipotética**.  
  
3.  No **cenário** , selecione a coluna que contém o valor que você altere e especifique a alteração como um valor específico ou como uma porcentagem de alteração (seja aumentado ou diminuído) nos valores atuais.  
  
4.  No **o que acontece com** , especifique a coluna para o qual você deseja avaliar o efeito.  
  
5.  Opcionalmente, clique em **escolher colunas a serem usadas para análise** para selecionar as colunas que provavelmente serão úteis na previsão. Também é possível desmarcar as colunas que provavelmente serão pouco úteis na detecção de padrões, como IDs ou nomes de linhas.  
  
6.  No **especificar linha ou tabela** , escolha se deseja que o impacto seja avaliado para apenas a linha atualmente selecionada ou para o conjunto completo de dados na tabela.  
  
7.  Se você selecionar **nesta linha**, a ferramenta exibe o resultado na caixa de diálogo. Enquanto a caixa de diálogo permanece aberta, você pode modificar as seleções para testar outros cenários.  
  
8.  Se você selecionar **toda a tabela**, a ferramenta exibe uma mensagem de status na caixa de diálogo e adicionará duas novas colunas à tabela de dados original. Clique em **fechar** para exibir os resultados completos na planilha.  
  
### <a name="requirements"></a>Requisitos  
 Essa ferramenta usa o algoritmo Regressão Logística da Microsoft, que dá suporte para previsão de valores numéricos ou discretos. No entanto, para obter os melhores resultados, sugerimos as seguintes práticas recomendadas:  
  
-   Selecione colunas para análise que contenham informações úteis.  
  
-   Se você incluir poucas colunas, talvez seja difícil obter um resultado.  
  
-   Se você usar o **ao valor** opção, você deve digitar um valor na caixa ou selecione um valor na lista.  
  
-   Se você usar o **percentual** , defina a alteração como um percentual de aumento ou diminuição. O padrão é 120%, significando um aumento de 20% sobre o valor atual.  
  
> [!NOTE]  
>  Se você não definir um valor, talvez receba um erro.  
  
## <a name="understanding-the-results-of-what-if-analysis"></a>Compreendendo os resultados da análise E-Se  
 Quando você cria um **hipotética** cenário, a ferramenta faz três coisas:  
  
-   Cria uma estrutura de mineração de dados que armazena os fatos principais sobre os dados na tabela.  
  
-   Cria um modelo de mineração de regressão logística com base nos dados.  
  
-   Cria uma consulta de previsão para cada um dos valores especificados.  
  
 Você pode exibir todas as previsões de uma só vez, especificando **toda a tabela**. A ferramenta cria duas colunas novas na tabela de dados original.  
  
 As colunas adicionadas à tabela contêm dois tipos de informações: o valor previsto atribuído à alteração e sua confiança. Confiança significa a probabilidade de a previsão estar correta.  
  
 Também é possível inserir um valor de alteração de cada vez na caixa de diálogo e exibir as previsões de modo interativo. Isso é o mesmo que criar uma *consulta de previsão singleton*. Os resultados da consulta de previsão são incluídos na saída com as seguintes informações: o sucesso ou a falha da previsão, o valor previsto e o nível de confiança. O nível de confiança é mostrado como uma barra que contém uma linha pontilhada. Quanto maior a linha pontilhada, maior a confiança no resultado.  
  
 Por exemplo, se você estiver tentando determinar o efeito do aumento da idade do cliente a disposição do cliente comprar e aumentar a idade do cliente para 25, o **hipotética** ferramenta consulta o modelo de mineração de dados e retorna o resultado da seguinte:  
  
 **Teste de hipóteses para compras de bicicletas encontrou uma solução.**  
  
 **'Compras de bicicletas' = Sim**  
  
 **Confiança: razoável**  
  
 Como esse resultado se baseia em uma linha existente na tabela de dados, isso significa que, para um determinado cliente, se todos os dados referentes ao cliente permanecerem iguais, mas a idade do cliente aumentar para 25, ele provavelmente comprará uma bicicleta.  
  
 Incluir na saída as previsões para a tabela de dados original talvez facilite determinar se elas são úteis.  
  
## <a name="related-tools"></a>Ferramentas relacionadas  
 O Cliente de Mineração de Dados para Excel, um suplemento separado que fornece mais funções avançadas de mineração de dados, contém assistentes para criação de modelos de mineração de dados que preveem comportamento. Para obter mais informações, consulte [criando um modelo de mineração de dados](creating-a-data-mining-model.md).  
  
 Para obter mais informações sobre o algoritmo usado pelas **hipotética** cenário ferramenta, consulte o tópico "Microsoft algoritmo de regressão logística" nos Manuais Online do SQL Server.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de Análise de Tabela para Excel](table-analysis-tools-for-excel.md)  
  
  
