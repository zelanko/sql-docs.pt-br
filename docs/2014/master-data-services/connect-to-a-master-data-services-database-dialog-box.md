---
title: Caixa de diálogo Conectar-se a um Banco de Dados do Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.srvconnect.f1
ms.assetid: b2f8c9b9-c31e-4f0d-9095-978709423190
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 7b326d1f46641e0530eafdf8568354ad69ff103d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225806"
---
# <a name="connect-to-a-master-data-services-database-dialog-box"></a>Caixa de diálogo Conectar-se a um Banco de Dados do Master Data Services
  Use a caixa de diálogo **Conectar a um Banco de Dados do Master Data Services** para selecionar um banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
 No [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], esta caixa de diálogo está disponível nas seguintes páginas:  
  
-   Na página **Configuração do Banco de Dados** , clique em **Selecionar Banco de Dados** . Use esta caixa de diálogo para selecionar um banco de dados para o qual definir as configurações de sistema.  
  
-   Na página **Configuração da Web** , em **Associar Aplicativo ao Banco de Dados**, clique em **Selecionar** para selecionar o banco de dados para associar ao seu site ou aplicativo do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
## <a name="select-database"></a>Selecionar banco de dados  
 Especifique as informações para conexão com uma instância local ou remota do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] que hospeda o banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para conexão com uma instância remota, o banco de dados deve estar habilitado para conexões remotas.  
  
|Nome do controle|Description|  
|------------------|-----------------|  
|**Instância do SQL Server**|Especifique o nome da instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] na qual deseja hospedar o banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Pode ser uma instância padrão ou nomeada em um computador local ou remoto. Especifique as informações digitando:<br /><br /> Um ponto (.) para se conectar à instância padrão no computador local.<br /><br /> O nome do servidor ou o endereço IP para conectar à instância padrão no computador local ou remoto especificado.<br /><br /> O nome do servidor ou o endereço IP e o nome da instância para conexão à instância nomeada no computador local ou remoto especificado. Especifique essas informações no formato *server_name*\\*instance_name*.|  
|**Tipo de autenticação**|Selecione o tipo de autenticação a ser usado ao conectar à instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada. As credenciais que você usa para se conectar determinam os bancos de dados exibidos na lista suspensa **Banco de dados do Master Data Services** . Os tipos de autenticação incluem:<br /><br /> **Usuário Atual – Segurança Integrada**: usa a Autenticação Integrada do Windows para conexão usando as credenciais da conta do Windows do usuário atual. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] usa as credenciais do Windows do usuário que fez logon no computador e abriu o aplicativo. Não é possível especificar credenciais diferentes do Windows no aplicativo. Para conectar-se com credenciais diferentes do Windows, faça logon no computador como esse usuário e abra o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].<br /><br /> **Conta do SQL Server**: usa uma conta do SQL Server para a conexão. Quando você seleciona essa opção, os campos **Nome de usuário** e **Senha** são habilitados e você deve especificar credenciais de uma conta do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] na instância especificada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|**Nome de usuário**|Especifique o nome da conta de usuário que será usada para conexão à instância especificada do SQL Server. A conta deve fazer parte da função **sysadmin** na instância especificada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .<br /><br /> Quando o **Tipo de autenticação** é **Usuário Atual – Segurança Integrada**, a caixa **Nome de usuário** é somente leitura e exibe o nome da conta de usuário do Windows que está conectada no computador.<br /><br /> Quando o **Tipo de autenticação** é **Conta do SQL Server**, a caixa **Nome de usuário** está habilitada e você deve especificar credenciais para uma conta do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] na instância especificada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|**Senha**|Especifique a senha associada à conta de usuário:<br /><br /> Quando o **Tipo de autenticação** é **Usuário Atual – Segurança Integrada**, a caixa **Senha** é somente leitura e as credenciais da conta do usuário do Windows especificada são usadas para a conexão.<br /><br /> Quando o **Tipo de autenticação** é **Conta do SQL Server**, a caixa **Senha** está habilitada e você deve especificar a senha associada à conta de usuário especificada.|  
|**Connect**|Conecte-se à instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com as credenciais especificadas.|  
|**Banco de dados do Master Data Services**|Exibe os bancos de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] na instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada com base nos seguintes critérios:<br /><br /> Quando o usuário for um membro da função de servidor **sysadmin** para aquela instância, são exibidos todos os bancos de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] naquela instância.<br /><br /> Quando o usuário for membro da função de banco de dados **db_owner** em qualquer banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] nessa instância, os bancos de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] serão exibidos.<br /><br /> <br /><br /> Para obter mais informações sobre as funções do SQL Server, consulte [Funções em nível de servidor](../relational-databases/security/authentication-access/server-level-roles.md) e [Funções em nível de banco de dados](../relational-databases/security/authentication-access/database-level-roles.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Página Configuração do Banco de Dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Instalar o banco de dados e o site para o Master Data Services](set-up-the-database-and-website-for-master-data-services.md)  
  
  
