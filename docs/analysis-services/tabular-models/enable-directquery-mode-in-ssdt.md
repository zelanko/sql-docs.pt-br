---
title: Habilitar o modo DirectQuery do Analysis Services no SSDT | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 83fa1cf8d99f18cd82e00b4020a2d846b1bdfdc6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162886"
---
# <a name="enable-directquery-mode-in-ssdt"></a>Habilitar o modo DirectQuery no SSDT
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Neste tópico, descreveremos como habilitar o modo DirectQuery para um projeto de modelo de tabela no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
Quando você habilita o modo DirectQuery para um modelo de tabela que está criando no SSDT:
-   Recursos incompatíveis com o modo DirectQuery são desabilitados.  
-   O modelo existente é validado. Avisos são exibidos se os recursos são incompatíveis com o modo DirectQuery.  
-   Se os dados foram importados anteriormente antes de habilitar o modo DirectQuery, o cache do modelo de trabalho é esvaziado.  
  
### <a name="enable-directquery"></a>Habilitar o DirectQuery  
  
No SSDT, no painel **Propriedades** para o arquivo **Model.bim** file, altere a propriedade **modo DirectQuery**para **Ativo**.  

![Habilitar o modo DirectQuery no SSDT](../../analysis-services/tabular-models/media/enable-directquery-mode-in-ssdt.png)
  
Se o modelo já tiver uma conexão a uma fonte de dados e os dados existentes, será solicitado que você insira as credenciais do banco de dados usadas para se conectar ao banco de dados relacional. Todos os dados já existentes no modelo serão removidos do cache na memória.  
  
Se o seu modelo for parcialmente ou totalmente concluído antes de habilitar o modo DirectQuery, você poderá receber erros sobre recursos incompatíveis. No Visual Studio, abra a **Lista de Erros** e resolva todos os problemas que possam impedir a alternância do modelo para o modo DirectQuery.  


### <a name="whats-next"></a>O que vem a seguir? 
Agora, você pode importar dados usando o Assistente de Importação de Tabela para obter metadados para o modelo. Você não obterá linhas de dados, mas receberá tabelas, colunas e relações para usar como base para seu modelo. 

Você pode criar uma partição de exemplo para cada tabela e adicionar dados de exemplo para verificar o comportamento do modelo ao criá-lo. Os dados de exemplo que você adicionar são usados em **Analisar para Excel** ou em outras ferramentas de cliente que podem se conectar ao banco de dados do workspace. Consulte [Adicionar dados de exemplo a um modelo DirectQuery no modo de design](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md) para obter detalhes.  
  
> [!TIP]
>  Mesmo no modo DirectQuery em um modelo vazio, você sempre poderá exibir um pequeno conjunto de linhas interno para cada tabela. Em [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique em **Tabela** > **Propriedades da Tabela** para exibir o conjunto de dados de 50 linhas.  
  
  
## <a name="see-also"></a>Confira também  
[Habilitar o modo DirectQuery no SSMS](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md)

[Adicionar dados de exemplo a um modelo DirectQuery no modo de design](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md)
  
