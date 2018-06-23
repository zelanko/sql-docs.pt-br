---
title: Do Analysis Services preteridos recursos do SQL Server 2014 | Microsoft Docs
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
- Analysis Services, backward compatibility
- SSAS, backward compatibility
- SQL Server Analysis Services, backward compatibility
- deprecated features [Analysis Services]
ms.assetid: 2c96ecfe-a170-41d0-bee3-74503f880197
caps.latest.revision: 48
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 49a65a9ca1684a7bcec7b5f7f1d19d38b01f13d0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010551"
---
# <a name="deprecated-analysis-services-features-in-sql-server-2014"></a>Recursos do Analysis Services preteridos no SQL Server 2014
  Este tópico descreve os recursos substituídos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que ainda estão disponíveis no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Esses recursos estão programados para serem removidos em uma versão futura do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Recursos preteridos não devem ser usados em aplicativos novos.  
  
## <a name="features-not-supported-in-the-next-version-of-sql-server"></a>Recursos sem suporte na próxima versão do SQL Server  
 Os recursos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a seguir não terão suporte na próxima versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Não use esses recursos em novo trabalho de desenvolvimento e, assim que possível, modifique os aplicativos que os utilizam atualmente.  
  
|Categoria|Recurso substituído|Substituição|  
|--------------|------------------------|-----------------|  
|Função MDX|Função CalculationPassValue|Nenhum. O mecanismo OLAP gerencia a fase de cálculo. Essa função não é mais necessária.|  
|Função MDX|Função CalculationCurrentPass|Nenhum. O mecanismo OLAP gerencia a fase de cálculo. Essa função não é mais necessária.|  
|Linguagem MDX|A dica do otimizador de consulta NON_EMPTY_BEHAVIOR foi ativada por padrão.|A dica do otimizador de consulta NON_EMPTY_BEHAVIOR será desativada por padrão em uma versão futura. É uma dica de otimização MDX que pode gerar resultados incorretos quando não usada corretamente.|  
|Outro|Propriedade de célula intrínseca CELL_EVALUATION_LIST|Originalmente fornecia uma lista de fórmulas avaliadas que se aplicam a uma célula. Está em branco nesta versão do Analysis Services.  A ordem de resolução agora é especificada no script MDX. Para obter mais informações, consulte [Noções básicas sobre ordem de passar e ordem de resolução &#40;MDX&#41;](multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md)|  
|Objetos|Assemblies COM|Os assemblies COM podem representar um risco à segurança. O suporte a assemblies COM será removido em uma versão futura.|  
  
## <a name="features-not-supported-in-a-future-version-of-sql-server"></a>Recursos sem suporte em uma versão futura do SQL Server  
 Os recursos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a seguir terão suporte na próxima versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], mas serão removidos em uma versão posterior. A versão específica do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não foi determinada.  
  
|Categoria|Recurso substituído|Substituição|  
|--------------|------------------------|-----------------|  
|Modelos multidimensionais|Partições remotas|Nenhum. Use partições locais. Consulte [criar e gerenciar uma partição Local &#40;Analysis Services&#41; ](multidimensional-models/create-and-manage-a-local-partition-analysis-services.md) para obter mais informações.|  
|Modelos multidimensionais|Grupos de medidas vinculados remotos|Um grupo de medidas vinculado remoto é um grupo de medidas vinculado que usa uma fonte de dados em um servidor remoto. A capacidade de usar uma fonte de dados remotos para um grupo de medidas vinculado está agendada para substituição.<br /><br /> Não há substituição para esse recurso. Recomendamos usar grupos de medidas vinculados locais nesse caso. Consulte [grupos de medidas vinculados](multidimensional-models/linked-measure-groups.md) para obter mais informações.|  
|Modelos multidimensionais|Write-back dimensional|Nenhum. Use o write-back de partição se você precisar do recurso de write-back. Consulte [Set Partition Writeback](multidimensional-models/set-partition-writeback.md) para obter mais informações.|  
|Modelos multidimensionais|Dimensões vinculadas|Nenhum. Considere copiar dimensões para modelos adicionais, em vez de vincular a uma dimensão em outro modelo.|  
|MDX|Propriedade Non_Empty_Behavior|Nenhum. Ao criar um membro calculado, definir essa propriedade de forma incorreta aumenta a probabilidade de retorno de resultados inválidos. Otimizações recentes para o mecanismo OLAP melhoraram operações em conjuntos de dados esparsos, tornando essa propriedade menos relevante.|  
  
## <a name="see-also"></a>Consulte também  
 [Compatibilidade com versões anteriores do Analysis Services](analysis-services-backward-compatibility.md)   
 [Funcionalidade descontinuada do Analysis Services no SQL Server 2014](discontinued-analysis-services-functionality-in-sql-server-2014.md)  
  
  