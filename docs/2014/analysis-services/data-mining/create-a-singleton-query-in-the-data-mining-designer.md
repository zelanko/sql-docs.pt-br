---
title: Criar uma consulta Singleton no Designer de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- singleton queries [Analysis Services]
- Mining Model Prediction [Analysis Services], singleton queries
ms.assetid: 6cdca8a0-cf16-46eb-a652-0bff820625ab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 795347e0ef2bdee226daff57e85e2b02f8b00c9e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085305"
---
# <a name="create-a-singleton-query-in-the-data-mining-designer"></a>Criar uma consulta Singleton no Designer de Mineração de Dados
  Uma consulta singleton será útil se você quiser criar uma previsão para um único caso. Para obter mais informações sobre as consultas singleton, veja [Consultas de mineração de dados](data-mining-queries.md).  
  
 Na guia **Previsão do Modelo de Mineração** do Designer de Mineração de Dados, você pode criar vários tipos diferentes de consultas. Você pode criar uma consulta usando o designer ou digitando instruções DMX  (Extensões de Mineração de Dados). Você também pode começar com o designer e modificar a consulta que ele cria alterando as instruções DMX ou adicionando uma cláusula WHERE ou ORDER BY.  
  
 Para trocar entre a exibição de design de consulta e a exibição de texto de consulta, clique no primeiro botão na barra de ferramentas. Quando você está na exibição de texto de consulta, pode exibir o código DMX criado pelo Construtor de Consultas de Previsão. Você também pode executar a consulta, modificar a consulta e executar a consulta modificada. Porém, a consulta modificada não será mantida se você retornar à exibição de design de consulta.  
  
 O código seguinte mostra um exemplo de uma consulta singleton em relação ao modelo de correspondência destinada, TM_Decision_Tree.  
  
```  
SELECT [Bike Buyer], PredictProbability([Bike Buyer]) as ProbableBuyer  
FROM [TM_Decision_Tree]  
NATURAL PREDICTION JOIN  
(SELECT '2' AS [Number Children At Home], '45' as [Age])  
AS [t]  
```  
  
 As etapas a seguir explicam como criar essa consulta de previsão.  
  
### <a name="to-create-a-singleton-query-by-using-the-data-mining-designer"></a>Para criar uma consulta singleton utilizando o Designer de Mineração de Dados  
  
1.  Clique na guia **Previsão do Modelo de Mineração** do Designer de Mineração de Dados.  
  
2.  Clique em **Selecionar Modelo** na tabela **Modelo de Mineração** .  
  
     A caixa de diálogo **Selecionar Modelo de Mineração** é aberta e mostra todas as estruturas de mineração existentes no projeto atual.  
  
     Selecione o modelo que deseja usar para criar a previsão.  
  
     Por exemplo, para criar o código de amostra mostrado no início deste tópico, selecione TM_Decision_Tree e, em seguida, clique em **OK**.  
  
3.  Clique em **Consulta Singleton** na barra de ferramentas da guia **Previsão do Modelo de Mineração** .  
  
     A tabela **Entrada da Consulta Singleton** é exibida na guia, com as colunas mapeadas automaticamente para as colunas na tabela **Modelo de Mineração** .  
  
4.  Na tabela **Entrada da Consulta Singleton** , selecione os valores na coluna **Valor** para descrever o caso para o qual deseja criar uma previsão.  
  
     Por exemplo, selecione **2** para **número de crianças em casa**e, em seguida, digite `45` para **idade**.  
  
5.  Arraste uma coluna previsível da tabela **Modelo de Mineração** para a coluna **Origem** na parte inferior da guia. Opcionalmente, você pode digitar um alias para a coluna.  
  
     Por exemplo, arraste **Comprador de Bicicleta** para a coluna **Origem** .  
  
6.  Adicione qualquer função extra à consulta, selecionando **Função de Previsão** ou **Expressão Personalizada** na lista suspensa na coluna **Origem** .  
  
     Por exemplo, clique em **Função de Previsão**e selecione **PredictProbability**.  
  
7.  Clique em **Critérios/Argumento** na linha **PredictProbability** e digite o nome da coluna para previsão e, como opção, um valor específico para previsão.  
  
     Por exemplo, digite `[Bike Buyer], 1`.  
  
8.  Clique na caixa **Alias** na linha **PredictProbability** e digite um nome para fazer referência à coluna nova.  
  
     Por exemplo, digite `ProbableBuyer`.  
  
9. Clique em **Alternar para a exibição do resultado da consulta** na barra de ferramentas da guia **Previsão do Modelo de Mineração** .  
  
     Uma tela nova se abre para mostrar o resultado da consulta. Para exibir a instrução DMX que você acabou de criar, clique em **SQL**.  
  
## <a name="see-also"></a>Consulte também  
 [Consultas de previsão &#40;Mineração de dados&#41;](prediction-queries-data-mining.md)  
  
  
