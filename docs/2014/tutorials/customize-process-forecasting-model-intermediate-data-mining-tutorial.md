---
title: Personalizando e processando o modelo de previsão (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4bd25e15-9d9e-4528-b7bc-ccb856643aec
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d2d0e73d1d9a4058ff63320552604b2bfa1bca8a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63249398"
---
# <a name="customizing-and-processing-the-forecasting-model-intermediate-data-mining-tutorial"></a>Personalizando e processando o modelo de previsão (Tutorial de mineração de dados intermediário)
  O algoritmo MTS da [!INCLUDE[msCoName](../includes/msconame-md.md)] oferece vários parâmetros que afetam o modo como um modelo é criado e como os dados de tempo são analisados. Alterar essas propriedades pode afetar significativamente a forma como o modelo de mineração faz previsões.  
  
 Para esta tarefa do tutorial, você executará as seguintes tarefas para modificar o modelo:  
  
1.  Você personalizará a maneira como seu modelo lida com períodos de tempo adicionando um novo valor para o parâmetro *PERIODICITY_HINT* .  
  
2.  Você aprenderá dois outros parâmetros importantes para o algoritmo MTS: FORECAST_METHOD, que permite controlar o método usado na previsão, e PREDICTION_SMOOTHING, que permite personalizar a combinação de previsões de longo prazo e de curto prazo.  
  
3.  Opcionalmente, você dirá ao algoritmo como deseja inserir os valores ausentes.  
  
4.  Depois de fazer todas as alterações, você implantará e processará o modelo.  
  
## <a name="setting-time-series-parameters"></a>Definindo os parâmetros de série temporal  
 **Dicas de periodicidade**  
  
 O parâmetro *PERIODICITY_HINT* fornece o algoritmo com informações sobre períodos de tempo adicionais que você espera ver nos dados. Por padrão, os modelos de série temporal tentarão detectar automaticamente um padrão nos dados. Porém, se você já souber o ciclo de tempo esperado, fornecer uma dica de periodicidade poderá melhorar a exatidão do modelo. No entanto, se você fornecer a dica de periodicidade errada, poderá diminuir exatidão; portanto, se você não souber ao certo que valor deve ser usado, é melhor usar o padrão.  
  
 Por exemplo, a exibição usada neste modelo agrega dados de vendas de [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] mensalmente. Portanto, cada intervalo de tempo usado pelo modelo representa um mês, e todas as previsões também estarão em meses. Como há 12 meses em um ano e você espera que os padrões de vendas sejam mais ou menos repetidos anualmente, você definirá o parâmetro *PERIODICITY_HINT* como `12`, para indicar que 12 frações de tempo (meses) constituem um ciclo de vendas completo.  
  
 **Método de previsão**  
  
 O parâmetro *FORECAST_METHOD* controla se o algoritmo de série temporal é otimizado para previsões de curto ou longo prazo. Por padrão, o parâmetro *FORECAST_METHOD* é definido como Mixed, o que significa que dois algoritmos diferentes são mesclados e balanceados para fornecer bons resultados para previsão de curto e longo prazo.  
  
 Entretanto, se você quiser usar um algoritmo específico, poderá altera o valor para ARIMA ou ARTXP.  
  
 **Ponderação de previsões de longo prazo versus de curto prazo**  
  
 Você também pode personalizar a forma como as previsões de longo prazo e de curto prazo são combinadas usando o parâmetro PREDICTION_SMOOTHING. Por padrão, esse parâmetro é definido como 0,5, o que geralmente oferece o melhor equilíbrio para a precisão geral.  
  
#### <a name="to-change-the-algorithm-parameters"></a>Para alterar parâmetros do algoritmo  
  
1.  Na guia **modelos de mineração** , clique com o botão direito do mouse em **previsão**e selecione **definir parâmetros de algoritmo**.  
  
2.  Na `PERIODICITY_HINT` linha da caixa de diálogo **parâmetros do algoritmo** , clique na coluna **valor** e digite `{12}`, incluindo as chaves.  
  
     Por padrão, o algoritmo também adicionará o valor {1}.  
  
3.  Na `FORECAST_METHOD` linha, verifique se a caixa de texto **valor** está em branco ou definida como `MIXED`. Se um valor diferente tiver sido inserido, digite `MIXED` para alterar o parâmetro de volta para o valor padrão.  
  
4.  Na linha **PREDICTION_SMOOTHING** , verifique se a caixa de texto **valor** está em branco ou definida como 0,5. Se um valor diferente tiver sido inserido, clique em **valor** e `0.5` digite para alterar o parâmetro de volta para o valor padrão.  
  
    > [!NOTE]  
    >  O parâmetro PREDICTION_SMOOTHING só está disponível no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise. Dessa forma, não é possível exibir ou alterar o valor do parâmetro PREDICTION_SMOOTHING no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard. Porém, o comportamento padrão é usar os dois algoritmos e atribuir o mesmo valor a ambos.  
  
5.  Clique em **OK**.  
  
## <a name="handling-missing-data-optional"></a>Manipulando dados ausentes (opcional)  
 Na maioria dos casos, seus dados de venda poderão ter lacunas preenchidas por nulos, ou uma loja pode não ter conseguido cumprir o prazo da emissão de relatórios, deixando uma célula vazia no final da série. Nesses cenários, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] gera o erro a seguir e não processa o modelo.  
  
 "Erro (mineração de dados): carimbos de data/hora \<não sincronizados começando com o nome da série \<de séries>, do modelo de mineração,> de nome do modelo. Todas as séries temporais devem terminar na mesma marca de tempo e não podem ter pontos de dados ausentes arbitrariamente. A definição do parâmetro MISSING_VALUE_SUBSTITUTION como Previous ou como uma constante numérica corrigirá automaticamente pontos de dados ausentes, onde possível."  
  
 Para impedir esse erro, você pode especificar que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] forneça automaticamente novos valores para preencher as lacunas usando qualquer um dos métodos a seguir:  
  
-   Usando um valor médio. Essa média é calculada usando todos os valores válidos da mesma série de dados.  
  
-   Usando o valor anterior. Você pode substituir valores anteriores por várias células ausentes, mas não pode preencher os valores iniciais.  
  
-   Usando um valor constante fornecido por você.  
  
#### <a name="to-specify-that-gaps-be-filled-by-averaging-values"></a>Para especificar que as lacunas sejam preenchidas por valores médios  
  
1.  Na guia **modelos de mineração** , clique com o botão direito do mouse na coluna **previsão** e selecione **definir parâmetros de algoritmo**.  
  
2.  Na caixa de diálogo **parâmetros de algoritmo** , na linha **MISSING_VALUE_SUBSTITUTION** , clique na coluna **valor** e digite `Mean`.  
  
## <a name="build-the-model"></a>Criar o modelo  
 Para usar o modelo, você deve implantá-lo em um servidor e processar o modelo executando os dados de treinamento pelo algoritmo.  
  
#### <a name="to-process-the-forecasting-model"></a>Para processar o modelo de previsão  
  
1.  No menu **Modelo de Mineração** do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], selecione **Estrutura de Mineração do Processo e Todos os Modelos**.  
  
2.  No aviso que pergunta se você deseja construir e implantar o projeto, clique em **Sim**.  
  
3.  Na caixa de diálogo **processar estrutura de mineração – Previsão** , clique em **executar**.  
  
     A caixa de diálogo **Andamento do Processo** é aberta para exibir informações sobre o processamento do modelo. O processamento do modelo pode demorar algum tempo.  
  
4.  Depois que o processamento estiver completo, clique em **Fechar** para sair da caixa de diálogo **Progresso do Processo** .  
  
5.  Clique em **fechar** novamente para sair da caixa de diálogo **processar estrutura de mineração-Previsão** .  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Explorando o modelo de previsão &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/exploring-the-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Referência técnica do algoritmo do Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Algoritmo do Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Requisitos e considerações de processamento &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
