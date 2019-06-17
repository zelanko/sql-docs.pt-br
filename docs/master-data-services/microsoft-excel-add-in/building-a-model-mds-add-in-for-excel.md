---
title: Compilando um modelo (Suplemento MDS para Excel) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8ae26ec3-c5d5-4c4f-a810-2951a7454439
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e3a946626223a464b63b2099912c0f89d95ff32b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65488921"
---
# <a name="building-a-model-mds-add-in-for-excel"></a>Compilando um modelo (Suplemento do MDS para Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], os administradores podem executar um subconjunto das funções administrativas disponíveis no aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
 As tarefas de compilação de modelo que os administradores podem realizar no [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] são:  
  
-   Criar entidades. Para obter mais informações sobre entidades, consulte [Entidades &#40;Master Data Services&#41;](../../master-data-services/entities-master-data-services.md).  
  
-   Criar atributos de todos os tipos, inclusive atributos baseados em domínio. Para obter mais informações sobre atributos, consulte [Atributos &#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md) e [Atributos baseados em domínio &#40;Master Data Services&#41;](../../master-data-services/domain-based-attributes-master-data-services.md).  
  
 Como um administrador, você deve criar o modelo usando o aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] ou o serviço Web. EM seguida, você pode usar o [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] para criar entidades e atributos dentro do modelo. Para obter mais informações sobre objetos de modelo, consulte [Modelos &#40;Master Data Services&#41;](../../master-data-services/models-master-data-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 A maioria das tarefas administrativas ainda deve ser realizada no aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] ou com o uso do serviço Web. A tabela a seguir mostra quais ferramentas os administradores podem usar para concluir tarefas no MDS.  
  
|Descrição da tarefa|Ferramenta|Tópico|  
|----------------------|----------|-----------|  
|Criar modelos.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] aplicativo ou serviço Web|[Criar um modelo &#40;Master Data Services&#41;](../../master-data-services/create-a-model-master-data-services.md)|  
|Criar uma entidade.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] aplicativo ou serviço Web ou [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|[Criar uma entidade &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md)|  
|Criar um atributo baseado em domínio.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] aplicativo ou serviço Web ou [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]|[Criar um atributo baseado em domínio &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|Criar grupos de atributos.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] aplicativo ou serviço Web|[Criar um grupo de atributos &#40;Master Data Services&#41;](../../master-data-services/create-an-attribute-group-master-data-services.md)|  
|Criar novas regras de negócio.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] aplicativo ou serviço Web|[Criar e publicar uma regra de negócio &#40;Master Data Services&#41;](../../master-data-services/create-and-publish-a-business-rule-master-data-services.md)|  
|Criar exibições de assinatura.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] aplicativo ou serviço Web|[Criar uma exibição de assinatura para exportar dados &#40;Master Data Services&#41;](../../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|Criar hierarquias.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] aplicativo ou serviço Web|[Criar uma hierarquia derivada &#40;Master Data Services&#41;](../../master-data-services/create-a-derived-hierarchy-master-data-services.md)<br /><br /> [Criar uma hierarquia explícita &#40;Master Data Services&#41;](../../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|Criar coleções.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] aplicativo ou serviço Web|[Criar uma coleção &#40;Master Data Services&#41;](../../master-data-services/create-a-collection-master-data-services.md)|  
|Criar versões de dados.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] aplicativo ou serviço Web|[Bloquear uma versão &#40;Master Data Services&#41;](../../master-data-services/lock-a-version-master-data-services.md)|  
|Implantar modelos.|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Aplicativo Web ou serviço Web ou ferramenta MDSModelDeploy.|[Criar um pacote de implantação de modelo usando o MDSModelDeploy](../../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Modelos &#40;Master Data Services&#41;](../../master-data-services/models-master-data-services.md)  
  
-   [Entidades &#40;Master Data Services&#41;](../../master-data-services/entities-master-data-services.md)  
  
-   [Atributos &#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md)  
  
-   [Atributos baseados em domínio &#40;Master Data Services&#41;](../../master-data-services/domain-based-attributes-master-data-services.md)  
  
-   [Grupos de atributos &#40;Master Data Services&#41;](../../master-data-services/attribute-groups-master-data-services.md)  
  
-   [Regras de negócio &#40;Master Data Services&#41;](../../master-data-services/business-rules-master-data-services.md)  
  
-   [Visão geral: Exportando dados &#40;Master Data Services&#41;](../../master-data-services/overview-exporting-data-master-data-services.md)  
  
-   [Hierarquias &#40;Master Data Services&#41;](../../master-data-services/hierarchies-master-data-services.md)  
  
-   [Coleções &#40;Master Data Services&#41;](../../master-data-services/collections-master-data-services.md)  
  
-   [Versões &#40;Master Data Services&#41;](../../master-data-services/versions-master-data-services.md)  
  
-   [Segurança &#40;Master Data Services&#41;](../../master-data-services/security-master-data-services.md)  
  
-   [Implantando modelos &#40;Master Data Services&#41;](../../master-data-services/deploying-models-master-data-services.md)  
  
  
