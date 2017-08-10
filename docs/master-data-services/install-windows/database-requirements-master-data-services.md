---
title: Requisitos (Master Data Services) do banco de dados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fe731839-c5c4-4884-bb6a-644eca28bb30
caps.latest.revision: 18
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9f48345ef6fb8bd0a27bf2d40a829e53e2eae308
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="database-requirements-master-data-services"></a>Requisitos do banco de dados (Master Data Services)
  Todos os dados mestres estão armazenados em um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] . O computador que hospeda esse banco de dados deve executar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Use o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] para criar e configurar o banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] em um computador local ou remoto. Se você mover o banco de dados de um ambiente para outro, poderá manter as informações em um novo ambiente associando o serviço Web do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e o [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] ao banco de dados em seu novo local.  
  
> [!NOTE]  
>  Qualquer computador em que os componentes do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] deve ser licenciado. Para obter mais informações, consulte o Contrato de Licença de Usuário Final (EULA).  
  
## <a name="requirements"></a>Requisitos  
 Antes de criar um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , verifique se os requisitos a seguir são atendidos.  
  
### <a name="sql-server-edition"></a>Edição do SQL Server  
 O banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] pode ser hospedado nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a seguir:  
  
 
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Enterprise (64 bits) x64  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Developer (64 bits) x64  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence (64 bits) x64  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (64 bits) x64  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer (64 bits) x64  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Business Intelligence (64 bits) x64  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Enterprise (64 bits) x64 – Atualização somente do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Enterprise  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Developer (64 bits) x64  
  
-   Microsoft SQL Server 2008 R2 Enterprise (64 bits) x64  
  
-   Microsoft SQL Server 2008 R2 Developer (64 bits) x64  
  
 Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md). 
  
### <a name="operating-system"></a>Sistema operacional  
 Para obter informações sobre os sistemas operacionais Windows com suporte e outros requisitos para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)], veja [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
### <a name="accounts-and-permissions"></a>Contas e permissões  
  
|Tipo|Descrição|  
|----------|-----------------|  
|Conta de usuário|No [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)], você pode usar uma conta do Windows ou uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para se conectar à instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para hospedar o banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] . A conta de usuário deve pertencer à função de servidor **sysadmin** na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Para obter mais informações sobre a função **sysadmin** , veja [Funções de nível de servidor](../../relational-databases/security/authentication-access/server-level-roles.md).|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] conta de administrador|Ao criar um banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , você deve especificar uma conta de usuário de domínio para ser o administrador do sistema [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] . Para todos os aplicativos Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] associados a este banco de dados, este usuário pode atualizar todos os modelos e todos os dados em todas as áreas funcionais. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../../master-data-services/administrators-master-data-services.md).|  
  
### <a name="database-backup"></a>Backup do banco de dados  
 Como prática recomendada, faça backup do banco de dados completo diariamente em um período de baixa atividade e faça backup dos logs de transações mais frequentemente, dependendo das necessidades do seu ambiente. Para obter mais informações sobre backups de banco de dados, confira [Visão geral de Backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instalar o Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)   
 [Criar um banco de dados do Master Data Services](../../master-data-services/install-windows/create-a-master-data-services-database.md)   
 [Banco de dados dos Master Data Services](../../master-data-services/master-data-services-database.md)   
 [Conecte-se a uma caixa de diálogo banco de dados do Master Data Services](../../master-data-services/connect-to-a-master-data-services-database-dialog-box.md)   
 [Criar Assistente de banco de dados &#40; Gerenciador de configuração do Master Data Services &#41;](../../master-data-services/create-database-wizard-master-data-services-configuration-manager.md)  
  
  
