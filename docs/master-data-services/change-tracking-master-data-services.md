---
title: Controle de alterações (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- change tracking [SQL Server]
ms.assetid: 5e879c65-0d38-454f-9a20-62a6e72c89f7
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: d02dd9770c152c91201a133d35034611a76a3535
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855084"
---
# <a name="change-tracking-master-data-services"></a>Controle de alterações (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode usar grupos de controle de alterações para executar uma ação quando um valor de atributo muda. Use o controle de alterações quando você não souber qual será o novo valor, mas desejar saber se houve alterações.  
  
## <a name="configuring-change-tracking"></a>Configurando o controle de alterações  
 Para configurar o controle de alterações, você adiciona um atributo a um grupo de controle de alterações. O grupo pode conter um ou muitos atributos. Depois, você cria uma regra de negócios para definir a ação que é executada quando há mudanças em quaisquer dos atributos no grupo.  
  
> [!NOTE]  
>  Regras de negócio de controle de alterações consideram os dados preparados (importados) a serem alterados.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Adicionar atributos a um grupo de controle de alterações.|[Adicionar atributos a um grupo de controle de alterações &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)|  
|Criar uma regra de negócios que inicie ações com base em alterações de atributos.|[Iniciar ações com base em alterações no valor do atributo &#40;Master Data Services&#41;](../master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Validação &#40;Master Data Services&#41;](../master-data-services/validation-master-data-services.md)  
  
-   [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
-   [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
