---
title: Especificando um conjunto de dados de teste para a estrutura (Tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 75cd508f-b126-418b-848d-3c4c3e6c303f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 21eaa86fb1ff594e8b9d2b779b787276ee13ab4b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62720103"
---
# <a name="specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial"></a>Especificando um conjunto de dados de teste para a estrutura (Tutorial de mineração de dados básico)
  Nas últimas telas do Assistente de Mineração de Dados, você dividirá seus dados entre um conjunto de teste e um conjunto de treinamento. Em seguida, dará um nome à sua estrutura e habilitará o detalhamento do modelo.  
  
## <a name="specifying-a-testing-set"></a>Especificando um conjunto de teste  
 A separação dos dados em conjuntos de treinamento e de teste na criação de uma estrutura de mineração possibilita a avaliação fácil da precisão dos modelos de mineração criados posteriormente. Para obter mais informações sobre conjuntos de teste, consulte [conjuntos de dados de teste e treinamento](../../2014/analysis-services/data-mining/training-and-testing-data-sets.md).  
  
#### <a name="to-specify-the-testing-set"></a>Para especificar o conjunto de teste  
  
1.  Sobre o **criar conjunto de testes** página, para **porcentagem de dados de teste**, deixe o valor padrão de `30`.  
  
2.  Para **o número máximo de casos no conjunto de dados de teste**, tipo `1000`.  
  
3.  Clique em **Avançar**.  
  
## <a name="specifying-drillthrough"></a>Especificando o detalhamento  
 O detalhamento pode ser habilitado em modelos e em estruturas. A caixa de seleção nesta caixa de diálogo permite o detalhamento no modelo nomeado. Depois que o modelo tiver sido processado, você poderá recuperar as informações detalhadas dos dados de treinamento que foram usados para criar o modelo.  
  
 Se a estrutura de mineração subjacente também estiver configurada para permitir o detalhamento, você poderá recuperar informações detalhadas dos casos de modelo e da estrutura de mineração, inclusive colunas que não foram incluídas no modelo de mineração. Para obter mais informações, consulte [Consultas de detalhamento &#40;Mineração de dados&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
#### <a name="to-name-the-model-and-structure-and-specify-drillthrough"></a>Para nomear o modelo e a estrutura e especificar o detalhamento  
  
1.  Sobre o **Concluindo o assistente** página, na **nome da estrutura de mineração**, tipo `Targeted Mailing`.  
  
2.  Na **nome do modelo de mineração**, tipo `TM_Decision_Tree`.  
  
3.  Selecione o **permitir detalhamento** caixa de seleção.  
  
4.  Examine os **visualização** painel. Observe que somente as colunas selecionadas, como **chave**, **entrada** ou **previsível** são mostrados. As outras colunas selecionadas (como AddressLine1, por exemplo) não são usadas para a criação do modelo, mas estarão disponíveis na estrutura subjacente e podem ser consultadas após o processamento e a implantação do modelo.  
  
5.  Clique em **Concluir**.  
  
## <a name="previous-task-in-lesson"></a>Tarefa anterior da lição  
 [Especificando o tipo de dados e o tipo de conteúdo &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/specifying-the-data-type-and-content-type-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 3: Adicionando e processando modelos](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
  
## <a name="see-also"></a>Consulte também  
 [Habilitar o detalhamento para um modelo de mineração](../../2014/analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)   
 [Consultas de detalhamento &#40;Mineração de dados&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)   
 [Especificar os dados de treinamento &#40;Assistente de mineração de dados&#41;](../../2014/analysis-services/specify-the-training-data-data-mining-wizard.md)  
  
  
