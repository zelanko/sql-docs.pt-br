---
title: Caixa de diálogo Criar perfil e conta do Database Mail
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.dbmailprofileacct.f1
ms.assetid: b93ea3d4-9f22-490e-8e26-d766b454aed6
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 50f301dd0c64b75deb12706b6364b72744e22c34
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81728443"
---
# <a name="create-database-mail-profile-and-account-dialog-box"></a>Caixa de diálogo Criar perfil e conta do Database Mail

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Use a caixa de diálogo **Criar Perfil e Conta do Database Mail** para criar um perfil e uma conta do Database Mail para o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Este perfil será usado para notificar usuários e grupos através de email quando falhar a validação de regras de negócio.  
  
## <a name="database-mail-profile-and-account"></a>Perfil e conta do Database Mail  
 Um *perfil do Database Mail* é uma coleção de contas de correio de banco de dados. Uma *conta de correio de banco de dados* contém as informações que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usam para enviar mensagens de e-mail para um servidor SMTP. Quando você cria o perfil e a conta no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], a conta é acrescentada automaticamente ao perfil e as informações de conta são usadas para enviar emails.  
  
> [!NOTE]  
>  Você não pode usar o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para atualizar perfis ou contas existentes do Database Mail, nem pode configurar mais de uma conta para um perfil. Para realizar mais tarefas avançadas com o Database Mail, você pode usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ou scripts Transact-SQL. Para obter mais informações, consulte a seção [objetos de configuração do Database Mail](../relational-databases/database-mail/database-mail-configuration-objects.md) nos Manuais Online do SQL Server.  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|**Nome do perfil**|Digite um nome para o novo perfil do Database Mail. Este nome deve ser exclusivo entre os perfis do Database Mail configurados para o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .<br /><br /> Depois de criar este perfil, ele estará disponível e selecionado na página **Banco de Dados** no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].|  
|**Nome da Conta**|Digite um nome para a nova conta do Database Mail para associar a este perfil. Este nome deve ser exclusivo entre as contas do Database Mail configuradas para o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Essa conta não corresponde a uma conta do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nem a uma conta do Windows.|  
  
## <a name="outgoing-smtp-mail-server"></a>Servidor de saída de emails (SMTP)  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|**Endereço de email**|Digite o nome do endereço de email da conta. Este é o endereço de e-mail de que o e-mail é enviado, e deve estar no formato *email_name*@*domain_name*. Um exemplo de endereço de email é sales@contoso.com.|  
|**Nome de exibição**|Configuração opcional. Digite o nome que será exibido nas mensagens de email enviadas por essa conta. Um nome para exibição de exemplo é Grupo de Vendas da Contoso.|  
|**Endereço de email de resposta**|Configuração opcional. Digite o endereço de email a ser usado em respostas a mensagens de email enviadas desta conta. Um exemplo de endereço de email de resposta é admin@contoso.com.|  
|**Servidor SMTP**|Digite o nome ou o endereço IP do servidor SMTP usado pela conta para enviar email. Um formato de servidor SMTP de exemplo é **smtp.***<company_name>***.com**. Para obter mais ajuda sobre isso, consulte o administrador de mail.|  
|**Número da porta**|Digite o número da porta do servidor SMTP para a conta. A porta SMTP padrão é 25.|  
|**Esse servidor requer uma conexão segura (SSL)**|Criptografa a comunicação usando o TLS (Transport Layer Security, segurança de camada de transporte), anteriormente conhecido como Secure Sockets Layer (SSL).|  
  
## <a name="smtp-authentication"></a>Autenticação SMTP  
 O Database Mail pode ser enviado usando as credenciais do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]usando outras credenciais que você forneça ou de modo anônimo. Como prática recomendada, se seu servidor de email exibir a autenticação, crie uma conta de usuário específica para o Database Mail. Essa conta de usuário deve ter permissões mínimas e não deve ser usada para nenhum outro propósito.  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|**Autenticação do Windows usando as credenciais do serviço Mecanismo de Banco de Dados**|Especifique que o Database [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] Mail deve usar as credenciais da conta de serviço do Windows para autenticação no servidor SMTP.|  
|**Autenticação básica**|Especifique que o Database deve usar nome de usuário e senha específicos para autenticar no servidor SMTP. Estas informações são usadas somente para autenticação no servidor de email, e a conta não precisa corresponder a um usuário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou ao usuário no computador que executa o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
|**Nome de usuário**|Digite o nome da conta de usuário que o Database Mail usa para fazer logon no servidor SMTP. Um nome do usuário será necessário se o servidor SMTP exigir autenticação básica.|  
|**Senha**|Digite a senha que o Database Mail usa para fazer logon no servidor SMTP. Uma senha será necessária se o servidor SMTP exigir autenticação básica.|  
|**Confirmar senha**|Digite a senha novamente para confirmar.|  
|**Autenticação anônima**|Especifique que o servidor SMTP não requer autenticação. O Database Mail não usará nenhuma credencial para a autenticação no servidor SMTP.|  
  
## <a name="see-also"></a>Consulte Também  
 [Página de configuração de banco de dados &#40;gerente de configuração de serviços de dados mestre&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
[Instalação e configuração do Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md)
  
  
