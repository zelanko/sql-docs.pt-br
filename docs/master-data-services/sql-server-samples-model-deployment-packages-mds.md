---
title: Exemplos de pacote de implantação de modelo
ms.custom: ''
ms.date: 07/28/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
keywords:
- master data services
- exemplo
ms.assetid: 9b31b7b6-319b-4840-b67d-eb383e7762b1
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 76ef4f409fd5a4072d27cdfa3e4180896534eaa0
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85811375"
---
# <a name="sql-server-examples-model-deployment-packages-mds"></a>Exemplos de SQL Server: Pacotes de implantação de modelo (MDS)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Pacotes de modelo de exemplo com dados são incluídos durante a instalação do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. O local padrão para esses arquivos de pacote é \<drive> \Program Files\Microsoft SQL Server\130\Master Data Services\Samples\Packages.  
  
 Para obter instruções sobre como implantar os pacotes de modelo de exemplo, consulte [Implantando dados e modelos de exemplo](../master-data-services/master-data-services-installation-and-configuration.md#deploySample). Implante os pacotes de modelo de exemplo usando a [ferramenta MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
> [!IMPORTANT]
>  **Atualizações de amostra no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**  
> 
>  Os pacotes de exemplo foram atualizados para dar suporte às novas funcionalidades a seguir.  
> 
>  -   Mostre relações muitos-para-muitos.  
> 
>      Para obter mais informações, consulte [Relação M2M no modelo de exemplo](../master-data-services/show-many-to-many-relationships-in-derived-hierarchies-master-data-services.md#M2MSample).  
> 
> -   Restringir valores permitidos para atributos baseados em domínio.  
> 
>      Para obter mais informações, consulte [Criar um atributo baseado em domínio &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md).  
> -   Exige aprovação para alterações de entidade.  
> 
>      Para obter mais informações, consulte [aprovação necessária &#40;Master Data Services&#41;](../master-data-services/approval-required-master-data-services.md).  
> -   Usar operadores Not e Else em regras de negócio  
> 
>      Para obter mais informações, consulte [Exemplos de regras de negócio](../master-data-services/business-rule-examples-master-data-services.md).  
> -   Implementar um índice personalizado  
> 
>      Para obter mais informações, consulte [Índice personalizado #40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md).  
 

 
 No Master Data Services, um pacote é um arquivo XML que contém uma estrutura de modelo implantável e, opcionalmente, dados do modelo. Use pacotes de modelo para mover cópias de modelos de um ambiente MDS para outro, ou crie novos modelos em seu ambiente do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] existente.  
  
## <a name="see-also"></a>Consulte Também  
 [Implantar um pacote de implantação de modelo usando MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
  
