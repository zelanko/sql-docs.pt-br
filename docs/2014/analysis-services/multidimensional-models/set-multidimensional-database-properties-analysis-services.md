---
title: Definir propriedades do banco de dados multidimensional (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- properties [Analysis Services], databases
ms.assetid: a8be5b3f-3148-448a-976c-7222705155d9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aa3e1544f625183df3240359aa22b117144244d3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66072998"
---
# <a name="set-multidimensional-database-properties-analysis-services"></a>Definir propriedades de banco de dados multidimensional (Analysis Services)
  Há várias propriedades de banco [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de dados que você pode configurar no designer [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] de banco de dados.  
  
 Nesse criador, você pode executar os seguintes tipos de tarefas:  
  
-   Se você estiver conectado ao banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo online, você poderá alterar o nome do banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Se você estiver trabalhando no modo de projeto, você pode alterar o nome do banco de dados da próxima implantação do projeto. Para obter mais informações, consulte [Renomear um Banco de Dados Multidimensional &#40;Analysis Services&#41;](rename-a-multidimensional-database-analysis-services.md) e [Configurar propriedades de projeto do Analysis Services &#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md).  
  
-   Você pode fornecer uma descrição do banco de dados que pode ser apresentada aos usuários. Você também pode exibir o nome do banco de dados, mas não pode alterá-lo. Para alterar o nome de banco de dados, você deve editar as propriedades do projeto.  
  
-   Você pode fornecer traduções para o nome do banco de dados e descrição para um ou mais idiomas. Para obter mais informações, consulte traduções de [cubos](../multidimensional-models-olap-logical-cube-objects/cube-translations.md), [traduções de dimensão](../multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)e [traduções &#40;Analysis Services&#41;](../translations-analysis-services.md).  
  
-   Você pode exibir e pode modificar mapeamentos de tipo de conta padrão. Os mapeamentos de tipo da conta são usados quando uma ou mais medidas usarem a função de agregação *ByAccount* . Para cada tipo de conta, você pode especificar um alias e modificar a função de agregação padrão associada ao tipo de conta. Para obter mais informações sobre como modificar a agregação padrão, consulte [Definir comportamento semiaditivo](define-semiadditive-behavior.md).  
  
## <a name="database-properties"></a>Propriedades de banco de dados  
 Além das propriedades acima, há várias propriedades de banco de dados que você pode configurar na janela Propriedades.  
  
|Propriedade|DESCRIÇÃO|  
|--------------|-----------------|  
|Prefixo de agregação|O prefixo comum que pode ser usado para nomes de agregação para todas as partições em um banco de dados. Para obter mais informações, consulte [Elemento AggregationPrefix &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/aggregationprefix-element-assl).|  
|Collation|Quando o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é implantando em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o banco de dados herda a propriedade do servidor de ordenação a menos que um valor diferente seja fornecido aqui.|  
|Informações de representação da fonte de dados|Especifica o modo de representação padrão para todos os objetos da fonte de dados no banco de dados. Esse é o modo que o serviço [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa ao processar objetos, sincronizar servidores e executar as instruções de mineração de dados OpenQuery e SystemOpenSchema.|  
|Tamanho Estimado|Fornece um tamanho estimado dos arquivos de banco de dados no disco. Se os dados forem armazenados em vários locais, esta estimativa será limitada a apenas os arquivos de dados armazenados na pasta do banco de dados.<br /><br /> 
  `EstimatedSize` também pode ser usado como base para estimar memória. Geralmente, os requisitos de memória serão maiores que o tamanho dos dados em disco devido a estruturas de dados adicionais que são criadas quando o banco de dados é carregado na memória.<br /><br /> Para ampliar os requisitos de memória de estimativa, você também pode usar o Gerenciador de Tarefa para observar a memória do processo do Analysis Services antes e depois de processar o banco de dados e observar a memória utilizada como um método para entender os requisitos de memória do banco de dados.|  
|Linguagem|Quando o projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é implantando em uma instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , o banco de dados herda a propriedade do servidor de idioma a menos que um valor diferente seja fornecido aqui.|  
|ID do MasterDataSource|Usada com partições remotas. Para obter mais informações, consulte [Partições Remotas](../multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo Propriedades do banco de dados &#40;SSAS –&#41;multidimensional](../database-properties-dialog-box-ssas-multidimensional.md)   
 [Configurar propriedades do projeto de Analysis Services &#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md)  
  
  
