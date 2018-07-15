---
title: Operações de serviço Web categorizadas (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: master-data-services
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: e3f346b5-7e26-481d-9821-1846e2e91289
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 25e0bdf059d1fec6c0716a809c54dd63153defca
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37351518"
---
# <a name="categorized-web-service-operations-master-data-services"></a>Operações de serviço Web categorizadas (Master Data Services)
  O serviço Web [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] contém um conjunto completo de operações que permitem a você escrever código para controlar todos os recursos que o [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] usa por meio de sua interface do usuário. As operações de serviço Web são definidas pela interface <xref:Microsoft.MasterDataServices.IService> e são implementadas como métodos na classe <xref:Microsoft.MasterDataServices.ServiceClient>. Este tópico agrupa as operações do serviço Web em categorias conceituais para ajudá-lo a entender como usar a API do serviço Web.  
  
## <a name="model-operations"></a>Operações de modelo  
 Estas operações são usadas para criar, atualizar e excluir modelos, bem como operar em todos os conteúdos de um modelo, como entidades, hierarquias e versões. Para obter mais informações, consulte [Modelos &#40;Master Data Services&#41;](../models-master-data-services.md).  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.MetadataClone%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.MetadataCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.MetadataDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.MetadataGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.MetadataUpdate%2A>|  
  
## <a name="entity-operations"></a>Operações de entidade  
 Estas operações são usadas para criar, atualizar e excluir os membros de uma única entidade. Para obter mais informações, consulte [Entidades &#40;Master Data Services&#41;](../entities-master-data-services.md) e [Membros &#40;Master Data Services&#41;](../members-master-data-services.md).  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMemberKeyLookup%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersCopy%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersMerge%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMembersUpdate%2A>|  
  
## <a name="member-operations"></a>Operações de membro  
 Estas operações são usadas para obter, atualizar e excluir os membros. O conjunto de membros operado pode conter membros de várias entidades. Para obter mais informações, consulte [Membros &#40;Master Data Services&#41;](../members-master-data-services.md).  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ModelMembersBulkDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ModelMembersBulkMerge%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ModelMembersBulkUpdate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ModelMembersGet%2A>|  
  
## <a name="attribute-and-hierarchy-operations"></a>Operações de atributo e hierarquia  
 Estas operações são usadas para obter informações sobre atributos e hierarquias. Atributos e hierarquias também podem ser modificados com o uso das operações de modelo, como <xref:Microsoft.MasterDataServices.ServiceClient.MetadataUpdate%2A>. Para obter mais informações, consulte [Atributos &#40;Master Data Services&#41;](../attributes-master-data-services.md) e [Hierarquias &#40;Master Data Services&#41;](../hierarchies-master-data-services.md).  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMemberAttributesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.HierarchyMembersGet%2A>|  
  
## <a name="business-rule-operations"></a>Operações de regra de negócio  
 Estas operações são usadas para criar, atualizar, excluir e publicar regras de negócios. Para obter mais informações, consulte [Regras de negócio &#40;Master Data Services&#41;](../business-rules-master-data-services.md).  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesClone%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesPaletteGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesPublish%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.BusinessRulesUpdate%2A>|  
  
## <a name="annotation-operations"></a>Operações de anotação  
 Estas operações são usadas para criar, atualizar e excluir anotações. Para obter mais informações, consulte [Anotações &#40;Master Data Services&#41;](../annotations-master-data-services.md).  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.AnnotationsDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.AnnotationsUpdate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMemberAnnotationsCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityMemberAnnotationsGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.TransactionAnnotationsCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.TransactionAnnotationsGet%2A>|  
  
## <a name="transaction-operations"></a>Operações de transação  
 Estas operações são usadas para obter e reverter transações. Para obter mais informações, consulte [Transações &#40;Master Data Services&#41;](../transactions-master-data-services.md).  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.TransactionsGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.TransactionsReverse%2A>|  
  
## <a name="version-and-validation-operations"></a>Operações de versão e validação  
 Estas operações são usadas para copiar e validar versões. Para obter mais informações, consulte [Versões &#40;Master Data Services&#41;](../versions-master-data-services.md) e [Validação &#40;Master Data Services&#41;](../validation-master-data-services.md).  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.VersionCopy%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ValidationGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ValidationProcess%2A>|  
  
## <a name="data-quality-operations"></a>Operações de qualidade de dados  
 Estas operações são usadas para executar tarefas de qualidade de dados e examinar seus resultados.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityCleansingOperationCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityMatchingOperationCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityOperationStart%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityInstalledState%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityKnowledgeBasesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityOperationResultsGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.DataQualityOperationStatus%2A>|  
  
## <a name="data-import-operations"></a>Operações de importação de dados  
 Estas operações são usadas para importar dados para um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Para obter mais informações, consulte [Importação de dados &#40;Master Data Services&#41;](../overview-importing-data-from-tables-master-data-services.md).  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityStagingClear%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityStagingGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityStagingLoad%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.EntityStagingProcess%2A>|  
  
 As operações a seguir são usadas para importar dados utilizando o processo de preparo incluído no [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. Estas operações só devem ser usadas para dar suporte aos bancos de dados existentes. Para um novo desenvolvimento, use as operações listadas anteriormente.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.StagingClear%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.StagingGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.StagingNameCheck%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.StagingProcess%2A>|  
  
## <a name="data-export-operations"></a>Operações de exportação de dados  
 Estas operações são usadas para exportar dados por meio do uso de exibições de assinatura. Para obter mais informações, consulte [exportação de dados &#40;Master Data Services&#41;](../overview-exporting-data-master-data-services.md).  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ExportViewCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ExportViewDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ExportViewListGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ExportViewUpdate%2A>|  
  
## <a name="security-operations"></a>Operações de segurança  
 Estas operações são usadas para modificar as configurações de segurança que controlam o acesso ao banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Para obter mais informações, consulte [Segurança &#40;Master Data Services&#41;](../security-master-data-services.md).  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsClone%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrincipalsUpdate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesClone%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesCreate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SecurityPrivilegesUpdate%2A>|  
  
## <a name="system-operations"></a>Operações de sistema  
 Estas operações são usadas para obter e atualizar configurações de sistema e preferências do usuário.  
  
||  
|-|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ServiceCheck%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.ServiceVersionGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SystemDomainListGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SystemPropertiesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SystemSettingsGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.SystemSettingsUpdate%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.UserPreferencesDelete%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.UserPreferencesGet%2A>|  
|<xref:Microsoft.MasterDataServices.ServiceClient.UserPreferencesUpdate%2A>|  
  
  
