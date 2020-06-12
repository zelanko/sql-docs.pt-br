---
title: Criar conjunto de testes (Assistente de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.holdout.f1
ms.assetid: d0a44b59-ffbd-45fc-baa8-6b8046b1a2f5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 84dd9e307279c83b955d6569571772414123f0f5
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84526446"
---
# <a name="create-testing-set-data-mining-wizard"></a>Criar Conjunto de Testes (Assistente de Mineração de Dados)
  Use a página **Criar Conjunto de Testes** para especificar a quantidade de dados que precisa ser usada para treinamento e a quantidade que precisa ser reservada para uso como um conjunto de testes. Separando os dados em um conjunto de treinamento e outro de teste ao criar uma estrutura de mineração, você facilita a avaliação da precisão dos modelos de mineração que criar depois.  
  
 Você pode especificar a quantidade de dados de teste em porcentagem ou indicar um número para limitar o número de casos usados para teste. Se forem especificados tanto uma porcentagem como um número de casos a serem usados para teste, as duas configurações serão usadas e o conjunto de dados de teste conterá o menor número de casos. Por padrão, 30% dos dados são usados para teste, 70% para treinamento e não há um número máximo de casos de teste.  
  
 Por padrão, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] gera uma semente numérica usada para iniciar o particionamento. Essa semente é baseada no nome da estrutura de mineração. Para garantir que a partição permaneça igual mesmo que o nome da estrutura de mineração seja alterada, você pode especificar um valor para a semente, definindo a propriedade HoldoutSeed da estrutura de mineração. Se você alterar a semente de validação, deverá reprocessar a estrutura.  
  
 Se posteriormente você quiser alterar a quantidade de dados de teste ou treinamento, poderá modificar as `HoldoutMaxCases` Propriedades e `HoldoutMaxPercent` na estrutura de Data Mining usando a janela **Propriedades** . Porém, depois de alterar, você deve reprocessar a estrutura de mineração e todos os modelos de mineração associados. As seguintes limitações também se aplicam:  
  
-   O particionamento de uma estrutura de mineração de dados só tem suporte quando a estrutura de mineração de dados é armazenada no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. As versões anteriores do não [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dão suporte ao cache de informações de partição para estruturas de mineração.  
  
-   Você não pode particionar uma estrutura de mineração se esta contiver uma coluna Key Time, que é obrigatória para modelos de mineração de série temporal.  
  
-   Você não pode particionar dados se estiver tentando prever um valor armazenado em uma tabela aninhada.  
  
 **Para obter mais informações:** [Teste e validação &#40;Data Mining&#41;](data-mining/testing-and-validation-data-mining.md), [Criar uma estrutura de mineração relacional](data-mining/create-a-relational-mining-structure.md), [Tutorial básico de Data Mining](../../2014/tutorials/basic-data-mining-tutorial.md)  
  
## <a name="options"></a>Opções  
 **Percentual de dados para teste**  
 Clique nas setas para cima e para baixo para aumentar ou diminuir a porcentagem de dados a serem usados como um conjunto de treinamento. Se preferir, digite um valor entre 0 e 100 na caixa de texto.  
  
 **Número máximo de casos no conjunto de dados de teste**  
 Digite um número para limitar o número de casos que podem ser usados para teste.  
  
 Se for especificado um número maior que o de casos reais nos dados, todos os casos serão usados.  
  
 O padrão é NULO. Isso significa não há nenhum limite.  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuda F1 do assistente de mineração de dados &#40;Analysis Services Data Mining&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Sugerir colunas relacionadas &#40;assistente de mineração de dados&#41;](suggest-related-columns-data-mining-wizard.md)   
 [Especificar tipos de tabela &#40;assistente de mineração de dados&#41;](specify-table-types-data-mining-wizard.md)   
 [Especifique o tipo de conteúdo e de dados da coluna &#40;assistente de mineração de dados&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
