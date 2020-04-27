---
title: Especificar o tipo de conteúdo e de dados da coluna (Assistente de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0634be64-4c38-4381-9b19-fe9a5889306c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d224a321ed78f89a798966bd28c0ff7f16d55134
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66068465"
---
# <a name="specify-column-content-and-data-type-data-mining-wizard"></a>Especificar tipo de conteúdo e de dados da coluna (Assistente de Mineração de Dados)
  Use a página **Especificar Tipo de Conteúdo e de Dados da Coluna** para especificar o uso e o tipo de dados de cada coluna selecionada na página anterior do assistente. Se desejar ignorar a coluna, clique em **Voltar** para voltar à página **Especificar os Dados de Treinamento**e desmarque todas as caixas de seleção.  
  
 O uso de uma coluna indica como os dados serão usados no modelo. Uma coluna pode ser usada como chave para identificar uma série, como um valor de entrada a ser usado na análise ou como o valor que você deseja prever. As colunas podem ser usadas tanto para previsão como para entrada.  
  
 O tipo de dados especifica detalhes adicionais sobre o tipo de dados contidos na coluna e como eles serão usados durante o treinamento. Alguns tipos de conteúdo requerem um tipo de dados específico e vice-versa. Você também pode precisar especificar um tipo de dados específico, dependendo do algoritmo usado ao criar um modelo de mineração. Para obter informações sobre tipos de conteúdo e de dados em modelos e estruturas de mineração, consulte [Tipos de conteúdo &#40;Mineração de dados&#41;](data-mining/content-types-data-mining.md).  
  
 **Para obter mais informações:** [Estruturas de mineração &#40;Analysis Services – Mineração de dados&#41;](data-mining/mining-structures-analysis-services-data-mining.md), [Colunas do modelo de mineração](data-mining/mining-model-columns.md), [Assistente de Mineração de dados &#40;Analysis Services – Mineração de dados&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md) e [Criar uma estrutura de mineração relacional](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>Opções  
 **Estrutura do modelo de mineração**  
 Exibe as colunas das exibições e tabelas aninhadas que você selecionou na página anterior do assistente.  
  
 **Colunas**  
 Lista as colunas.  
  
 **Tipo de conteúdo**  
 Especifique o tipo de conteúdo da coluna Se você especificou que a coluna é uma chave na página anterior do assistente, os seguintes valores estarão disponíveis:  
  
|Opção|Descrição|  
|------------|-----------------|  
|Chave|Especifique que a coluna contém um identificador exclusivo para a série de casos.|  
|Key Sequence|Especifique que a coluna contém um identificador de sequência.|  
|Key Time|Especifique que a coluna contém uma data ou outro número contínuo exclusivo que é usado para identificar uma série de datas ou horários.|  
  
 Se você selecionou a coluna como uma coluna que não seja uma coluna de chave, os valores seguintes estarão disponíveis, dependendo do tipo de dados:  
  
|Opção|Descrição|  
|------------|-----------------|  
|Contínuo|Especifique que a coluna contém valores numéricos contínuos.|  
|Discretizado|Especifique que a coluna contém valores numéricos que foram tornados discretos ou podem ser tratados como valores discretos.|  
|Discreto|Especifique que a coluna contém valores de texto ou outros valores não numéricos.|  
  
 **Tipo de dados**  
 Especifique o tipo de dados da coluna.  
  
 Os seguintes valores estão disponíveis:  
  
-   `Boolean`  
  
-   `Date`  
  
-   `Double`  
  
-   `Long`  
  
-   `Text`  
  
 **Detect**  
 Analise uma amostra de dados em todas as colunas numéricas. Substitui valores de **Tipo de conteúdo** especificados por um tipo de conteúdo recomendado.  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuda F1 do assistente de mineração de dados &#40;Analysis Services Data Mining&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Sugerir colunas relacionadas &#40;assistente de mineração de dados&#41;](suggest-related-columns-data-mining-wizard.md)   
 [Especificar tipos de tabela &#40;assistente de mineração de dados&#41;](specify-table-types-data-mining-wizard.md)   
 [Especifique o tipo de conteúdo e de dados da coluna &#40;assistente de mineração de dados&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
