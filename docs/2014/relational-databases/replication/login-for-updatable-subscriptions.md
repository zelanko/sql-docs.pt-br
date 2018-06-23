---
title: Logon para assinaturas atualizáveis | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.newsubwizard.updatablesubscriptionslogin.f1
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 2379b7b58cdfd6ee55abf848bbac314f2180931e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019117"
---
# <a name="login-for-updatable-subscriptions"></a>Logon para Assinaturas Atualizáveis
  Se você selecionou **replicar** no **assinaturas atualizáveis** página deste assistente, você deve especificar uma conta no assinante na qual as conexões com o publicador são feitas para atualização imediata assinaturas. Conexões são usadas pelos gatilhos acionados no Assinante e que propagam as alterações no Publicador. Essa conta é necessária mesmo que você selecionou **enfileirar alterações e confirmar quando possível** no **assinaturas atualizáveis** página, porque, por padrão o Assistente para nova assinatura configura atualização enfileirada a capacidade de alternar para atualização imediata, se necessário.  
  
> [!IMPORTANT]  
>  A conta especificada para a conexão só deve receber permissão para inserir, atualizar e excluir dados nas exibições criadas pela replicação no banco de dados de publicação; nenhuma permissão adicional será dada. Conceda permissões para exibições no banco de dados de publicação que são nomeadas no formato **syncobj_***\<HexadecimalNumber>* para a conta configurada em cada Assinante.  
  
 Há três opções disponíveis para o tipo de conexão:  
  
-   Um servidor vinculado ou remoto que você já definiu.  
  
-   Um servidor vinculado que a replicação cria; a conexão é feita com as credenciais que você especifica nesse assistente.  
  
-   Um servidor vinculado que a replicação cria; a conexão é feita com as credenciais do usuário que faz a alteração no Assinante.  
  
 As duas primeiras opções podem ser especificadas nesse assistente. A última opção só pode ser especificada com o uso de [sp_link_publication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql); especifique um valor igual a **1** para o parâmetro **@security_mode**.  
  
## <a name="options"></a>Opções  
 **Criar um servidor vinculado que conecta usando o seguinte logon de Autenticação do SQL Server:**  
 A replicação cria um servidor vinculado usando as credenciais especificadas nos campos **Logon** e **Senha** .  
  
 **Logon**  
 Insira um logon [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tenha somente as permissões descritas neste tópico.  
  
 **Senha**  
 Insira uma senha forte para o logon especificado em **Logon**.  
  
 **Confirmar Senha**  
 Reinsira a senha para confirmar que ela foi inserida corretamente.  
  
 **Usar servidor vinculado ou remoto já definido.**  
 Essa opção requer um servidor vinculado ou remoto já definido. Para obter mais informações, consulte [Servidores vinculados &#40;Mecanismo de Banco de Dados&#41;](../linked-servers/linked-servers-database-engine.md) e [Servidores remotos](../../database-engine/configure-windows/remote-servers.md). Verifique se o logon usado para o servidor vinculado ou servidor remoto tem uma senha forte e somente as permissões descritas nesse tópico.  
  
## <a name="see-also"></a>Consulte também  
 [Create an Updatable Subscription to a Transactional Publication](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [Exibir e modificar configurações de segurança de replicação](security/view-and-modify-replication-security-settings.md)   
 [Assinaturas atualizáveis para replicação transacional](transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Assinar publicações](subscribe-to-publications.md)  
  
  
