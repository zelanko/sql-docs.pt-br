---
title: Configurar o site da Web e o banco de dados para Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.mds.configmanager.general.f1
ms.assetid: d50863e7-50d9-4ab8-aabb-fd68e2d132a1
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 09e3e92d20182be2feb1c357cc1d3f518c55e5ad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117439"
---
# <a name="set-up-the-database-and-website-for-master-data-services"></a>Instalar o banco de dados e o site para o Master Data Services
  Use o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para definir o banco de dados e o site para [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS)  
  
 Para instalar o banco de dados e o site, conclua as seguintes tarefas.  
  
1.  Criar um banco de dados usando o **configuração de banco de dados** página [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].  
  
     Para obter informações, consulte [página de configuração de banco de dados &#40;Gerenciador de configuração do Master Data Services&#41; ](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md) e [criar Assistente de banco de dados &#40;Gerenciador de configuração do Master Data Services&#41; ](../../2014/master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
2.  Criar um novo site, selecione o site padrão ou selecione outro site existente, usando o **configuração da Web** página [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Em seguida, associe o banco de dados do MDS ao aplicativo Web que você selecionar ou criar.  
  
     Para obter informações, consulte [página Configuração da Web &#40;Gerenciador de configuração do Master Data Services&#41; ](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md) e [caixa de diálogo Criar site &#40;Gerenciador de configuração do Master Data Services&#41; ](../../2014/master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md).  
  
3.  (Opcional) Habilitar a integração com serviços de qualidade de dados usando o **configuração da Web** página [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].  
  
     Para obter mais informações, consulte [página Configuração da Web &#40;Gerenciador de configuração do Master Data Services&#41; ](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md) e [Enable Data Quality Services Integration with Master Data Services](install-windows/enable-data-quality-services-integration-with-master-data-services.md).  
  
 Você também pode usar [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para especificar configurações para os aplicativos web e serviços associados ao banco de dados MDS. Por exemplo, você pode especificar a frequência com que os dados são carregados ou os emails de validação são enviados. Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Banco de dados dos Master Data Services](../../2014/master-data-services/master-data-services-database.md)   
 [Aplicativo Web Master Data Manager](../../2014/master-data-services/master-data-manager-web-application.md)  
  
  