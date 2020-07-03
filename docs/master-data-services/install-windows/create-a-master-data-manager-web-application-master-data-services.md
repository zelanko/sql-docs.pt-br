---
title: Criar aplicativo Web Master Data Manager
description: O aplicativo Web Master Data Manager fornece uma interface para que os usuários trabalhem com os dados mestres e para que os administradores configurem e administrem o MDS.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 241d46d7-8008-47f6-bebd-0dfff1cc856a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1f7504244f658af94cccb42bead95de60b2c409e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882113"
---
# <a name="create-a-master-data-manager-web-application-master-data-services"></a>Criar um aplicativo Web do Master Data Manager (Master Data Services)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  O aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] oferece uma interface para usuários trabalharem com dados mestre e para administradores configurarem e administrarem o MDS.  
  
 Um aplicativo Web sempre deve ser contido por um site. Para criar um aplicativo Web, você deve:  
  
-   Usar o site Padrão e criar o aplicativo Web,  
  
-   Usar um site existente e criar o aplicativo Web ou  
  
-   Criar um novo site, que cria automaticamente um aplicativo Web.  
  
 Após criar o aplicativo Web, associe-o com o banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
-   Para obter informações sobre os requisitos para o computador que hospeda o aplicativo Web, consulte [Requisitos do aplicativo Web &#40;Master Data Services&#41;](../../master-data-services/install-windows/web-application-requirements-master-data-services.md).  
  
## <a name="to-create-a-master-data-manager-web-application-in-a-new-website"></a>Para criar um aplicativo Web do Master Data Manager em um novo site  
 Quando você cria um novo site, o aplicativo Web raiz é o aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . O aplicativo Web também é adicionado a um novo pool de aplicativos.  
  
> [!NOTE]  
>  Se você seguir este procedimento, não poderá especificar um caminho virtual e um alias do aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . Se desejar especificar um caminho virtual e um alias para o [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], crie um aplicativo Web em um site existente que ainda não esteja configurado como um aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
 Adicionalmente, o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] só oferece suporte à criação de sites com associações de HTTP. Para adicionar uma associação de HTTPS, crie um novo site e aplicativo no [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] e, em seguida, consulte [Proteger um aplicativo Web Master Data Manager](../../master-data-services/install-windows/secure-a-master-data-manager-web-application.md) para obter mais informações.  
  
#### <a name="to-create-a-master-data-manager-web-application-in-a-new-website"></a>Para criar um aplicativo Web do Master Data Manager em um novo site  
  
1.  Abra [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
2.  No painel esquerdo, clique em **Configuração da Web**.  
  
3.  Na página **Configuração da Web** , na lista de Sites, selecione **Criar novo site**.  
  
4.  Na caixa de diálogo **Criar Site** , especifique as informações para um novo site. Para obter mais informações sobre as opções da interface do usuário na caixa de diálogo, consulte [Caixa de diálogo Criar Site &#40;Gerenciador de Configuração do Master Data Services&#41;](../../master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md).  
  
5.  Clique em **OK**.  
  
## <a name="to-create-a-master-data-manager-web-application-in-an-existing-website"></a>Para criar um aplicativo Web do Master Data Manager em um site existente  
 Ao criar um aplicativo Web em um site existente, você pode escolher o caminho virtual e o alias do aplicativo Web. O aplicativo Web é adicionado a um novo pool de aplicativos.  
  
#### <a name="to-create-a-master-data-manager-web-application-in-an-existing-website"></a>Para criar um aplicativo Web do Master Data Manager em um site existente  
  
1.  Abra [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
2.  No painel esquerdo, clique em **Configuração da Web**.  
  
3.  Na página **Configuração da Web** , da lista **Site** , selecione o site no qual você deseja criar o aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
4.  Clique em **Criar Aplicativo**.  
  
5.  Na caixa de diálogo **Criar Aplicativo Web** , especifique as informações para um novo aplicativo Web. Para obter mais informações sobre as opções da interface do usuário na caixa de diálogo, consulte [Caixa de diálogo Criar Aplicativo Web &#40;Gerenciador de Configuração do Master Data Services&#41;](../../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md).  
  
6.  Clique em **OK**.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   Associe o aplicativo Web a um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] . Para obter mais informações, consulte [Associar um banco de dados do Master Data Services a um aplicativo Web](../../master-data-services/install-windows/associate-a-master-data-services-database-and-web-application.md).  
  
-   Opcionalmente, configure o site que hospeda o [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] aplicativo Web para usar uma associação HTTPS se você quiser criptografar o conteúdo usando TLS (segurança de camada de transporte), anteriormente conhecido como protocolo SSL (SSL). Você deve usar uma ferramenta Serviços de Informações da Internet (IIS), como o Gerenciador do IIS, para configurar o certificado do servidor para o servidor Web e para configurar uma associação HTTPS e as configurações de TLS para o site. Para obter mais informações, consulte [Secure a Master Data Manager Web Application](../../master-data-services/install-windows/secure-a-master-data-manager-web-application.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
