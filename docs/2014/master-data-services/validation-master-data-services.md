---
title: Validação (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 98eb49e7-b190-4a21-8316-08c07cde14ed
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 78433a93f4b9ce60393f6cdf9c8c128ec5011387
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65481320"
---
# <a name="validation-master-data-services"></a>Validação (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], os dados são validados para garantir sua exatidão. Alguma validação ocorre automaticamente e outra validação é baseada em regras de negócio que são criadas por administradores.  
  
## <a name="when-data-validation-occurs"></a>Quando ocorre a validação de dados  
 A validação ocorre em momentos diferentes e é exibida de maneira diferente no aplicativo Web do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
|Tipo de validação|Padrões determinados por|Quando ocorre|Exibido na interface de usuário na Web do MasterData Manager como|Exibido no suplemento para Excel como|Os dados são salvos no repositório do MDS?|  
|---------------------|-----------------------------|--------------------|---------------------------------------------------|-------------------------------------------|------------------------------------------|  
|Validação da regra de negócios|Um administrador do MDS|Automaticamente quando um usuário adiciona ou edita dados.<br /><br /> Manualmente quando um usuário aplica regras de negócio.<br /><br /> Manualmente quando um administrador na área funcional de **Gerenciamento de Versões** do aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] valida uma versão em relação às regras de negócio.|Erros de validação|ValidationStatus|Sim|  
|Validação de tipo de dados e de conteúdo|Um administrador do MDS, ao criar objetos modelo (por exemplo, o comprimento ou o tipo de dados de um atributo)|Automaticamente quando um usuário adiciona ou edita dados|Erros de entrada|InputStatus|Não|  
|Validação de tipo de dados e de conteúdo|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|Automaticamente quando um usuário adiciona ou edita dados|Erros de entrada|InputStatus|Não |  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar regras de negócio e publicá-las, de forma que os dados sejam validados em relação a elas.|[Criar e publicar uma regra de negócio &#40;Master Data Services&#41;](create-and-publish-a-business-rule-master-data-services.md)|  
|Validar uma versão de dados em relação às regras de negócio. Apenas administradores.|[Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)|  
|Validar subconjuntos específicos de dados em relação às regras de negócio. Todos os usuários com permissão para a área funcional do **Gerenciador** .|[Validar membros específicos em relação a regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)|  
|Validar subconjuntos específicos de dados em relação às regras de negócio. Todos os usuários com permissão para a área funcional do **Gerenciador** e que usam o [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].|[Aplicar regras de negócio &#40;Suplemento MDS para Excel&#41;](microsoft-excel-add-in/apply-business-rules-mds-add-in-for-excel.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
