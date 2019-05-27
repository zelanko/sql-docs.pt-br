---
title: Especificar os dados de treinamento (Assistente de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.specifytrainingdata.f1
ms.assetid: cb04deeb-0f89-4bba-b3f1-efccada16825
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c3bbeb708cdb0c2882b85d55081446b3dc12b56b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66068072"
---
# <a name="specify-the-training-data-data-mining-wizard"></a>Especificar os dados de treinamento (Assistente de Mineração de Dados)
  Use a página **Especificar os Dados de Treinamento** para identificar quais as colunas a incluir na estrutura de mineração. Você pode selecionar colunas a serem incluídas na estrutura mesmo se não usá-las em todos os modelos. Por exemplo, para detalhar até as colunas a partir do modelo de mineração, você pode incluí-las na estrutura, mas não no modelo.  
  
 Pelo menos uma coluna de chave é obrigatória para cada tabela incluída na estrutura. A coluna escolhida como chave depende de a tabela ser a tabela de casos ou uma tabela aninhada. Se for uma tabela aninhada, a chave frequentemente também será a coluna previsível, não a chave estrangeira relacional. Para saber mais sobre chaves aninhadas, consulte [Tabelas aninhadas &#40;Analysis Services – Data Mining&#41;](data-mining/nested-tables-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Algoritmos de mineração diferentes usam as chaves de maneira diferente. Para saber mais sobre os tipos diferentes de chaves, consulte [Tipos de conteúdo &#40;Data Mining&#41;](data-mining/content-types-data-mining.md).  
  
 **Para obter mais informações:** [Estruturas de mineração &#40;Analysis Services - mineração de dados&#41;](data-mining/mining-structures-analysis-services-data-mining.md), [as colunas do modelo de mineração](data-mining/mining-model-columns.md), [Assistente de mineração de dados &#40;Analysis Services - mineração de dados&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md), [ Criar uma estrutura de mineração relacional](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>Opções  
 **Tabelas/colunas**  
 Exibe as tabelas e colunas que você selecionou na página anterior do assistente.  
  
 **\<caixa de seleção >**  
 Selecione as colunas a serem incluídas na estrutura de mineração.  
  
 Se sua fonte de dados incluir tabelas aninhadas ou várias exibições, expanda a lista de colunas para exibir as tabelas aninhadas.  
  
 **Chave**  
 Selecione para usar a coluna como um identificador exclusivo para os dados.  
  
 Em uma tabela de casos, a chave normalmente é o identificador exclusivo.  
  
 Na tabela aninhada, a **Chave** indica o identificador de uma linha no contexto do caso associado.  
  
 **Entrada**  
 Selecione para usar a coluna ao criar previsões.  
  
> [!NOTE]  
>  Essa coluna só estará disponível quando você estiver criando um modelo de mineração com a estrutura de mineração.  
  
 **Previsível**  
 Selecione para habilitar a tabela ou a coluna a ser prevista com base na entrada futura adicional.  
  
 Se você também marcar uma tabela aninhada como previsível, toda a tabela aninhada se tornará previsível. Se não houver colunas marcadas na tabela aninhada como de entrada ou previsível, a tabela aninhada será exibida na estrutura de mineração, mas será ignorada no modelo.  
  
 **Observação** Essa coluna só estará disponível quando você estiver criando um modelo de mineração com a estrutura de mineração.  
  
 **Sugerir**  
 Clique para abrir a caixa de diálogo **Sugerir Colunas Relacionadas** , que faz uma análise de uma amostra de dados para identificar colunas de entrada que mostram a relação maior com a coluna **Previsível** selecionada com base na entropia. Essa análise também se aplica a colunas de tabela aninhadas ou a estruturas de mineração baseadas em fontes OLAP.  
  
 **Observação** Essa coluna só estará disponível quando você estiver criando um modelo de mineração com a estrutura de mineração.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda F1 do Assistente de mineração de dados &#40;Analysis Services - mineração de dados&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Sugerir colunas relacionadas &#40;Assistente de mineração de dados&#41;](suggest-related-columns-data-mining-wizard.md)   
 [Especificar tipos de tabela &#40;Assistente de mineração de dados&#41;](specify-table-types-data-mining-wizard.md)   
 [Especificar conteúdo e o tipo de dados da coluna &#40;Assistente de mineração de dados&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
