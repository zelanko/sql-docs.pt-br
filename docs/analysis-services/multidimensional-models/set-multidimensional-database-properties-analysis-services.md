---
title: Definir propriedades de banco de dados Multidimensional (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- properties [Analysis Services], databases
ms.assetid: a8be5b3f-3148-448a-976c-7222705155d9
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6585737ac1f796b7e9e6e8834d6ca5b5c1c11612
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="set-multidimensional-database-properties-analysis-services"></a>Definir propriedades de banco de dados multidimensional (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Há uma série de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] propriedades que você pode configurar no banco de dados de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] designer de banco de dados.  
  
 Nesse criador, você pode executar os seguintes tipos de tarefas:  
  
-   Se você estiver conectado ao banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo online, você poderá alterar o nome do banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Se você estiver trabalhando no modo de projeto, você pode alterar o nome do banco de dados da próxima implantação do projeto. Para obter mais informações, consulte [Renomear um Banco de Dados Multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/rename-a-multidimensional-database-analysis-services.md) e [Configurar propriedades de projeto do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md).  
  
-   Você pode fornecer uma descrição do banco de dados que pode ser apresentada aos usuários. Você também pode exibir o nome do banco de dados, mas não pode alterá-lo. Para alterar o nome de banco de dados, você deve editar as propriedades do projeto.  
  
-   Você pode fornecer traduções para o nome do banco de dados e descrição para um ou mais idiomas. Para obter mais informações, consulte [Traduções de Cubo](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-translations.md), [Traduções da Dimensão](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)e [Suporte a tradução no Analysis Services](../../analysis-services/translation-support-in-analysis-services.md).  
  
-   Você pode exibir e pode modificar mapeamentos de tipo de conta padrão. Os mapeamentos de tipo da conta são usados quando uma ou mais medidas usarem a função de agregação *ByAccount* . Para cada tipo de conta, você pode especificar um alias e modificar a função de agregação padrão associada ao tipo de conta. Para obter mais informações sobre como modificar a agregação padrão, consulte [Definir comportamento semiaditivo](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md).  
  
## <a name="database-properties"></a>Propriedades de banco de dados  
 Além das propriedades acima, há várias propriedades de banco de dados que você pode configurar na janela Propriedades.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|Prefixo de agregação|O prefixo comum que pode ser usado para nomes de agregação para todas as partições em um banco de dados. Para obter mais informações, consulte [Elemento AggregationPrefix &#40;ASSL&#41;](../../analysis-services/scripting/properties/aggregationprefix-element-assl.md).|  
|Agrupamento|Quando o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é implantando em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , o banco de dados herda a propriedade do servidor de agrupamento a menos que um valor diferente seja fornecido aqui.|  
|Informações de representação da fonte de dados|Especifica o modo de representação padrão para todos os objetos da fonte de dados no banco de dados. Esse é o modo que o serviço [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa ao processar objetos, sincronizar servidores e executar as instruções de mineração de dados OpenQuery e SystemOpenSchema.|  
|Tamanho Estimado|Fornece um tamanho estimado dos arquivos de banco de dados no disco. Se os dados forem armazenados em vários locais, esta estimativa será limitada a apenas os arquivos de dados armazenados na pasta do banco de dados.<br /><br /> **EstimatedSize** também pode ser usado como base para estimar a memória. Geralmente, os requisitos de memória serão maiores que o tamanho dos dados em disco devido a estruturas de dados adicionais que são criadas quando o banco de dados é carregado na memória.<br /><br /> Para ampliar os requisitos de memória de estimativa, você também pode usar o Gerenciador de Tarefa para observar a memória do processo do Analysis Services antes e depois de processar o banco de dados e observar a memória utilizada como um método para entender os requisitos de memória do banco de dados.|  
|Linguagem|Quando o projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é implantando em uma instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , o banco de dados herda a propriedade do servidor de idioma a menos que um valor diferente seja fornecido aqui.|  
|ID do MasterDataSource|Usada com partições remotas. Para obter mais informações, consulte [Partições Remotas](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo Propriedades do Banco de Dados &#40;SSAS – Multidimensional&#41;](http://msdn.microsoft.com/library/70f000b7-917f-4699-b142-7a0d13ff767c)   
 [Configurar propriedades do projeto do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)  
  
  
