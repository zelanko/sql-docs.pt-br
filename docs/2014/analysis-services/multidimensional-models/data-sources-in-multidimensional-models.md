---
title: Fontes de dados em modelos multidimensionais | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- metadata [Analysis Services]
- Analysis Services objects, data sources
- storing data [Analysis Services], data sources
- data sources [Analysis Services], about data sources
- security [Analysis Services], data sources
- data sources [Analysis Services]
- storage [Analysis Services], data sources
ms.assetid: a16469d9-9d53-4e35-9982-fc06327a9d33
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fb84aceb83b3dfd0ac5e1e36d884b41df2850769
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009855"
---
# <a name="data-sources-in-multidimensional-models"></a>Fontes de dados em modelos multidimensionais
  Todos os dados que você importa ou carrega em um modelo multidimensional são originados de uma fonte de dados externa. Normalmente, os dados de origem são de um data warehouse criado para fins de geração de relatórios, mas poderiam vir de qualquer banco de dados relacional que seja acessado diretamente ou indiretamente por um intermediário, como um pacote do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Um objeto de **fonte de dados** no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especifica uma conexão direta com uma fonte de dados externa. Além do local físico, um objeto de fonte de dados especifica a cadeia de conexão, o provedor de dados, as credenciais e outras propriedades que controlam o comportamento da conexão.  
  
 As informações fornecidas pelo objeto de fonte de dados são usadas durante as seguintes operações:  
  
-   Obter informações de esquema e outros metadados usados para gerar exibições de fontes de dados em um modelo.  
  
-   Consultar ou carregar dados em um modelo durante o processamento.  
  
-   Executar as consultas em modelos multidimensionais ou de mineração de dados que usam o modo de armazenamento ROLAP  
  
-   Ler ou gravar em partições remotas.  
  
-   Conectar a objetos vinculados, assim como sincronizar do destino para a origem.  
  
-   Executar operações de write-back que atualizam dados de tabela de fatos armazenadas em um banco de dados relacional.  
  
 Ao construir um modelo multidimensional debaixo pra cima, você inicia criando o objeto de fonte de dados e, em seguida, usa-o para gerar o próximo objeto, uma **exibição da fonte de dados**. Uma exibição da fonte de dados é a camada de abstração de dados no modelo. Ela é criada normalmente depois do objeto de fonte de dados, usando o esquema do banco de dados de origem como a base. No entanto, você pode escolher outros modos de criar um modelo, inclusive iniciar com cubos e dimensões, e gerando o esquema que melhor dê suporte ao seu design.  
  
 Independentemente de como você crie isto, cada modelo exige pelo menos um objeto de fonte de dados que especifica uma conexão com os dados de origem. Você pode criar vários objetos de fonte de dados em um único modelo para usar dados de origens diferentes ou variar as propriedades de conexão para objetos específicos.  
  
 Os objetos de fonte de dados podem ser gerenciados independentemente de outros objetos em seu modelo. Depois que você criar uma fonte de dados, pode alterar suas propriedades posteriormente e, em seguida, pré-processar o modelo para assegurar que os dados sejam recuperados corretamente.  
  
## <a name="related-topics-and-tasks"></a>Tópicos relacionados e tarefas  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Fontes de dados suportadas &#40;Multidimensional do SSAS&#41;](supported-data-sources-ssas-multidimensional.md)|Descreve os tipos de fonte de dados que podem ser usados em um modelo multidimensional.|  
|[Criar uma fonte de dados &#40;Multidimensional do SSAS&#41;](create-a-data-source-ssas-multidimensional.md)|Explica como adicionar um objeto de fonte de dados a um modelo multidimensional.|  
|[Excluir uma fonte de dados no Gerenciador de soluções &#40;Multidimensional do SSAS&#41;](delete-a-data-source-in-solution-explorer-ssas-multidimensional.md)|Use este procedimento para excluir um objeto de fonte de dados de um modelo multidimensional.|  
|[Definir propriedades de fonte de dados &#40;Multidimensional do SSAS&#41;](set-data-source-properties-ssas-multidimensional.md)|Descreve cada propriedade e explica como definir cada uma.|  
|[Definir opções de representação &#40;SSAS - Multidimensional&#41;](set-impersonation-options-ssas-multidimensional.md)|Explica como configurar as opções na caixa de diálogo de Informações sobre Representação.|  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de banco de dados &#40; Analysis Services - dados multidimensionais &#41;](olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [Arquitetura lógica &#40; Analysis Services - dados multidimensionais &#41;](olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Exibições da fonte de dados em modelos multidimensionais](data-source-views-in-multidimensional-models.md)   
 [Fontes de dados e associações &#40;Multidimensional do SSAS&#41;](data-sources-and-bindings-ssas-multidimensional.md)  
  
  