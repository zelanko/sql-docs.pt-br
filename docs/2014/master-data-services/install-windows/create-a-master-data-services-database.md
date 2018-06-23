---
title: Criar um banco de dados do Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8373bb35-f0f9-4c3c-a53c-dfaa2ce567ac
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: d73e6531af9e6485c5ac784ef101d3209f551eb2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117451"
---
# <a name="create-a-master-data-services-database"></a>Criar um banco de dados do Master Data Services
  Crie um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] quando precisar de um novo banco de dados para oferecer suporte ao aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e ao serviço Web do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   Para obter informações sobre os requisitos para o computador que hospeda o banco de dados, veja [Requisitos do banco de dados &#40;Master Data Services&#41;](database-requirements-master-data-services.md).  
  
### <a name="to-create-a-master-data-services-database"></a>Para criar um banco de dados do Master Data Services  
  
1.  Abra o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
2.  No painel esquerdo, clique em **Configuração do Banco de Dados**.  
  
3.  Na página **Configuração do Banco de Dados** , clique em **Criar Banco de Dados**.  
  
4.  Conclua o assistente **Criar Banco de Dados** para criar e configurar o banco de dados. Para obter informações sobre as opções da interface do usuário no assistente, veja [Assistente para Criar Banco de Dados &#40;Master Data Services Configuration Manager&#41;](../create-database-wizard-master-data-services-configuration-manager.md).  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   Defina as configurações do sistema para o banco de dados e o aplicativo Web. Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](../system-settings-master-data-services.md).  
  
-   Crie um aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] para associar a este banco de dados. Para obter mais informações, veja [Criar um aplicativo Web do Master Data Manager &#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md).  
  
-   Configure um plano de manutenção para fazer backup dos logs de banco de dados e de transação. Para obter mais informações, veja [Requisitos do banco de dados &#40;Master Data Services&#41;](database-requirements-master-data-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instalar o Master Data Services](install-master-data-services.md)  
  
  