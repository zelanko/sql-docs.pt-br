---
title: "Caixa de di&#225;logo Criar perfil e conta do Database Mail (Gerenciador de Configura&#231;&#227;o do Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.mds.configmanager.dbmailprofileacct.f1"
ms.assetid: b93ea3d4-9f22-490e-8e26-d766b454aed6
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
---
# Caixa de di&#225;logo Criar perfil e conta do Database Mail (Gerenciador de Configura&#231;&#227;o do Master Data Services)
  Use a caixa de diálogo **Criar Perfil e Conta do Database Mail** para criar um perfil e uma conta do Database Mail para o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Este perfil será usado para notificar usuários e grupos através de email quando falhar a validação de regras de negócio.  
  
## Perfil e conta do Database Mail  
 Um *perfil do Database Mail* é uma coleção de contas do Database Mail. Uma *conta do Database Mail* contém as informações que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa para enviar mensagens de email a um servidor SMTP. Quando você cria o perfil e a conta no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], a conta é acrescentada automaticamente ao perfil e as informações de conta são usadas para enviar emails.  
  
> [!NOTE]  
>  Você não pode usar o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para atualizar perfis ou contas existentes do Database Mail, nem pode configurar mais de uma conta para um perfil. Para realizar mais tarefas avançadas com o Database Mail, você pode usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ou scripts Transact-SQL. Para obter mais informações, consulte a seção [objetos de configuração do Database Mail](../relational-databases/database-mail/database-mail-configuration-objects.md) nos Manuais Online do SQL Server.  
  
|Nome do controle|Description|  
|------------------|-----------------|  
|**Nome do perfil**|Digite um nome para o novo perfil do Database Mail. Este nome deve ser exclusivo entre os perfis do Database Mail configurados para o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].<br /><br /> Depois de criar este perfil, ele estará disponível e selecionado na página **Banco de Dados** no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].|  
|**Nome da conta**|Digite um nome para a nova conta do Database Mail para associar a este perfil. Este nome deve ser exclusivo entre as contas do Database Mail configuradas para o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Essa conta não corresponde a uma conta do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nem a uma conta do Windows.|  
  
## Servidor de saída de emails (SMTP)  
  
|Nome do controle|Description|  
|------------------|-----------------|  
|**Endereço de email**|Digite o nome do endereço de email da conta. Este é o endereço de email por meio do qual o email é enviado e deve estar no formato *email_name*@*domain_name*. Um endereço de email de exemplo é sales@contoso.com.|  
|**Nome para exibição**|Configuração opcional. Digite o nome que será exibido nas mensagens de email enviadas por essa conta. Um nome para exibição de exemplo é Grupo de Vendas da Contoso.|  
|**Endereço de email de resposta**|Configuração opcional. Digite o endereço de email a ser usado em respostas a mensagens de email enviadas desta conta. Um endereço de email de resposta de exemplo é admin@contoso.com.|  
|**Servidor SMTP**|Digite o nome ou o endereço IP do servidor SMTP usado pela conta para enviar email. Um formato de servidor SMTP de exemplo é **smtp.***<company_name>***.com**. Para obter mais ajuda sobre isso, consulte o administrador de mail.|  
|**Número da porta**|Digite o número da porta do servidor SMTP para a conta. A porta SMTP padrão é 25.|  
|**Esse servidor requer uma conexão segura (SSL)**|Criptografa a comunicação usando o protocolo SSL (Secure Sockets Layer).|  
  
## Autenticação SMTP  
 O Database Mail pode ser enviado usando as credenciais do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] usando outras credenciais que você forneça ou de modo anônimo. Como prática recomendada, se seu servidor de email exibir a autenticação, crie uma conta de usuário específica para o Database Mail. Essa conta de usuário deve ter permissões mínimas e não deve ser usada para nenhum outro propósito.  
  
|Nome do controle|Description|  
|------------------|-----------------|  
|**Autenticação do Windows usando as credenciais do serviço Mecanismo de Banco de Dados**|Especifique que o Database Mail deve usar as credenciais da conta de serviço Windows do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] para autenticação no servidor SMTP.|  
|**Autenticação Básica**|Especifique que o Database deve usar nome de usuário e senha específicos para autenticar no servidor SMTP. Estas informações são usadas somente para autenticação no servidor de email, e a conta não precisa corresponder a um usuário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou ao usuário no computador que executa o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
|**Nome de usuário**|Digite o nome da conta de usuário que o Database Mail usa para fazer logon no servidor SMTP. Um nome do usuário será necessário se o servidor SMTP exigir autenticação básica.|  
|**Senha**|Digite a senha que o Database Mail usa para fazer logon no servidor SMTP. Uma senha será necessária se o servidor SMTP exigir autenticação básica.|  
|**Confirmar senha**|Digite a senha novamente para confirmar.|  
|**Autenticação anônima**|Especifique que o servidor SMTP não requer autenticação. O Database Mail não usará nenhuma credencial para a autenticação no servidor SMTP.|  
  
## Consulte também  
 [Página Configuração do Banco de Dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Introdução ao Master Data Services &#40;SQL Server 2016&#41;](../Topic/Get%20Started%20with%20Master%20Data%20Services%20\(SQL%20Server%202016\).md)  
  
  