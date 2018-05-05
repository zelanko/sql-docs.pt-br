---
title: Habilitar o modo DirectQuery no SSDT | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 71fc7ebd-2e86-4a76-994b-66d3a57bcc9b
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8b8df527759c89579e5e6e73a703964eaed6d448
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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

Você pode criar uma partição de exemplo para cada tabela e adicionar dados de exemplo para verificar o comportamento do modelo ao criá-lo. Os dados de exemplo que você adicionar são usados em **Analisar para Excel** ou em outras ferramentas de cliente que podem se conectar ao banco de dados do espaço de trabalho. Consulte [Adicionar dados de exemplo a um modelo DirectQuery no modo de design](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md) para obter detalhes.  
  
> [!TIP]  
    >  Mesmo no modo DirectQuery em um modelo vazio, você sempre poderá exibir um pequeno conjunto de linhas interno para cada tabela. Em [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique em **Tabela** > **Propriedades da Tabela** para exibir o conjunto de dados de 50 linhas.  
  
  
## <a name="see-also"></a>Consulte também  
[Habilitar o modo DirectQuery no SSMS](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md)

[Adicionar dados de exemplo a um modelo DirectQuery no modo de design](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md)
  
