---
title: "Logon para Assinaturas Atualiz&#225;veis | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.updatablesubscriptionslogin.f1"
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# Logon para Assinaturas Atualiz&#225;veis
  Para atualização imediata, se você tiver selecionado **replicar** sobre o **assinaturas atualizáveis** página desse assistente, você deve especificar uma conta com o assinante na qual são feitas conexões com o publicador. 
  
 Conexões são usadas pelos gatilhos acionados no assinante e propagam alterações para o publicador. Essa conta é necessária mesmo que você selecionou **enfileirar alterações e confirmar quando possível** sobre o **assinaturas atualizáveis** página. Por padrão o novo Assistente de assinatura configura atualização enfileirada com a capacidade de alternar para atualização imediata, se necessário.  
  
> **IMPORTANTE:** A conta especificada para a conexão só deve ser concedida permissão inserir, atualizar e excluir dados nas exibições que a replicação cria o banco de dados de publicação. Ele não deve ser fornecido nenhuma permissão adicional. Conceder permissões nos modos de exibição no banco de dados de publicação nomeado no formato **syncobj _***\< Número_hexadecimal>* para a conta configurada em cada assinante.  
  
 Há três opções disponíveis para o tipo de conexão:  
  
-   Um servidor vinculado ou remoto que você já definiu.  
  
-   Um servidor vinculado que a replicação cria; a conexão é feita com as credenciais que você especifica nesse assistente.  
  
-   Um servidor vinculado que a replicação cria; a conexão é feita com as credenciais do usuário que faz a alteração no Assinante.  
  
 As duas primeiras opções podem ser especificadas nesse assistente. A última opção só pode ser especificada usando [sp_link_publication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md); Especifique um valor de **1** para o parâmetro **@security_mode**.  
  
## Opções  
 **Criar um servidor vinculado que conecta usando o seguinte logon de Autenticação do SQL Server:**  
 A replicação cria um servidor vinculado usando as credenciais especificadas no **Login** e **senha** campos.  
  
 **Logon**  
 Insira um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon que tenha somente as permissões descritas neste tópico.  
  
 **Senha**  
 Digite uma senha forte para o logon especificado em **Login**.  
    
 **Usar servidor vinculado ou remoto já definido.**  
 Essa opção requer um servidor vinculado ou remoto já definido. Para obter mais informações, consulte [servidores vinculados e 40; o mecanismo de banco de dados e 41;](../../relational-databases/linked-servers/linked-servers-database-engine.md) e [servidores remotos](../../database-engine/configure-windows/remote-servers.md). Verifique se o logon usado para o servidor vinculado ou servidor remoto tem uma senha forte e somente as permissões descritas nesse tópico.  
  
## Consulte também  
 [Criar uma assinatura atualizável em uma publicação transacional](https://msdn.microsoft.com/library/ms152769.aspx)   
 [Exibir e modificar configurações de segurança de replicação](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)  
  
  