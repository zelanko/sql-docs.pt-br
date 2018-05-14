---
title: Assistente para Criar Banco de Dados (Gerenciador de Configuração do Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.createdbwiz.f1
ms.assetid: 45fe7a23-a46c-4d40-8bca-3431fbfc5c9d
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: f29c8f95b93fc45f853294b5fdcb82a0119c92cd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="create-database-wizard-master-data-services-configuration-manager"></a>Assistente para Criar Banco de Dados (Gerenciador de Configuração do Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Use o assistente para **Criar Banco de Dados** para criar um banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
## <a name="database-server"></a>Servidor de Banco de Dados  
 Especifique as informações para conexão com uma instância local ou remota do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] na qual hospedar o banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para conexão com uma instância remota, o banco de dados deve estar habilitado para conexões remotas.  
  
|Nome do controle|Description|  
|------------------|-----------------|  
|**Instância do SQL Server**|Especifique o nome da instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] na qual deseja hospedar o banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Pode ser uma instância padrão ou nomeada em um computador local ou remoto. Especifique as informações digitando:<br /><br /> Um ponto (.) para se conectar à instância padrão no computador local.<br /><br /> O nome do servidor ou o endereço IP para conectar à instância padrão no computador local ou remoto especificado.<br /><br /> O nome do servidor ou o endereço IP e o nome da instância para conexão à instância nomeada no computador local ou remoto especificado. Especifique essas informações no formato *server_name*\\*instance_name*.|  
|**Tipo de autenticação**|Selecione o tipo de autenticação a ser usado ao conectar à instância do SQL Server especificada. As credenciais usadas para conexão devem fazer parte da função de servidor **sysadmin** para a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada. Para obter mais informações sobre a função sysadmin, veja [Funções em nível de servidor](../relational-databases/security/authentication-access/server-level-roles.md).<br /><br /> Os tipos de autenticação incluem:<br /><br /> **Usuário Atual – Segurança Integrada**: usa a Autenticação Integrada do Windows para conexão usando as credenciais da conta do Windows do usuário atual. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] usa as credenciais do Windows do usuário que fez logon no computador e abriu o aplicativo. Não é possível especificar credenciais diferentes do Windows no aplicativo. Para conectar-se com credenciais diferentes do Windows, faça logon no computador como esse usuário e abra o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].<br /><br /> **Conta do SQL Server**: usa uma conta do SQL Server para a conexão. Quando você seleciona essa opção, os campos **Nome de usuário** e **Senha** são habilitados e você deve especificar credenciais de uma conta do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] na instância especificada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|**User name**|Especifique o nome da conta de usuário que será usada para conexão à instância especificada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . A conta deve fazer parte da função **sysadmin** na instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada.<br /><br /> Quando o **Tipo de autenticação** é **Usuário Atual – Segurança Integrada**, a caixa **Nome de usuário** é somente leitura e exibe o nome da conta de usuário do Windows que está conectada no computador.<br /><br /> Quando o **Tipo de autenticação** é **Conta do SQL Server**, a caixa **Nome de usuário** está habilitada e você deve especificar credenciais para uma conta do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] na instância especificada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|**Senha**|Especifique a senha associada à conta de usuário:<br /><br /> Quando o **Tipo de autenticação** é **Usuário Atual – Segurança Integrada**, a caixa **Senha** é somente leitura e as credenciais da conta do usuário do Windows especificada são usadas para a conexão.<br /><br /> Quando o **Tipo de autenticação** é **Conta do SQL Server**, a caixa **Senha** está habilitada e você deve especificar a senha associada à conta de usuário especificada.|  
|**Testar Conexão**|Verifique se a conta de usuário especificada pode se conectar à instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e se a conta tem permissão para criar um banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] nessa instância. Se você não clicar em **Testar Conexão**, a conexão será testada quando você clicar em **Avançar**.|  
  
## <a name="database"></a>banco de dados  
 Especifique um nome de banco de dados e as opções de agrupamento para o novo banco de dados. Os agrupamentos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornecem propriedades de regras de classificação, de diferenciação de maiúsculas e minúsculas e de diferenciação de acentos para seus dados. Os agrupamentos utilizados com tipos de dados de caractere, como char e varchar, determinam a página de código e os caracteres correspondentes que podem ser representados para o tipo de dados em questão. Para obter mais informações sobre agrupamento de banco de dados, consulte [Suporte a agrupamentos e a Unicode](../relational-databases/collations/collation-and-unicode-support.md).  
  
|Nome do controle|Description|  
|------------------|-----------------|  
|**Nome do banco de dados**|Especifique um nome para o banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**Agrupamento padrão do SQL Server**|Selecione para usar a configuração de agrupamento atual do banco de dados da instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada para o novo banco de dados.|  
|**Agrupamento do Windows**|Especifique as configurações de agrupamento do Windows para uso com o novo banco de dados. Os agrupamentos do Windows definem regras para armazenar dados de caractere com base em uma localidade do Windows associada. Para obter mais informações sobre agrupamentos do Windows e as opções associadas, consulte [Nome de agrupamento do Windows &#40;Transact-SQL&#41;](../t-sql/statements/windows-collation-name-transact-sql.md).<br /><br /> Observação: a lista **Agrupamento do Windows** e as opções associadas são habilitadas apenas depois de você desmarcar a caixa **Agrupamento padrão do SQL Server** .|  
  
## <a name="administrator-account"></a>Conta Administrador  
  
|Nome do controle|Description|  
|------------------|-----------------|  
|**User name**|Especifique o Superusuário padrão para o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Um Superusuário tem acesso a todas as áreas funcionais e pode adicionar, excluir e atualizar todos os modelos. Para obter informações sobre a permissão de Superusuário e outros tipos de administradores no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], consulte [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).|  
  
## <a name="summary"></a>Resumo  
 Exibe um resumo das opções selecionadas. Examine suas seleções e clique em **Avançar** para começar a criar o banco de dados com as configurações especificadas.  
  
## <a name="progress-and-finish"></a>Progresso e Conclusão  
 Exibe o progresso do processo de criação. Depois que o banco de dados for criado, clique em **Concluir** para fechar o assistente de banco de dados e retornar à página **Bancos de dados** . O novo banco de dados é selecionado e você pode exibir e modificar as configurações do sistema.  
  
## <a name="see-also"></a>Consulte Também  
 [Página Configuração do Banco de Dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
[Instalação e configuração do Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md)[Requisitos do banco de dados &#40;Master Data Services&#41;](../master-data-services/install-windows/database-requirements-master-data-services.md)  
  
  
