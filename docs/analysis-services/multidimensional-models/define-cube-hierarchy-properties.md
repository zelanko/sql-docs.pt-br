---
title: Definir propriedades de hierarquia de cubo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9632719018cf91eebc97b7a56e651bdc3037e5a3
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="define-cube-hierarchy-properties"></a>Definir propriedades de hierarquia de cubo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  As propriedades de hierarquia de cubo permitem a especificação de configurações exclusivas para hierarquias definidas pelo usuário em dimensões de cubo com base na mesma dimensão do banco de dados. A tabela a seguir descreve as propriedades de uma hierarquia de cubo.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|**Enabled**|Determina se a hierarquia está habilitada para a dimensão de cubo.|  
|**HierarchyID**|Contém o identificador exclusivo (ID) da hierarquia.|  
|**OptimizedState**|Determina o nível de otimização aplicado à hierarquia. Essa propriedade pode ter os seguintes valores:<br /><br /> **FullyOptimized**:<br />                    A instância cria índices para a hierarquia a fim de melhorar o desempenho das consultas. Este é o valor padrão.<br /><br /> **NotOptimized**:<br />                    A instância não cria índices adicionais.|  
|**Visível**|Determina a visibilidade da hierarquia de cubo. O valor padrão é **True**.|  
  
## <a name="see-also"></a>Consulte também  
 [Hierarquias de usuário](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
