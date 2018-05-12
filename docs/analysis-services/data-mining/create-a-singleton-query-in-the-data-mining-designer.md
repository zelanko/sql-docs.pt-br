---
title: Criar uma consulta Singleton no Designer de mineração de dados | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d30fee91882ecd2f76fde1e0c61d0e5bc3d302bc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="create-a-singleton-query-in-the-data-mining-designer"></a>Criar uma consulta Singleton no Designer de Mineração de Dados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Uma consulta singleton será útil se você quiser criar uma previsão para um único caso. Para obter mais informações sobre as consultas singleton, veja [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md).  
  
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
  
     Por exemplo, selecione **2** para **Número de Crianças em Casa**e, em seguida, digite **45** para **Idade**.  
  
5.  Arraste uma coluna previsível da tabela **Modelo de Mineração** para a coluna **Origem** na parte inferior da guia. Opcionalmente, você pode digitar um alias para a coluna.  
  
     Por exemplo, arraste **Comprador de Bicicleta** para a coluna **Origem** .  
  
6.  Adicione qualquer função extra à consulta, selecionando **Função de Previsão** ou **Expressão Personalizada** na lista suspensa na coluna **Origem** .  
  
     Por exemplo, clique em **Função de Previsão**e selecione **PredictProbability**.  
  
7.  Clique em **Critérios/Argumento** na linha **PredictProbability** e digite o nome da coluna para previsão e, como opção, um valor específico para previsão.  
  
     Por exemplo, digite **[Bike Buyer], 1**.  
  
8.  Clique na caixa **Alias** na linha **PredictProbability** e digite um nome para fazer referência à coluna nova.  
  
     Por exemplo, digite **ProbableBuyer**.  
  
9. Clique em **Alternar para a exibição do resultado da consulta** na barra de ferramentas da guia **Previsão do Modelo de Mineração** .  
  
     Uma tela nova se abre para mostrar o resultado da consulta. Para exibir a instrução DMX que você acabou de criar, clique em **SQL**.  
  
## <a name="see-also"></a>Consulte também  
 [Consultas de previsão & #40; mineração de dados & #41;](../../analysis-services/data-mining/prediction-queries-data-mining.md)  
  
  
