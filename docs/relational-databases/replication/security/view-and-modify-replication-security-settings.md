---
title: Exibir e modificar configurações de segurança de replicação | Microsoft Docs
description: Saiba como exibir e modificar as configurações de segurança de replicação no SQL Server usando o SQL Server Management Studio, o Transact-SQL ou o Replication Management Objects.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying replication security settings
- replication [SQL Server], security
- security [SQL Server replication], viewing settings
- viewing replication security settings
- security [SQL Server replication], modifying settings
ms.assetid: 67d79532-1482-4de1-ac9f-4a23d162c85e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 84175e90bdc9c441238f9259268d8a3078364066
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917723"
---
# <a name="view-and-modify-replication-security-settings"></a>Exibir e modificar configurações de segurança de replicação
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Este tópico descreve como exibir e modificar configurações de segurança de replicação no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)], ou RMO (Replication Management Objects). Por exemplo, você pode querer alterar a conexão do Agente de Leitor de Log com o Publicador de uma autenticação do SQL Server para uma autenticação integrada do Windows ou alterar as credenciais usadas para executar um trabalho do agente quando a senha do Windows foi alterada. Para obter informações sobre as permissões exigidas por cada agente, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para exibir e modificar configurações de segurança de replicação, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
-   **Acompanhamento:**  [depois de modificar configurações de segurança de replicação](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Os procedimentos armazenados usados dependem do tipo de agente e do tipo de conexão de servidor.  
  
-   As classes e propriedades RMO que você usa dependem do tipo de agente e do tipo de conexão de servidor.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 Por questões de segurança, os valores reais das senhas são mascarados em conjuntos de resultados retornados por procedimentos armazenados de replicação.  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Exiba e modifique as configurações de segurança nas seguintes caixas de diálogo:  
  
1.  A caixa de diálogo **Atualizar Senhas de Replicação** que está disponível na pasta **Replicação** do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Se você alterar a senha para uma conta do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou uma conta do Windows no servidor em uma topologia de replicação, use essa caixa de diálogo ao invés de atualizar a senha para cada agente que usa essa conta. Se agentes em mais de um servidor usam a mesma conta, você deverá conectar-se a cada servidor e alterar a senha. A senha será atualizada em todos os lugares em que a replicação usa a senha. A senha não é atualizada em outros lugares, como servidores vinculados.  
  
2.  A página **Segurança do Agente** da caixa de diálogo **Propriedades da Publicação – \<Publication>** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
3.  A caixa de diálogo **Propriedades de Assinatura – \<Subscription>** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) e [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
4.  As caixas de diálogo **Propriedades do Distribuidor – \<Distributor>** e **Propriedades do Banco de Dados de Distribuição – \<Database>** . Para obter mais informações sobre como acessar essas caixas de diálogo, consulte [View and Modify Distributor and Publisher Properties](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
5.  A caixa de diálogo **Propriedades do Publicador – \<Publisher>** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Distributor and Publisher Properties](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  

#### <a name="to-change-the-password-for-an-account-used-by-one-or-more-agents"></a>Para alterar a senha para uma conta usada por um ou mais agentes  
  
1.  Se a conta for uma conta do SQL Server, essa caixa de diálogo também alterará a senha para a conta do SQL Server. Se a conta for uma conta de Windows, altere primeiro a senha no Windows. Para obter mais informações, consulte a documentação do Windows.  
  
    > [!NOTE]  
    >  Depois de alterar a senha de replicação de um agente, você deve parar e reiniciar cada agente que a usa para que a alteração entre em vigor para aquele agente.  
  
2.  Conecte-se ao servidor no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
3.  Clique com o botão direito do mouse na pasta **Replicação** e, então, clique em **Atualizar Senhas de Replicação**.  
  
4.  Na caixa de diálogo **Atualizar Senhas de Replicação** , especifique a conta e a nova senha.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent"></a>Para alterar as configurações de segurança do Snapshot Agent  
  
1.  Na página **Segurança do Agente** da caixa de diálogo **Propriedades da Publicação – \<Publication>** , clique no botão **Configurações de Segurança** próximo à caixa de texto **Agente de Instantâneo**.  
  
2.  Na caixa de diálogo **Segurança do Snapshot Agent** , especifique a conta sob a qual o agente deveria ser executado:  
  
    -   Digite uma nova conta de Windows na caixa de texto **Conta do Agent** .  
  
    -   Digite uma nova senha forte nas caixas de texto de **Senha** e **Confirmar senha** .  
  
3.  Especifique o contexto sob o qual o agente deveria se conectar do Distribuidor ao Publicador. Se você selecionar **Usando o seguinte logon do SQL Server**, você também terá que especificar o logon:  
  
    -   Digite um logon na caixa de texto **Logon**  
  
    -   Digite uma nova senha forte nas caixas de texto de **Senha** e **Confirmar senha** .  
  
    > [!NOTE]  
    >  Se o Publicador for um Editor Oracle, o contexto de conexão será especificado na caixa de diálogo **Propriedades do Distribuidor – \<Distributor>** . Veja a seguir o procedimento para alterar o contexto.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-log-reader-agent"></a>Para alterar as configurações de segurança para o Log Reader Agent  
  
1.  Na página **Segurança do Agente** da caixa de diálogo **Propriedades da Publicação – \<Publication>** , clique no botão **Configurações de Segurança** próximo à caixa de texto **Agente de Leitor de Log**.  
  
2.  Na caixa de diálogo **Segurança do Log Reader Agent** , especifique a conta sob a qual o agente deveria ser executado:  
  
    -   Digite uma nova conta de Windows na caixa de texto **Conta do Agent** .  
  
    -   Digite uma nova senha forte nas caixas de texto de **Senha** e **Confirmar senha** .  
  
3.  Especifique o contexto sob o qual o agente deveria se conectar do Distribuidor ao Publicador. Se você selecionar **Usando o seguinte logon do SQL Server**, você também terá que especificar o logon:  
  
    -   Digite um logon na caixa de texto **Logon**  
  
    -   Digite uma nova senha forte nas caixas de texto de **Senha** e **Confirmar senha** .  
  
    > [!NOTE]  
    >  Se o Publicador for um Editor Oracle, o contexto de conexão será especificado na caixa de diálogo **Propriedades do Distribuidor – \<Distributor>** . Altere o contexto usando o procedimento a seguir.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Há um Log Reader Agent para cada banco de dados publicado. A alteração das configurações de segurança para o agente para uma publicação afeta as configurações no banco de dados de publicação.  
  
#### <a name="to-change-the-context-under-which-the-snapshot-agent-and-log-reader-agent-for-an-oracle-publication-make-connections-to-the-publisher"></a>Para alterar o contexto no qual o Snapshot Agent e o Log Reader Agent de um Editor Oracle fazem conexões com o Publicador  
  
1.  Na página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor – \<Distributor>** , clique no botão de propriedades ( **...** ) próximo a um Publicador.  
  
2.  Na seção **Conexão do Agente com o Publicador** , especifique o logon e a senha usados pelo esquema de usuário administrativo de replicação que você configurou. Para obter mais informações, consulte [Configure an Oracle Publisher](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md) (Configurar um publicador do Oracle).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription"></a>Para alterar configurações de segurança do Distribution Agent para uma assinatura push  
  
1.  Na caixa de diálogo **Propriedades de Assinatura – \<Subscription>** no Publicador, você pode fazer as seguintes alterações:  
  
    -   Para alterar a conta na qual o Agente de Distribuição executa e faz conexões com o Distribuidor, clique na linha **Conta de processo de agente** e, depois, clique no botão ( **...** ) de propriedades na linha. Especifique uma conta e uma senha na caixa de diálogo **Segurança do Agente de Distribuição** .  
  
    -   Para alterar o contexto no qual o Agente de Distribuição conecta-se ao Assinante, clique na linha **Conexão do Assinante** e, depois, clique no botão ( **...** ) de propriedades na linha. Especifique o contexto na caixa de diálogo **Inserir Informações de Conexão** .  
  
         Se você usar assinaturas de atualização enfileirada, o Queue Reader Agent também usará o contexto especificado aqui para conexões com o Assinante.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription"></a>Para alterar as configurações de segurança do Distribution Agent para uma assinatura pull  
  
1.  Na caixa de diálogo **Propriedades de Assinatura – \<Subscription>** no Assinante, você poderá fazer as seguintes alterações:  
  
    -   Para alterar a conta na qual o Agente de Distribuição executa e faz conexões com o Assinante, clique na linha **Conta de processo de agente** e, depois, clique no botão ( **...** ) de propriedades na linha. Especifique uma conta e uma senha na caixa de diálogo **Segurança do Agente de Distribuição** .  
  
         Se você usar assinaturas de atualização enfileirada, o Queue Reader Agent também usará o contexto especificado aqui para conexões com o Assinante.  
  
    -   Para alterar o contexto no qual o Agente de Distribuição se conecta ao Distribuidor, clique na linha **Conexão do Distribuidor** e, depois, clique no botão ( **...** ) de propriedades na linha. Especifique o contexto na caixa de diálogo **Inserir Informações de Conexão** .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription"></a>Para alterar as configurações de segurança do Merge Agent para uma assinatura push  
  
1.  Na caixa de diálogo **Propriedades de Assinatura – \<Subscription>** no Publicador, você pode fazer as seguintes alterações:  
  
    -   Para alterar a conta na qual o Agente de Mesclagem executa e faz conexões com o Publicador e o Distribuidor, clique na linha **Conta de processo de agente** e, em seguida, clique no botão ( **...** ) de propriedades na linha. Especifique a conta e a senha na caixa de diálogo **Segurança do Agente de Mesclagem** .  
  
    -   Para alterar o contexto no qual o Agente de Mesclagem se conecta ao Assinante, clique na linha **Conexão do Assinante** e, depois, clique no botão ( **...** ) de propriedades na linha. Especifique o contexto na caixa de diálogo **Inserir Informações de Conexão** .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription"></a>Para alterar as configurações de segurança do Merge Agent para uma assinatura pull  
  
1.  Na caixa de diálogo **Propriedades de Assinatura – \<Subscription>** no Assinante, você poderá fazer as seguintes alterações:  
  
    -   Para alterar a conta na qual o Agente de Mesclagem executa e faz conexões com o Assinante, clique na linha **Conta de processo de agente** e, depois, clique no botão ( **...** ) de propriedades na linha. Especifique a conta e a senha na caixa de diálogo **Segurança do Agente de Mesclagem** .  
  
    -   Para alterar o contexto no qual o Agente de Mesclagem é conectado ao Publicador e ao Distribuidor, clique na linha **Conexão do Publicador** e, em seguida, clique no botão ( **...** ) de propriedades na linha. Especifique o contexto na caixa de diálogo **Inserir Informações de Conexão** .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-the-account-under-which-the-queue-reader-agent-runs"></a>Para alterar a conta sob a qual o Queue Reader Agent é executado  
  
1.  Na página **Geral** da caixa de diálogo **Propriedades do Distribuidor – \<Distributor>** , clique no botão de propriedades ( **…** ), ao lado do banco de dados de distribuição.  
  
2.  Na caixa de diálogo **Propriedades do Banco de Dados de Distribuição – \<Database>** , clique no botão **Configurações de Segurança** próximo à caixa de texto **Conta de processo de agente**.  
  
3.  Na caixa de diálogo **Segurança do Queue Reader Agent** , especifique a conta na qual o agente é executado e efetua conexões com o Distribuidor.  
  
    -   Digite uma nova conta de Windows na caixa de texto **Conta de processo** .  
  
    -   Digite uma nova senha forte nas caixas de texto de **Senha** e **Confirmar senha** .  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Há um Agente de Leitor de Fila para cada banco de dados de distribuição. Alterar as configurações de segurança do agente afeta as configurações de todas as publicações em todos os Publicadores que usam esse banco de dados de distribuição.  
  
#### <a name="to-change-the-context-under-which-the-queue-reader-agent-makes-connections-to-the-publisher"></a>Para alterar o contexto sob a qual o Queue Reader Agent faz conexões com o Publicador  
  
1.  Na página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor – \<Distributor>** , clique no botão de propriedades ( **...** ) próximo do Publicador.  
  
2.  Na seção **Conexão do Agente com o Publicador** , especifique o valor de **Representar a conta de processo do agente** ou **Autenticação do SQL Server** para a opção **Modo de Conexão de Agente** . Se você especificar a **Autenticação do SQL Server**, também digite os valores para **Logon** e **Senha**.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Há um Agente de Leitor de Fila para cada banco de dados de distribuição. Alterar as configurações de segurança do agente afeta as configurações de todas as publicações em todos os Publicadores que usam esse banco de dados de distribuição.  
  
#### <a name="to-change-the-context-under-which-the-queue-reader-agent-makes-connections-to-the-subscriber"></a>Para alterar o contexto sob o qual o Queue Reader Agent faz conexões com o Assinante  
  
-   O Queue Reader Agent usa o mesmo contexto de conexão que o Distribution Agent para a assinatura. Para obter mais informações, veja os procedimentos acima para o Distribution Agent.  
  
#### <a name="to-change-security-settings-for-an-immediate-updating-pull-subscription"></a>Para alterar as configurações de segurança para uma assinatura pull de atualização imediata  
  
1.  Na caixa de diálogo **Propriedades de Assinatura – \<Subscription>** no Assinante, clique na linha **Conexão do Publicador** e, em seguida, clique no botão ( **&#x2026;** ) de propriedades na linha.  
  
2.  Na caixa de diálogo **Inserir Informações de Conexão** , selecione uma das seguintes opções:  
  
    -   **Usar um logon de servidor vinculado ou remoto**. Selecione esta opção se você tiver definido um servidor remoto ou vinculado entre o Assinante e o Publicador usando [sp_addserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou outro método.  
  
    -   **Usar a Autenticação do SQL Server com estas informações de logon e senha**. Selecione essa opção se um servidor vinculado ou remoto entre o Assinante e o Publicador ainda não tiver sido definido. A replicação criará um servidor vinculado para você. É necessário que a conta especificada já exista no Publicador.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Esse procedimento altera o método utilizado pelos gatilhos de replicação para conexão do Assinante com o Publicador quando as alterações são feitas no Assinante. Você também pode alterar as configurações associadas com o Distribution Agent para uma assinatura de atualização imediata. Para obter mais informações, consulte os procedimentos descritos anteriormente neste tópico.  
>   
>  Este procedimento só se aplica às assinaturas pull. Para assinaturas push, use o procedimento armazenado [sp_link_publication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md).  
  
#### <a name="to-change-the-password-for-the-administrative-connection-from-the-publisher-to-the-distributor"></a>Para alterar a senha para a conexão administrativa do Publicador para o Distribuidor  
  
1.  Na página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor – \<Distributor>** , insira uma senha forte nas caixas de texto **Senha** e **Confirmar Senha**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
3.  Na página **Geral** da caixa de diálogo **Propriedades do Publicador – \<Publisher>** , insira uma senha forte nas caixas de texto **Senha** e **Confirmar Senha**.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
> [!IMPORTANT]  
>  Em todos os procedimentos a seguir, quando possível, solicite aos usuários que digitem as credenciais de segurança em runtime. Se armazenar credenciais em um arquivo de script, proteja o arquivo para evitar acesso não autorizado.  
  
#### <a name="to-change-all-instances-of-a-stored-password-at-a-replication-server"></a>Para alterar todas as instâncias de uma senha armazenada em um servidor de replicação  
  
1.  Em um servidor, em uma topologia de replicação do banco de dados mestre, execute [sp_changereplicationserverpasswords](../../../relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql.md). Especifique a conta do Windows [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ou o logon do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuja senha está sendo alterada para `@login` e a nova senha para a conta ou o logon de `@password`. Isso altera todas as instâncias da senha usada por todos os agentes no servidor quando em conexão com outros servidores da topologia.  
  
    > [!NOTE]  
    >  Para alterar apenas o logon e a senha de uma conexão com um servidor específico na topologia (como o Distribuidor ou o Assinante), especifique o nome desse servidor como `@server`.  
  
2.  Repita a Etapa 1 em todos servidores da topologia de replicação nos quais a senha precise ser atualizada.  
  
    > [!NOTE]  
    >  Depois de alterar a senha de replicação de um agente, você deve parar e reiniciar cada agente que a usa para que a alteração entre em vigor para aquele agente.  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent"></a>Para alterar as configurações de segurança do Snapshot Agent  
  
1.  No Publicador, execute [sp_helppublication_snapshot](../../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md) especificando `@publication`. Isso retorna as atuais configurações de segurança do Snapshot Agent.  
  
2.  No Publicador, execute [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md) especificando `@publication` e uma ou mais das seguintes configurações de segurança a serem alteradas:  
  
    -   Para alterar a conta do Windows na qual o agente é executado ou apenas a senha dessa conta, especifique `@job_login` e `@job_password`.  
  
    -   Para alterar o modo de segurança usado ao se conectar ao Publicador, especifique um valor igual a **1** ou **0** para `@publisher_security_mode`.  
  
    -   Ao alterar o modo de segurança usado ao se conectar ao Publicador de **1** para **0** ou ao alterar um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usado para essa conexão, especifique `@publisher_login` e `@publisher_password`.  
  
    > [!IMPORTANT]  
    >  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-change-security-settings-for-the-log-reader-agent"></a>Para alterar as configurações de segurança para o Log Reader Agent  
  
1.  No Publicador, execute [sp_helplogreader_agent](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) especificando `@publisher`. Isso retorna as atuais configurações de segurança para o Log Reader Agent.  
  
2.  No Publicador, execute [sp_changelogreader_agent](../../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md) especificando `@publication` e uma ou mais das seguintes configurações de segurança a serem alteradas:  
  
    -   Para alterar a conta do Windows na qual o agente é executado ou apenas a senha dessa conta, especifique `@job_login` e `@job_password`.  
  
    -   Para alterar o modo de segurança usado ao se conectar ao Publicador, especifique um valor igual a **1** ou **0** para `@publisher_security_mode`.  
  
    -   Ao alterar o modo de segurança usado ao se conectar ao Publicador de **1** para **0** ou ao alterar um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usado para essa conexão, especifique `@publisher_login` e `@publisher_password`.  
  
    > [!NOTE]  
    >  Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
    > [!IMPORTANT]  
    >  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription"></a>Para alterar configurações de segurança do Distribution Agent para uma assinatura push  
  
1.  No Publicador do banco de dados de publicação, execute [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) especificando `@publication` e `@subscriber`. Isso retorna propriedades de assinatura, inclusive configurações de segurança para o Distribution Agent em execução no Distribuidor.  
  
2.  No Publicador do banco de dados de publicação, execute [sp_changesubscription](../../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md) especificando `@publication`, `@subscriber`, `@subscriber_db**`, um valor igual a `all` para `@article`, o nome da propriedade de segurança para `@property` e o novo valor da propriedade para `@value`.  
  
3.  Repita a Etapa 2, para cada uma das seguintes propriedades de segurança que forem alteradas:  
  
    -   Para alterar a conta do Windows na qual o agente é executado ou apenas a senha dessa conta, especifique um valor igual a **distrib_job_password** para `@property` e uma nova senha para `@value`. Ao alterar a própria conta, repita a etapa 2 especificando um valor igual a **distrib_job_login** para `@property` e a nova conta do Windows para `@value`.  
  
    -   Para alterar o modo de segurança usado ao se conectar ao Assinante, especifique um valor igual a **subscriber_security_mode** para `@property` e um valor igual a **1** (Autenticação Integrada do Windows) ou **0** (Autenticação do SQL Server) para `@value`.  
  
    -   Ao alterar o modo de segurança do Assinante para a Autenticação do SQL Server ou se alterar as informações de logon para a Autenticação do SQL Server, especifique um valor igual a **subscriber_password** para `@property` e a nova senha para `@value`. Repita a etapa 2 especificando um valor igual a **subscriber_login** para `@property` e um novo logon para `@value`.  
  
    > [!NOTE]  
    >  Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
    > [!IMPORTANT]  
    >  Quando o Publicador for configurado com um Distribuidor remoto, os valores fornecidos para todas as propriedades, inclusive **distrib_job_login** e **distrib_job_password**, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription"></a>Para alterar as configurações de segurança do Distribution Agent para uma assinatura pull  
  
1.  No Assinante, execute [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md) especificando `@publication`. Isto retornará propriedades de assinatura, inclusive configurações de segurança para o Distribution Agent que é executado no Assinante.  
  
2.  No Assinante do banco de dados de assinatura, execute [sp_change_subscription_properties](../../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md) especificando `@publisher`, `@publisher_db`, `@publication`, o nome da propriedade de segurança para `@property` e o novo valor da propriedade para `@value`.  
  
3.  Repita a Etapa 2, para cada uma das seguintes propriedades de segurança que forem alteradas:  
  
    -   Para alterar a conta do Windows na qual o agente é executado ou apenas a senha dessa conta, especifique um valor igual a **distrib_job_password** para `@property` e uma nova senha para `@value`. Ao alterar a própria conta, repita a etapa 2 especificando um valor igual a **distrib_job_login** para `@property` e a nova conta do Windows para `@value`.  
  
    -   Para alterar o modo de segurança usado ao se conectar ao Distribuidor, especifique um valor igual a **distributor_security_mode** para `@property` e um valor igual a **1** (Autenticação Integrada do Windows) ou **0** (Autenticação do SQL Server) para `@value`.  
  
    -   Ao alterar o modo de segurança do Distribuidor para a Autenticação do SQL Server ou se alterar as informações de logon para a Autenticação do SQL Server, especifique um valor igual a **distributor_password** para `@property` e a nova senha para `@value`. Repita a etapa 2 especificando um valor igual a **distributor_login** para `@property` e o novo logon para `@value`.  
  
    > [!NOTE]  
    >  Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription"></a>Para alterar as configurações de segurança do Merge Agent para uma assinatura push  
  
1.  No Publicador do banco de dados de publicação, execute [sp_helpmergesubscription](../../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md) especificando `@publication`, `@subscriber,` e `@subscriber_db`. Isto retorna propriedades de assinatura, inclusive configurações de segurança para o Merge Agent em execução no Distribuidor.  
  
2.  No Publicador do banco de dados de publicação, execute [sp_changemergesubscription](../../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md) especificando `@publication`, `@subscriber`, `@subscriber_db`, o nome da propriedade de segurança para `@property` e o novo valor da propriedade para `@value`.  
  
3.  Repita a Etapa 2, para cada uma das seguintes propriedades de segurança que forem alteradas:  
  
    -   Para alterar a conta do Windows na qual o agente é executado ou apenas a senha dessa conta, especifique um valor igual a **merge_job_password** para `@property` e uma nova senha para `@value`. Ao alterar a própria conta, repita a etapa 2 especificando um valor igual a **merge_job_login** para `@property` e a nova conta do Windows para `@value`.  
  
    -   Para alterar o modo de segurança usado ao se conectar ao Assinante, especifique um valor igual a **subscriber_security_mode** para `@property` e um valor igual a **1** (Autenticação Integrada do Windows) ou **0** (Autenticação do SQL Server) para `@value`.  
  
    -   Ao alterar o modo de segurança do Assinante para a Autenticação do SQL Server ou se alterar as informações de logon para a Autenticação do SQL Server, especifique um valor igual a **subscriber_password** para `@property` e a nova senha para `@value`. Repita a etapa 2 especificando um valor igual a **subscriber_login** para `@property` e um novo logon para `@value`.  
  
    -   Para alterar o modo de segurança usado ao se conectar ao Publicador, especifique um valor igual a **publisher_security_mode** para `@property` e um valor igual a **1** (Autenticação Integrada do Windows) ou **0** (Autenticação do SQL Server) para `@value`.  
  
    -   Ao alterar o modo de segurança do Publicador para a Autenticação do SQL Server ou se alterar as informações de logon para a Autenticação do SQL Server, especifique um valor igual a **publisher_password** para `@property` e a nova senha para `@value`. Repita a etapa 2 especificando um valor igual a **publisher_login** para `@property` e o novo logon para `@value`.  
  
    > [!NOTE]  
    >  Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
    > [!IMPORTANT]  
    >  Quando o Publicador for configurado com um Distribuidor remoto, os valores fornecidos para todas as propriedades, inclusive **merge_job_login** e **merge_job_password**, serão enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription"></a>Para alterar as configurações de segurança do Merge Agent para uma assinatura pull  
  
1.  No Assinante, execute [sp_helpmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md) especificando ``@publication``. Isso retornará propriedades de assinatura, inclusive configurações de segurança para o Merge Agent que executa no Assinante.  
  
2.  No Assinante do banco de dados de assinatura, execute [sp_change_subscription_properties](../../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md) especificando `@publisher`, `@publisher_db`, `@publication`, o nome da propriedade de segurança para `@property` e o novo valor da propriedade para `@value`.  
  
3.  Repita a Etapa 2, para cada uma das seguintes propriedades de segurança que forem alteradas:  
  
    -   Para alterar a conta do Windows na qual o agente é executado ou apenas a senha dessa conta, especifique um valor igual a **merge_job_password** para `@property` e uma nova senha para `@value`. Ao alterar a própria conta, repita a Etapa 2 especificando um valor igual a **merge_job_login** para `@property` e a nova conta do Windows para `@value`.  
  
    -   Para alterar o modo de segurança usado ao se conectar ao Distribuidor, especifique um valor igual a **distributor_security_mode** para `@property` e um valor igual a **1** (Autenticação Integrada do Windows) ou **0** (Autenticação do SQL Server) para `@value`.  
  
    -   Ao alterar o modo de segurança do Distribuidor para a Autenticação do SQL Server ou se alterar as informações de logon para a Autenticação do SQL Server, especifique um valor igual a **distributor_password** para `@property` e a nova senha para `@value`. Repita a etapa 2 especificando um valor igual a **distributor_login** para `@property` e o novo logon para `@value`.  
  
    -   Para alterar o modo de segurança usado ao se conectar ao Publicador, especifique um valor igual a **publisher_security_mode** para `@property` e um valor igual a **1** (Autenticação Integrada do Windows) ou **0** (Autenticação do SQL Server) para `@value`.  
  
    -   Ao alterar o modo de segurança do Publicador para a Autenticação do SQL Server ou se alterar as informações de logon da Autenticação do SQL Server, especifique um valor igual a **publisher_password** para `@property` e a nova senha para `@value`. Repita a etapa 2 especificando um valor igual a **publisher_login** para `@property` e o novo logon para `@value`.  
  
    > [!NOTE]  
    >  Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent-to-generate-a-filtered-snapshot-for-a-subscriber"></a>Para alterar configurações de segurança para o Snapshot Agent para gerar um instantâneo filtrado para um Assinante  
  
1.  No Publicador, execute [sp_helpdynamicsnapshot_job](../../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md) especificando `@publication`. No conjunto de resultados, observe o valor de **job_name** para a partição do Assinante a ser alterada.  
  
2.  No Publicador, execute [sp_changedynamicsnapshot_job](../../../relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql.md) especificando `@publication`, o valor obtido na etapa 1 para `dynamic_snapshot_jobname` e uma nova senha para `@job_password` ou o logon e a senha da conta do Windows na qual o agente é executado para `@job_login` e `@job_password`.  
  
    > [!IMPORTANT]  
    >  Quando um Publicador é configurado com um Distribuidor remoto, os valores fornecidos para todos os parâmetros, inclusive *job_login* e *job_password*, são enviados ao Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
#### <a name="to-change-security-settings-for-the-queue-reader-agent"></a>Para alterar as configurações de segurança para o Queue Reader Agent  
  
1.  Para o Distribuidor, execute [sp_helpqreader_agent](../../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md). Isso retorna a conta do atual em que o Queue Reader Agent é executado.  
  
    -   No Distribuidor, execute [sp_changeqreader_agent](../../../relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql.md) especificando as configurações da conta do Windows para `@job_login` e `@job_password`.  
  
    > [!NOTE]  
    >  Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor. Há um Agente de Leitor de Fila para cada banco de dados de distribuição. Alterar as configurações de segurança do agente afeta as configurações de todas as publicações em todos os Publicadores que usam esse banco de dados de distribuição.  
  
2.  O Queue Reader Agent faz conexões com o Assinante usando o mesmo contexto de conexão do Distribution Agent para a assinatura.  
  
#### <a name="to-change-security-mode-used-by-an-immediate-updating-subscriber-when-connecting-to-the-publisher"></a>Para alterar modo de segurança usado por um Assinante de atualização imediato durante conexão com o Publicador  
  
1.  No Assinante, no banco de dados de assinatura, execute [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md). Especifique `@publisher`, `@publication`, o nome do banco de dados da publicação para `@publisher_db`e um dos seguintes valores para `@security_mode`:  
  
    -   **0** para usar a Autenticação do SQL Server ao fazer atualizações no Publicador. Essa opção requer a especificação de um logon válido no Publicador para `@login` e `@password`.  
  
    -   **1** para usar o contexto de segurança do usuário que faz alterações no Assinante durante conexão com o Assinante. Consulte [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) quanto às restrições relacionadas a esse modo de segurança.  
  
    -   **2** Para usar um logon de servidor vinculado existente, definido pelo usuário, usando [sp_addlinkedserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
#### <a name="to-change-the-password-for-a-remote-distributor"></a>Para alterar a senha de um Distribuidor remoto  
  
1.  No Distribuidor do banco de dados de distribuição, execute [sp_changedistributor_password](../../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) especificando a nova senha desse logon para `@password`.  
  
    > [!IMPORTANT]  
    >  Não altere diretamente a senha para **distributor_admin** .  
  
2.  Em todos os Publicadores que usam esse Distribuidor remoto, execute [sp_changedistributor_password](../../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) especificando a senha da etapa 1 para `@password`.  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os serviços [criptográficos](https://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework do Windows.  
  
#### <a name="to-change-all-instances-of-a-password-stored-on-a-replication-server"></a>Para alterar todas as instâncias de uma senha armazenada em um servidor de replicação  
  
1.  Crie uma conexão com o servidor de replicação usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationServer> usando a conexão da Etapa 1.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeReplicationServerPasswords%2A> . Especifique os seguintes parâmetros:  
  
    -   *security_mode* - a <xref:Microsoft.SqlServer.Replication.ReplicationSecurityMode> que especifica o tipo de autenticação para a qual todas as instâncias da senha estão sendo alteradas.  
  
    -   *login* - o logon para a qual todas as instâncias da senha estão sendo alteradas.  
  
    -   *password* - o novo valor de senha.  
  
        > [!IMPORTANT]  
        >  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os [serviços criptográficos](https://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo Windows .NET Framework.  
  
        > [!NOTE]  
        >  Só um membro da **sysadmin** função de servidor fixa pode chamar este método.  
  
4.  Repita as Etapas 1-3 em todo servidor, na topologia de replicação, onde a senha deve ser atualizada.  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription-to-a-transactional-publication"></a>Para alterar as configurações de segurança para o Distribution Agent de uma assinatura push para uma publicação transacional  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.TransSubscription>.  
  
3.  Defina o <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, e as propriedades <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> para a assinatura, e defina a conexão da Etapa 1 para a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de assinatura na etapa 3 foram definidas incorretamente ou a assinatura não existe.  
  
5.  Defina uma ou mais das seguintes propriedades de segurança na instância de <xref:Microsoft.SqlServer.Replication.TransSubscription>:  
  
    -   Para alterar as credenciais para a conta do Windows sob a qual o agente é executado, defina a <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e os campos <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> de <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>.  
  
    -   Para especificar a Autenticação Integrada do Windows como o tipo de autenticação que o agente usa ao se conectar ao Assinante, defina o campo <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> da propriedade <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> como **true**.  
  
    -   Para especificar a Autenticação do SQL Server como o tipo de autenticação que o agente usa ao conectar-se ao Assinante, defina o campo de <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> da propriedade <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> para **false**, e especifique as credenciais de logon do Assinante para os campos <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> .  
  
        > [!NOTE]  
        >  A conexão de agente para o Distribuidor sempre é feita usando as credenciais de Windows especificadas por <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>. Essa conta é também usada para fazer conexões remotas que usam a Autenticação do Windows.  
  
6.  (Opcional) Se você especificar um valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para confirmar as alterações no servidor. (Opcional) Se você especificar um valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (padrão), as alterações serão enviadas imediatamente ao servidor.  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription-to-a-transactional-publication"></a>Para alterar as configurações de segurança para o Distribution Agent de uma assinatura pull para uma publicação transacional  
  
1.  Crie uma conexão com o Assinante usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPullSubscription>.  
  
3.  Defina o <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, e as propriedades <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> para a assinatura, e defina a conexão da Etapa 1 para a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de assinatura na etapa 3 foram definidas incorretamente ou a assinatura não existe.  
  
5.  Defina uma ou mais das seguintes propriedades de segurança na instância de <xref:Microsoft.SqlServer.Replication.TransPullSubscription>:  
  
    -   Para alterar as credenciais para a conta do Windows sob a qual o agente é executado, defina a <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e os campos <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> de <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>.  
  
    -   Para especificar a Autenticação Integrada do Windows como o tipo de autenticação que o agente usa ao conectar-se ao Distribuidor, defina o campo <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> da propriedade <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> para **true**.  
  
    -   Para especificar a Autenticação do SQL Server como o tipo de autenticação que o agente usa ao conectar-se ao Distribuidor, defina o campo de <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> da propriedade <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> para **false**, e especifique as credenciais de logon do Distribuidor para os campos <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> .  
  
        > [!NOTE]  
        >  A conexão de agente para o Assinante sempre é feita usando as credenciais de Windows especificadas por <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>. Essa conta é também usada para fazer conexões remotas que usam a Autenticação do Windows.  
  
6.  (Opcional) Se você especificar um valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para confirmar as alterações no servidor. (Opcional) Se você especificar um valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (padrão), as alterações serão enviadas imediatamente ao servidor.  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription-to-a-merge-publication"></a>Para alterar as configurações de segurança para o Merge Agent para uma assinatura pull para uma publicação de mesclagem  
  
1.  Crie uma conexão com o Assinante usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePullSubscription>.  
  
3.  Defina o <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, e as propriedades <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> para a assinatura, e defina a conexão da Etapa 1 para a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de assinatura na etapa 3 foram definidas incorretamente ou a assinatura não existe.  
  
5.  Defina uma ou mais das seguintes propriedades de segurança na instância de <xref:Microsoft.SqlServer.Replication.MergePullSubscription>:  
  
    -   Para alterar as credenciais para a conta do Windows sob a qual o agente é executado, defina a <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e os campos <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> de <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>.  
  
    -   Para especificar a Autenticação Integrada do Windows como o tipo de autenticação que o agente usa ao conectar-se ao Distribuidor, defina o campo <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> da propriedade <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> para **true**.  
  
    -   Para especificar a Autenticação do SQL Server como o tipo de autenticação que o agente usa ao conectar-se ao Distribuidor, defina o campo de <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> da propriedade <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> para **false**, e especifique as credenciais de logon do Distribuidor para os campos <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> .  
  
    -   Para especificar a Autenticação Integrada do Windows como o tipo de autenticação que o agente usa ao se conectar ao Publicador, defina o campo <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> da propriedade <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> para **true**.  
  
    -   Para especificar a Autenticação do SQL Server como o tipo de autenticação que o agente usa ao se conectar ao Publicador, defina o campo <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> da propriedade <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> para **false**, e especifique as credenciais de logon do Publicador para os campos <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> .  
  
        > [!NOTE]  
        >  A conexão de agente para o Assinante sempre é feita usando as credenciais de Windows especificadas por <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>. Essa conta é também usada para fazer conexões remotas que usam a Autenticação do Windows.  
  
6.  (Opcional) Se você especificar um valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para confirmar as alterações no servidor. (Opcional) Se você especificar um valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (padrão), as alterações serão enviadas imediatamente ao servidor.  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription-to-a-merge-publication"></a>Para alterar as configurações de segurança para o Merge Agent para uma assinatura push para uma publicação de mesclagem  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.MergeSubscription>.  
  
3.  Defina o <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, e as propriedades <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> para a assinatura, e defina a conexão da Etapa 1 para a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de assinatura na etapa 3 foram definidas incorretamente ou a assinatura não existe.  
  
5.  Defina uma ou mais das seguintes propriedades de segurança na instância de <xref:Microsoft.SqlServer.Replication.MergeSubscription>:  
  
    -   Para alterar as credenciais para a conta do Windows sob a qual o agente é executado, defina a <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e os campos <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> de <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>.  
  
    -   Para especificar a Autenticação Integrada do Windows como o tipo de autenticação que o agente usa ao se conectar ao Assinante, defina o campo <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> da propriedade <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> como **true**.  
  
    -   Para especificar a Autenticação do SQL Server como o tipo de autenticação que o agente usa ao conectar-se ao Assinante, defina o campo de <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> da propriedade <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> para **false**, e especifique as credenciais de logon do Assinante para os campos <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> .  
  
    -   Para especificar a Autenticação Integrada do Windows como o tipo de autenticação que o agente usa ao se conectar ao Publicador, defina o campo <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> da propriedade <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> para **true**.  
  
    -   Para especificar a Autenticação do SQL Server como o tipo de autenticação que o agente usa ao se conectar ao Publicador, defina o campo <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> da propriedade <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> para **false**, e especifique as credenciais de logon do Publicador para os campos <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardPassword%2A> .  
  
        > [!NOTE]  
        >  A conexão de agente para o Distribuidor sempre é feita usando as credenciais de Windows especificadas por <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>. Essa conta é também usada para fazer conexões remotas que usam a Autenticação do Windows.  
  
6.  (Opcional) Se você especificar um valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para confirmar as alterações no servidor. (Opcional) Se você especificar um valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (padrão), as alterações serão enviadas imediatamente ao servidor.  
  
#### <a name="to-change-the-login-information-used-by-an-immediate-updating-subscriber-when-it-connects-to-the-transactional-publisher"></a>Para alterar a informação de logon usada por um Assinante de atualização imediata ao se conectar ao publicador transacional  
  
1.  Crie uma conexão com o Assinante usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> para o banco de dados de assinatura. Especifique <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.Name%2A> e o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da Etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades de banco de dados na etapa 2 foram definidas incorretamente ou o banco de dados não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LinkPublicationForUpdateableSubscription%2A> , passando os parâmetros seguintes:  
  
    -   *Publisher* - o nome do Publicador.  
  
    -   *PublisherDB* - o nome do banco de dados de publicação.  
  
    -   *Publication* - o nome da publicação para a qual o Assinante de atualização imediata fez sua assinatura.  
  
    -   *Distributor* - o nome do Distribuidor.  
  
    -   *PublisherSecurity* - A <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext> objeto que especifica o tipo de modo de segurança usado pelo Assinante de atualização imediata ao se conectar ao Publicador e as credenciais de logon para a conexão.  
  
###  <a name="example-rmo"></a><a name="PShellExample"></a> Exemplo (RMO)  
 Este exemplo verifica o valor do logon fornecido e altera todas as senhas para o logon do Windows fornecido ou o logon do SQL Server armazenado por replicação no servidor.  
  
 [!code-cs[HowTo#rmo_ChangeServerPasswords](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changeserverpasswords)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeServerPasswords](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changeserverpasswords)]  
  
##  <a name="follow-up-after-you-modify-replication-security-settings"></a><a name="FollowUp"></a> Acompanhamento: depois de modificar configurações de segurança de replicação  
 Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
## <a name="see-also"></a>Consulte Também  
 [Replication Management Objects Concepts](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Atualizar scripts de replicação &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [Controle de acesso e identidade para replicação](../../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [Modelo de segurança do agente de replicação](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Exibir e modificar configurações de segurança de replicação](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
