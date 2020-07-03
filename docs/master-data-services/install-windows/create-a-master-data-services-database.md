---
title: Criar um banco de dados do Master Data Services
description: Crie um banco de dados Master Data Services quando precisar de um novo banco de dados para dar suporte ao aplicativo Web Master Data Manager e ao serviço Web Master Data Services.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8373bb35-f0f9-4c3c-a53c-dfaa2ce567ac
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: af13d59ddb5c8837959feb83b31fc17dbcd7aa29
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85883866"
---
# <a name="create-a-master-data-services-database"></a>Criar um banco de dados do Master Data Services

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Crie um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] quando precisar de um novo banco de dados para oferecer suporte ao aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e ao serviço Web do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
-   Para obter informações sobre os requisitos para o computador que hospeda o banco de dados, veja [Requisitos do banco de dados &#40;Master Data Services&#41;](../../master-data-services/install-windows/database-requirements-master-data-services.md).  
  
### <a name="to-create-a-master-data-services-database"></a>Para criar um banco de dados do Master Data Services  
  
1.  Abra [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
2.  No painel esquerdo, clique em **Configuração do Banco de Dados**.  
  
3.  Na página **Configuração do Banco de Dados** , clique em **Criar Banco de Dados**.  
  
4.  Conclua o assistente **Criar Banco de Dados** para criar e configurar o banco de dados. Para obter informações sobre as opções da interface do usuário no assistente, veja [Assistente para Criar Banco de Dados &#40;Master Data Services Configuration Manager&#41;](../../master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   Defina as configurações do sistema para o banco de dados e o aplicativo Web. Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](../../master-data-services/system-settings-master-data-services.md).  
  
-   Crie um aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] para associar a este banco de dados. Para obter mais informações, veja [Criar um aplicativo Web do Master Data Manager &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md).  
  
-   Configure um plano de manutenção para fazer backup dos logs de banco de dados e de transação. Para obter mais informações, veja [Requisitos do banco de dados &#40;Master Data Services&#41;](../../master-data-services/install-windows/database-requirements-master-data-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
