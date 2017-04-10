---
title: "Exibir e modificar configura&#231;&#245;es de seguran&#231;a de replica&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modifying replication security settings"
  - "replication [SQL Server], security"
  - "security [SQL Server replication], viewing settings"
  - "viewing replication security settings"
  - "segurança [replicação do SQL Server], modificando configurações"
ms.assetid: 67d79532-1482-4de1-ac9f-4a23d162c85e
caps.latest.revision: 47
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 47
---
# Exibir e modificar configura&#231;&#245;es de seguran&#231;a de replica&#231;&#227;o
  Este tópico descreve como exibir e modificar configurações de segurança de replicação no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)], ou RMO (Replication Management Objects). Por exemplo, você pode querer alterar a conexão do Agente de Leitor de Log com o Publicador de uma autenticação do SQL Server para uma autenticação integrada do Windows ou alterar as credenciais usadas para executar um trabalho do agente quando a senha do Windows foi alterada. Para obter informações sobre as permissões necessárias para cada agente, consulte [modelo de segurança do agente de replicação](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para exibir e modificar configurações de segurança de replicação, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
-   **Acompanhamento:**  [Depois de modificar configurações de segurança de replicação](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Os procedimentos armazenados usados dependem do tipo de agente e do tipo de conexão de servidor.  
  
-   As classes e propriedades RMO que você usa dependem do tipo de agente e do tipo de conexão de servidor.  
  
###  <a name="Security"></a> Segurança  
 Por questões de segurança, os valores reais das senhas são mascarados em conjuntos de resultados retornados por procedimentos armazenados de replicação.  
  
####  <a name="Permissions"></a> Permissões  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Exiba e modifique as configurações de segurança nas seguintes caixas de diálogo:  
  
1.  A caixa de diálogo **Atualizar Senhas de Replicação** que está disponível na pasta **Replicação** do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Se você alterar a senha para uma conta do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou uma conta do Windows no servidor em uma topologia de replicação, use essa caixa de diálogo ao invés de atualizar a senha para cada agente que usa essa conta. Se agentes em mais de um servidor usam a mesma conta, você deverá conectar-se a cada servidor e alterar a senha. A senha será atualizada em todos os lugares em que a replicação usa a senha. A senha não é atualizada em outros lugares, como servidores vinculados.  
  
2.  O **segurança do agente** página o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
3.  O **Propriedades de assinatura - \< assinatura>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) e [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
4.  O **Propriedades do distribuidor - \< distribuidor>** e **Propriedades de banco de dados de distribuição - \< banco de dados>** caixas de diálogo. Para obter mais informações sobre como acessar essas caixas de diálogo, consulte [View and Modify Distributor and Publisher Properties](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
5.  O **Propriedades do publicador - \< publicador>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Distributor and Publisher Properties](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
#### Para alterar a senha para uma conta usada por um ou mais agentes  
  
1.  Se a conta for uma conta do SQL Server, essa caixa de diálogo também alterará a senha para a conta do SQL Server. Se a conta for uma conta de Windows, altere primeiro a senha no Windows. Para obter mais informações, consulte a documentação do Windows.  
  
    > [!NOTE]  
    >  Depois de alterar a senha de replicação de um agente, você deve parar e reiniciar cada agente que a usa para que a alteração entre em vigor para aquele agente.  
  
2.  Conecte-se ao servidor no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
3.  Clique com botão direito do **replicação** pasta e clique **Atualizar senhas de replicação**.  
  
4.  Na caixa de diálogo **Atualizar Senhas de Replicação** , especifique a conta e a nova senha.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para alterar as configurações de segurança do Snapshot Agent  
  
1.  No **segurança do agente** página do **Propriedades de publicação - \< publicação>** caixa de diálogo, clique o **as configurações de segurança** próximo ao **Snapshot Agent** caixa de texto.  
  
2.  Na caixa de diálogo **Segurança do Snapshot Agent** , especifique a conta sob a qual o agente deveria ser executado:  
  
    -   Digite uma nova conta de Windows na caixa de texto **Conta do Agent** .  
  
    -   Digite uma nova senha forte nas caixas de texto de **Senha** e **Confirmar senha** .  
  
3.  Especifique o contexto sob o qual o agente deveria se conectar do Distribuidor ao Publicador. Se você selecionar **Usando o seguinte logon do SQL Server**, você também terá que especificar o logon:  
  
    -   Digite um logon na caixa de texto **Logon**  
  
    -   Digite uma nova senha forte nas caixas de texto de **Senha** e **Confirmar senha** .  
  
    > [!NOTE]  
    >  Se o publicador é um editor Oracle, o contexto de conexão é especificado no **Propriedades do distribuidor - \< distribuidor>**caixa de diálogo. Veja a seguir o procedimento para alterar o contexto.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para alterar as configurações de segurança para o Log Reader Agent  
  
1.  No **segurança do agente** página do **Propriedades de publicação - \< publicação>** caixa de diálogo, clique o **as configurações de segurança** próximo ao **Log Reader Agent** caixa de texto.  
  
2.  Na caixa de diálogo **Segurança do Log Reader Agent** , especifique a conta sob a qual o agente deveria ser executado:  
  
    -   Digite uma nova conta de Windows na caixa de texto **Conta do Agent** .  
  
    -   Digite uma nova senha forte nas caixas de texto de **Senha** e **Confirmar senha** .  
  
3.  Especifique o contexto sob o qual o agente deveria se conectar do Distribuidor ao Publicador. Se você selecionar **Usando o seguinte logon do SQL Server**, você também terá que especificar o logon:  
  
    -   Digite um logon na caixa de texto **Logon**  
  
    -   Digite uma nova senha forte nas caixas de texto de **Senha** e **Confirmar senha** .  
  
    > [!NOTE]  
    >  Se o publicador é um editor Oracle, o contexto de conexão é especificado no **Propriedades do distribuidor - \< distribuidor>**caixa de diálogo. Altere o contexto usando o procedimento a seguir.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Há um Log Reader Agent para cada banco de dados publicado. A alteração das configurações de segurança para o agente para uma publicação afeta as configurações no banco de dados de publicação.  
  
#### Para alterar o contexto no qual o Snapshot Agent e o Log Reader Agent de um Editor Oracle fazem conexões com o Publicador  
  
1.  No **editores** página do **Propriedades do distribuidor - \< distribuidor>** caixa de diálogo, clique no botão Propriedades (**...**) próximo ao publicador.  
  
2.  Na seção **Conexão do Agente com o Publicador** , especifique o logon e a senha usados pelo esquema de usuário administrativo de replicação que você configurou. Para obter mais informações, consulte [Configurar um editor Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para alterar configurações de segurança do Distribution Agent para uma assinatura push  
  
1.  No **Propriedades de assinatura - \< assinatura>** caixa de diálogo no Editor, você pode fazer as seguintes alterações:  
  
    -   Para alterar a conta sob a qual o Distribution Agent executa e faz conexões com o distribuidor, clique o **conta de processo do agente** linha e, em seguida, clique em propriedades (**...**) botão na linha. Especifique uma conta e uma senha na caixa de diálogo **Segurança do Agente de Distribuição** .  
  
    -   Para alterar o contexto no qual o Distribution Agent se conecta ao assinante, clique o **conexão do assinante** linha e, em seguida, clique em propriedades (**...**) botão na linha. Especifique o contexto na caixa de diálogo **Inserir Informações de Conexão** .  
  
         Se você usar assinaturas de atualização enfileirada, o Queue Reader Agent também usará o contexto especificado aqui para conexões com o Assinante.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para alterar as configurações de segurança do Distribution Agent para uma assinatura pull  
  
1.  No **Propriedades de assinatura - \< assinatura>** caixa de diálogo no assinante, você pode fazer as seguintes alterações:  
  
    -   Para alterar a conta sob a qual o Distribution Agent executa e faz conexões com o assinante, clique o **conta de processo do agente** linha e, em seguida, clique em propriedades (**...**) botão na linha. Especifique uma conta e uma senha na caixa de diálogo **Segurança do Agente de Distribuição** .  
  
         Se você usar assinaturas de atualização enfileirada, o Queue Reader Agent também usará o contexto especificado aqui para conexões com o Assinante.  
  
    -   Para alterar o contexto no qual o Distribution Agent se conecta ao distribuidor, clique o **conexão do distribuidor** linha e, em seguida, clique em propriedades (**...**) botão na linha. Especifique o contexto na caixa de diálogo **Inserir Informações de Conexão** .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para alterar as configurações de segurança do Merge Agent para uma assinatura push  
  
1.  No **Propriedades de assinatura - \< assinatura>** caixa de diálogo no Editor, você pode fazer as seguintes alterações:  
  
    -   Para alterar a conta sob a qual o Merge Agent é executado e faz conexões com o Editor e distribuidor, clique o **conta de processo do agente** linha e, em seguida, clique em propriedades (**...**) botão na linha. Especifique a conta e a senha na caixa de diálogo **Segurança do Agente de Mesclagem** .  
  
    -   Para alterar o contexto no qual o Merge Agent se conecta ao assinante, clique o **conexão do assinante** linha e, em seguida, clique em propriedades (**...**) botão na linha. Especifique o contexto na caixa de diálogo **Inserir Informações de Conexão** .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para alterar as configurações de segurança do Merge Agent para uma assinatura pull  
  
1.  No **Propriedades de assinatura - \< assinatura>** caixa de diálogo no assinante, você pode fazer as seguintes alterações:  
  
    -   Para alterar a conta sob a qual o Merge Agent executa e faz conexões com o assinante, clique o **conta de processo do agente** linha e, em seguida, clique em propriedades (**...**) botão na linha. Especifique a conta e a senha na caixa de diálogo **Segurança do Agente de Mesclagem** .  
  
    -   Para alterar o contexto sob o qual o agente de mesclagem se conecta ao publicador e distribuidor, clique o **conexão do publicador** linha e, em seguida, clique em propriedades (**...**) botão na linha. Especifique o contexto na caixa de diálogo **Inserir Informações de Conexão** .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para alterar a conta sob a qual o Queue Reader Agent é executado  
  
1.  Na **geral** página o **Propriedades do distribuidor - \< distribuidor>** caixa de diálogo, clique em propriedades (**...**) botão ao lado do banco de dados de distribuição.  
  
2.  No **Propriedades de banco de dados de distribuição - \< banco de dados>** caixa de diálogo, clique o **configurações de segurança** próximo ao **conta de processo do agente** caixa de texto.  
  
3.  Na caixa de diálogo **Segurança do Queue Reader Agent** , especifique a conta na qual o agente é executado e efetua conexões com o Distribuidor.  
  
    -   Digite uma nova conta de Windows na caixa de texto **Conta de processo** .  
  
    -   Digite uma nova senha forte nas caixas de texto de **Senha** e **Confirmar senha** .  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Há um Agente de Leitor de Fila para cada banco de dados de distribuição. Alterar as configurações de segurança do agente afeta as configurações de todas as publicações em todos os Publicadores que usam esse banco de dados de distribuição.  
  
#### Para alterar o contexto sob a qual o Queue Reader Agent faz conexões com o Publicador  
  
1.  No **editores** página do **Propriedades do distribuidor - \< distribuidor>** caixa de diálogo, clique no botão Propriedades (**...**) próximo ao publicador.  
  
2.  Na seção **Conexão do Agente com o Publicador** , especifique o valor de **Representar a conta de processo do agente** ou **Autenticação do SQL Server** para a opção **Modo de Conexão de Agente** . Se você especificar a **Autenticação do SQL Server**, também digite os valores para **Logon** e **Senha**.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Há um Agente de Leitor de Fila para cada banco de dados de distribuição. Alterar as configurações de segurança do agente afeta as configurações de todas as publicações em todos os Publicadores que usam esse banco de dados de distribuição.  
  
#### Para alterar o contexto sob o qual o Queue Reader Agent faz conexões com o Assinante  
  
-   O Queue Reader Agent usa o mesmo contexto de conexão que o Distribution Agent para a assinatura. Para obter mais informações, veja os procedimentos acima para o Distribution Agent.  
  
#### Para alterar as configurações de segurança para uma assinatura pull de atualização imediata  
  
1.  No **Propriedades de assinatura - \< assinatura>** caixa de diálogo no assinante, clique o **conexão do publicador** linha e, em seguida, clique em propriedades (**...**) botão na linha.  
  
2.  Na caixa de diálogo **Inserir Informações de Conexão** , selecione uma das seguintes opções:  
  
    -   **Usar um logon de servidor vinculado ou remoto**. Selecione esta opção se você tiver definido um servidor remoto ou vinculado entre o assinante e o publicador usando [sp_addserver & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], ou outro método.  
  
    -   **Usar a Autenticação do SQL Server com estas informações de logon e senha**. Selecione essa opção se um servidor vinculado ou remoto entre o Assinante e o Publicador ainda não tiver sido definido. A replicação criará um servidor vinculado para você. É necessário que a conta especificada já exista no Publicador.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Esse procedimento altera o método utilizado pelos gatilhos de replicação para conexão do Assinante com o Publicador quando as alterações são feitas no Assinante. Você também pode alterar as configurações associadas com o Distribution Agent para uma assinatura de atualização imediata. Para obter mais informações, consulte os procedimentos descritos anteriormente neste tópico.  
>   
>  Este procedimento só se aplica às assinaturas pull. Para assinaturas push, use o procedimento armazenado [sp_link_publication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md).  
  
#### Para alterar a senha para a conexão administrativa do Publicador para o Distribuidor  
  
1.  No **editores** página do **Propriedades do distribuidor - \< distribuidor>** caixa de diálogo, digite uma senha forte no **senha** e **Confirmar senha** caixas de texto.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
3.  Na **geral** página do **Propriedades do publicador - \< publicador>** caixa de diálogo, digite uma senha forte no **senha** e **Confirmar senha** caixas de texto.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
> [!IMPORTANT]  
>  Em todos os procedimentos a seguir, quando possível, solicite aos usuários que digitem as credenciais de segurança em tempo de execução. Se armazenar credenciais em um arquivo de script, proteja o arquivo para evitar acesso não autorizado.  
  
#### Para alterar todas as instâncias de uma senha armazenada em um servidor de replicação  
  
1.  Em um servidor em uma topologia de replicação no banco de dados mestre, execute [sp_changereplicationserverpasswords](../../../relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql.md). Especifique a conta do Windows [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ou o logon para o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , cuja senha está sendo trocada por **@login** e uma nova senha para a conta ou logon de **@password**. Isso altera todas as instâncias da senha usada por todos os agentes no servidor quando em conexão com outros servidores da topologia.  
  
    > [!NOTE]  
    >  Para alterar somente o logon e a senha para conexão a um determinado servidor na topologia (como o distribuidor ou assinante), especifique o nome do servidor para **@server**.  
  
2.  Repita a Etapa 1 em todos servidores da topologia de replicação nos quais a senha precise ser atualizada.  
  
    > [!NOTE]  
    >  Depois de alterar a senha de replicação de um agente, você deve parar e reiniciar cada agente que a usa para que a alteração entre em vigor para aquele agente.  
  
#### Para alterar as configurações de segurança do Snapshot Agent  
  
1.  No publicador, execute [sp_helppublication_snapshot](../../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md), especificando **@publication**. Isso retorna as atuais configurações de segurança do Snapshot Agent.  
  
2.  No publicador, execute [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md), especificando **@publication** e uma ou mais das seguintes configurações de segurança para alterar:  
  
    -   Para alterar a conta do Windows sob a qual o agente é executado ou apenas a senha da conta, especifique **@job_login** e **@job_password**.  
  
    -   Para alterar o modo de segurança usado ao conectar-se ao publicador, especifique um valor de **1** ou **0** para **@publisher_security_mode**.  
  
    -   Ao alterar o modo de segurança usado ao conectar-se com o publicador de **1** para **0** ou ao alterar uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] logon usado para essa conexão, especifique **@publisher_login** e **@publisher_password**.  
  
    > [!IMPORTANT]  
    >  Ao configurar um editor com um distribuidor remoto, os valores fornecidos para todos os parâmetros, incluindo *job_login* e *job_password*, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, consulte [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
#### Para alterar as configurações de segurança para o Log Reader Agent  
  
1.  No publicador, execute [sp_helplogreader_agent](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md), especificando **@publisher**. Isso retorna as atuais configurações de segurança para o Log Reader Agent.  
  
2.  No publicador, execute [sp_changelogreader_agent](../../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md), especificando **@publication** e uma ou mais das seguintes configurações de segurança para alterar:  
  
    -   Para alterar a conta do Windows sob a qual o agente é executado ou apenas a senha da conta, especifique **@job_login** e **@job_password**.  
  
    -   Para alterar o modo de segurança usado ao conectar-se ao publicador, especifique um valor de **1** ou **0** para **@publisher_security_mode**.  
  
    -   Ao alterar o modo de segurança usado ao conectar-se com o publicador de **1** para **0** ou ao alterar uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] logon usado para essa conexão, especifique **@publisher_login** e **@publisher_password**.  
  
    > [!NOTE]  
    >  Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
    > [!IMPORTANT]  
    >  Ao configurar um editor com um distribuidor remoto, os valores fornecidos para todos os parâmetros, incluindo *job_login* e *job_password*, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, consulte [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
#### Para alterar configurações de segurança do Distribution Agent para uma assinatura push  
  
1.  No publicador do banco de dados de publicação, execute [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md), especificando **@publication** e **@subscriber**. Isso retorna propriedades de assinatura, inclusive configurações de segurança para o Distribution Agent em execução no Distribuidor.  
  
2.  No publicador do banco de dados de publicação, execute [sp_changesubscription](../../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md), especificando **@publication**, **@subscriber**, **@subscriber_db**, um valor de **todos os** para **@article**, o nome da propriedade de segurança para **@property**, e o novo valor da propriedade de **@value**.  
  
3.  Repita a Etapa 2, para cada uma das seguintes propriedades de segurança que forem alteradas:  
  
    -   Para alterar a conta do Windows na qual o agente é executado ou apenas a senha da conta, especifique um valor de **distrib_job_password** para **@property** e uma nova senha para **@value**. Ao alterar a conta em si, repita a etapa 2, especificando um valor de **distrib_job_login** para **@property** e a nova conta do Windows para **@value**.  
  
    -   Para alterar o modo de segurança usado ao conectar-se ao assinante, especifique um valor de **subscriber_security_mode** para **@property** e um valor de **1** (autenticação integrada do Windows) ou **0** (autenticação do SQL Server) para **@value**.  
  
    -   Ao alterar o modo de segurança do assinante para autenticação do SQL Server, ou se as informações de logon para autenticação do SQL Server, especifique um valor de **subscriber_password** para **@property** e a nova senha para **@value**. Repita a etapa 2, especificando um valor de **subscriber_login** para **@property** e um novo logon para **@value**.  
  
    > [!NOTE]  
    >  Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
    > [!IMPORTANT]  
    >  Ao configurar um editor com um distribuidor remoto, os valores fornecidos para todas as propriedades, incluindo **distrib_job_login** e **distrib_job_password**, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, consulte [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
#### Para alterar as configurações de segurança do Distribution Agent para uma assinatura pull  
  
1.  No assinante, execute [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md), especificando **@publication**. Isto retornará propriedades de assinatura, inclusive configurações de segurança para o Distribution Agent que é executado no Assinante.  
  
2.  No assinante no banco de dados de assinatura, execute [sp_change_subscription_properties](../../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md), especificando **@publisher**, **@publisher_db**, **@publication**, o nome da propriedade de segurança para **@property**, e o novo valor da propriedade de **@value**.  
  
3.  Repita a Etapa 2, para cada uma das seguintes propriedades de segurança que forem alteradas:  
  
    -   Para alterar a conta do Windows na qual o agente é executado ou apenas a senha da conta, especifique um valor de **distrib_job_password** para **@property** e uma nova senha para **@value**. Ao alterar a conta em si, repita a etapa 2, especificando um valor de **distrib_job_login** para **@property** e a nova conta do Windows para **@value**.  
  
    -   Para alterar o modo de segurança usado ao conectar-se ao distribuidor, especifique um valor de **distributor_security_mode** para **@property** e um valor de **1** (autenticação integrada do Windows) ou **0** (autenticação do SQL Server) para **@value**.  
  
    -   Ao alterar o modo de segurança do distribuidor para autenticação do SQL Server ou alterar informações de logon para autenticação do SQL Server, especifique um valor de **distributor_password** para **@property** e a nova senha para **@value**. Repita a etapa 2, especificando um valor de **distributor_login** para **@property** e um novo logon para **@value**.  
  
    > [!NOTE]  
    >  Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
#### Para alterar as configurações de segurança do Merge Agent para uma assinatura push  
  
1.  No publicador do banco de dados de publicação, execute [sp_helpmergesubscription](../../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md), especificando **@publication**, **@subscriber**, e **@subscriber_db**. Isto retorna propriedades de assinatura, inclusive configurações de segurança para o Merge Agent em execução no Distribuidor.  
  
2.  No publicador do banco de dados de publicação, execute [sp_changemergesubscription](../../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md), especificando **@publication**, **@subscriber**, **@subscriber_db**, o nome da propriedade de segurança para **@property**, e o novo valor da propriedade de **@value**.  
  
3.  Repita a Etapa 2, para cada uma das seguintes propriedades de segurança que forem alteradas:  
  
    -   Para alterar a conta do Windows na qual o agente é executado, ou apenas a senha da conta, especifique um valor de **merge_job_password** para **@property** e uma nova senha para **@value**. Ao alterar a conta em si, repita a etapa 2, especificando um valor de **merge_job_login** para **@property** e a nova conta do Windows para **@value**.  
  
    -   Para alterar o modo de segurança usado ao conectar-se ao assinante, especifique um valor de **subscriber_security_mode** para **@property** e um valor de **1** (autenticação integrada do Windows) ou **0** (autenticação do SQL Server) para **@value**.  
  
    -   Ao alterar o modo de segurança do assinante para autenticação do SQL Server, ou se as informações de logon para autenticação do SQL Server, especifique um valor de **subscriber_password** para **@property** e a nova senha para **@value**. Repita a etapa 2, especificando um valor de **subscriber_login** para **@property** e um novo logon para **@value**.  
  
    -   Para alterar o modo de segurança usado ao conectar-se ao publicador, especifique um valor de **publisher_security_mode** para **@property** e um valor de **1** (autenticação integrada do Windows) ou **0** (autenticação do SQL Server) para **@value**.  
  
    -   Ao alterar o modo de segurança do publicador para autenticação do SQL Server, ou se as informações de logon para autenticação do SQL Server, especifique um valor de **publisher_password** para **@property** e a nova senha para **@value**. Repita a etapa 2, especificando um valor de **publisher_login** para **@property** e um novo logon para **@value**.  
  
    > [!NOTE]  
    >  Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
    > [!IMPORTANT]  
    >  Ao configurar um editor com um distribuidor remoto, os valores fornecidos para todas as propriedades, incluindo **merge_job_login** e **merge_job_password**, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, consulte [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
#### Para alterar as configurações de segurança do Merge Agent para uma assinatura pull  
  
1.  No assinante, execute [sp_helpmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md), especificando **@publication**. Isso retornará propriedades de assinatura, inclusive configurações de segurança para o Merge Agent que executa no Assinante.  
  
2.  No assinante no banco de dados de assinatura, execute [sp_change_subscription_properties](../../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md), especificando **@publisher**, **@publisher_db**, **@publication**, o nome da propriedade de segurança para **@property**, e o novo valor da propriedade de **@value**.  
  
3.  Repita a Etapa 2, para cada uma das seguintes propriedades de segurança que forem alteradas:  
  
    -   Para alterar a conta do Windows na qual o agente é executado ou apenas a senha da conta, especifique um valor de **merge_job_password** para **@property** e a nova senha para **@value**. Ao alterar a conta em si, repita a etapa 2, especificando um valor de **merge_job_login** para **@property** e a nova conta do Windows para **@value**.  
  
    -   Para alterar o modo de segurança usado ao conectar-se ao distribuidor, especifique um valor de **distributor_security_mode** para **@property** e um valor de **1** (autenticação integrada do Windows) ou **0** (autenticação do SQL Server) para **@value**.  
  
    -   Ao alterar o modo de segurança do distribuidor para autenticação do SQL Server ou alterar informações de logon para autenticação do SQL Server, especifique um valor de **distributor_password** para **@property** e a nova senha para **@value**. Repita a etapa 2, especificando um valor de **distributor_login** para **@property** e um novo logon para **@value**.  
  
    -   Para alterar o modo de segurança usado ao conectar-se ao publicador, especifique um valor de **publisher_security_mode** para **@property** e um valor de **1** (autenticação integrada do Windows) ou **0** (autenticação do SQL Server) para **@value**.  
  
    -   Ao alterar o modo de segurança do publicador para autenticação do SQL Server ou alterar informações de logon para autenticação do SQL Server, especifique um valor de **publisher_password** para **@property** e a nova senha para **@value**. Repita a etapa 2, especificando um valor de **publisher_login** para **@property** e um novo logon para **@value**.  
  
    > [!NOTE]  
    >  Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
#### Para alterar configurações de segurança para o Snapshot Agent para gerar um instantâneo filtrado para um Assinante  
  
1.  No publicador, execute [sp_helpdynamicsnapshot_job](../../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md), especificando **@publication**. No resultado definido, observe o valor de **job_name** para a partição do assinante alterar.  
  
2.  No publicador, execute [sp_changedynamicsnapshot_job](../../../relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql.md), especificando **@publication**, o valor obtido na etapa 1 para **@dynamic_snapshot_jobname**, e uma nova senha para **@job_password** ou logon e senha para a conta do Windows sob a qual o agente é executado para **@job_login** e **@job_password**.  
  
    > [!IMPORTANT]  
    >  Ao configurar um editor com um distribuidor remoto, os valores fornecidos para todos os parâmetros, incluindo *job_login* e *job_password*, são enviados ao distribuidor como texto sem formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, consulte [Habilitar conexões criptografadas para o mecanismo de banco de dados e 40; SQL Server Configuration Manager & 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
#### Para alterar as configurações de segurança para o Queue Reader Agent  
  
1.  No distribuidor, execute [sp_helpqreader_agent](../../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md). Isso retorna a conta do atual em que o Queue Reader Agent é executado.  
  
    -   No distribuidor, execute [sp_changeqreader_agent](../../../relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql.md), especificando as configurações de conta do Windows para **@job_login** e **@job_passwsord**.  
  
    > [!NOTE]  
    >  Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor. Há um Agente de Leitor de Fila para cada banco de dados de distribuição. Alterar as configurações de segurança do agente afeta as configurações de todas as publicações em todos os Publicadores que usam esse banco de dados de distribuição.  
  
2.  O Queue Reader Agent faz conexões com o Assinante usando o mesmo contexto de conexão do Distribution Agent para a assinatura.  
  
#### Para alterar modo de segurança usado por um Assinante de atualização imediato durante conexão com o Publicador  
  
1.  No assinante no banco de dados de assinatura, execute [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md). Especifique **@publisher**, **@publication**, o nome do banco de dados de publicação para **@publisher_db**, e um dos seguintes valores para **@security_mode**:  
  
    -   **0** para usar a Autenticação do SQL Server ao fazer atualizações no Publicador. Essa opção requer a especificação de um logon válido no Publicador para **@login** e **@password**.  
  
    -   **1** para usar o contexto de segurança do usuário que faz alterações no Assinante durante conexão com o Assinante. Consulte [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) para restrições relacionadas a esse modo de segurança.  
  
    -   **2** para usar um existente, definido pelo usuário vinculado logon de servidor criado usando [sp_addlinkedserver & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
#### Para alterar a senha de um Distribuidor remoto  
  
1.  No distribuidor no banco de dados de distribuição, execute [sp_changedistributor_password](../../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md), especificando a nova senha para esse logon para **@password**.  
  
    > [!IMPORTANT]  
    >  Não altere a senha para **distributor_admin** diretamente.  
  
2.  Em todos os publicadores que usam esse distribuidor remoto, execute [sp_changedistributor_password](../../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md), especificando a senha da etapa 1 para **@password**.  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os serviços [criptográficos](http://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework do Windows.  
  
#### Para alterar todas as instâncias de uma senha armazenada em um servidor de replicação  
  
1.  Criar uma conexão com o servidor de replicação usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.ReplicationServer> classe usando a conexão da etapa 1.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeReplicationServerPasswords%2A> método. Especifique os seguintes parâmetros:  
  
    -   *security_mode* - uma <xref:Microsoft.SqlServer.Replication.ReplicationSecurityMode> valor que especifica o tipo de autenticação para o qual todas as instâncias da senha estão sendo alteradas.  
  
    -   *logon* -o logon para que todas as instâncias da senha estão sendo alteradas.  
  
    -   *senha* -o novo valor de senha.  
  
        > [!IMPORTANT]  
        >  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for preciso armazenar credenciais, use os [serviços criptográficos](http://go.microsoft.com/fwlink/?LinkId=34733) fornecidos pelo Windows .NET Framework.  
  
        > [!NOTE]  
        >  Somente um membro do **sysadmin** função de servidor fixa pode chamar esse método.  
  
4.  Repita as Etapas 1-3 em todo servidor, na topologia de replicação, onde a senha deve ser atualizada.  
  
#### Para alterar as configurações de segurança para o Distribution Agent de uma assinatura push para uma publicação transacional  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransSubscription> classe.  
  
3.  Definir o <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, e <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> Propriedades para a assinatura e defina a conexão da etapa 1 para o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades da assinatura na etapa 3 foram definidas incorretamente ou a assinatura não existe.  
  
5.  Defina uma ou mais das seguintes propriedades de segurança na instância do <xref:Microsoft.SqlServer.Replication.TransSubscription>:  
  
    -   Para alterar as credenciais da conta do Windows sob a qual o agente é executado, defina o <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> campos de <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>.  
  
    -   Para especificar a autenticação integrada do Windows como o tipo de autenticação que o agente usa ao se conectar ao assinante, defina o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo o <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> propriedade **true**.  
  
    -   Para especificar a autenticação do SQL Server como o tipo de autenticação que o agente usa ao se conectar ao assinante, defina o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo o <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> propriedade **false**, e especifique as credenciais de logon do assinante para o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> campos.  
  
        > [!NOTE]  
        >  A conexão do agente para o distribuidor sempre é feita usando as credenciais do Windows especificadas por <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>. Essa conta é também usada para fazer conexões remotas que usam a Autenticação do Windows.  
  
6.  (Opcional) Se você tiver especificado um valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar as alterações no servidor. Se você tiver especificado um valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (o padrão), as alterações serão enviadas para o servidor imediatamente.  
  
#### Para alterar as configurações de segurança para o Distribution Agent de uma assinatura pull para uma publicação transacional  
  
1.  Criar uma conexão com o assinante usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.TransPullSubscription> classe.  
  
3.  Definir o <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, e <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> Propriedades para a assinatura e defina a conexão da etapa 1 para o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades da assinatura na etapa 3 foram definidas incorretamente ou a assinatura não existe.  
  
5.  Defina uma ou mais das seguintes propriedades de segurança na instância do <xref:Microsoft.SqlServer.Replication.TransPullSubscription>:  
  
    -   Para alterar as credenciais da conta do Windows sob a qual o agente é executado, defina o <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> campos de <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>.  
  
    -   Para especificar a autenticação integrada do Windows como o tipo de autenticação que o agente usa ao se conectar ao distribuidor, defina o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo o <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> propriedade **true**.  
  
    -   Para especificar a autenticação do SQL Server como o tipo de autenticação que o agente usa ao se conectar ao distribuidor, defina o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo o <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> propriedade **false**, e especifique as credenciais de logon do distribuidor para o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> campos.  
  
        > [!NOTE]  
        >  A conexão do agente para o assinante sempre é feita usando as credenciais do Windows especificadas por <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>. Essa conta é também usada para fazer conexões remotas que usam a Autenticação do Windows.  
  
6.  (Opcional) Se você tiver especificado um valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar as alterações no servidor. Se você tiver especificado um valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (o padrão), as alterações serão enviadas para o servidor imediatamente.  
  
#### Para alterar as configurações de segurança para o Merge Agent para uma assinatura pull para uma publicação de mesclagem  
  
1.  Criar uma conexão com o assinante usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergePullSubscription> classe.  
  
3.  Definir o <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, e <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> Propriedades para a assinatura e defina a conexão da etapa 1 para o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades da assinatura na etapa 3 foram definidas incorretamente ou a assinatura não existe.  
  
5.  Defina uma ou mais das seguintes propriedades de segurança na instância do <xref:Microsoft.SqlServer.Replication.MergePullSubscription>:  
  
    -   Para alterar as credenciais da conta do Windows sob a qual o agente é executado, defina o <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> campos de <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>.  
  
    -   Para especificar a autenticação integrada do Windows como o tipo de autenticação que o agente usa ao se conectar ao distribuidor, defina o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo o <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> propriedade **true**.  
  
    -   Para especificar a autenticação do SQL Server como o tipo de autenticação que o agente usa ao se conectar ao distribuidor, defina o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo o <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> propriedade **false**, e especifique as credenciais de logon do distribuidor para o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> campos.  
  
    -   Para especificar a autenticação integrada do Windows como o tipo de autenticação que o agente usa ao se conectar ao publicador, defina o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo o <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> propriedade **true**.  
  
    -   Para especificar a autenticação do SQL Server como o tipo de autenticação que o agente usa ao se conectar ao publicador, defina o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo o <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> propriedade **false**, e especifique as credenciais de logon do publicador para o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> campos.  
  
        > [!NOTE]  
        >  A conexão do agente para o assinante sempre é feita usando as credenciais do Windows especificadas por <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>. Essa conta é também usada para fazer conexões remotas que usam a Autenticação do Windows.  
  
6.  (Opcional) Se você tiver especificado um valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar as alterações no servidor. Se você tiver especificado um valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (o padrão), as alterações serão enviadas para o servidor imediatamente.  
  
#### Para alterar as configurações de segurança para o Merge Agent para uma assinatura push para uma publicação de mesclagem  
  
1.  Criar uma conexão com o publicador usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.MergeSubscription> classe.  
  
3.  Definir o <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, e <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> Propriedades para a assinatura e defina a conexão da etapa 1 para o <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades da assinatura na etapa 3 foram definidas incorretamente ou a assinatura não existe.  
  
5.  Defina uma ou mais das seguintes propriedades de segurança na instância do <xref:Microsoft.SqlServer.Replication.MergeSubscription>:  
  
    -   Para alterar as credenciais da conta do Windows sob a qual o agente é executado, defina o <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> campos de <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>.  
  
    -   Para especificar a autenticação integrada do Windows como o tipo de autenticação que o agente usa ao se conectar ao assinante, defina o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo o <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> propriedade **true**.  
  
    -   Para especificar a autenticação do SQL Server como o tipo de autenticação que o agente usa ao se conectar ao assinante, defina o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo o <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> propriedade **false**, e especifique as credenciais de logon do assinante para o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> campos.  
  
    -   Para especificar a autenticação integrada do Windows como o tipo de autenticação que o agente usa ao se conectar ao publicador, defina o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo o <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> propriedade **true**.  
  
    -   Para especificar a autenticação do SQL Server como o tipo de autenticação que o agente usa ao se conectar ao publicador, defina o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> campo o <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> propriedade **false**, e especifique as credenciais de logon do publicador para o <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardLogin%2A> e <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardPassword%2A> campos.  
  
        > [!NOTE]  
        >  A conexão do agente para o distribuidor sempre é feita usando as credenciais do Windows especificadas por <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>. Essa conta é também usada para fazer conexões remotas que usam a Autenticação do Windows.  
  
6.  (Opcional) Se você tiver especificado um valor de **true** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, chame o <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar as alterações no servidor. Se você tiver especificado um valor de **false** para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (o padrão), as alterações serão enviadas para o servidor imediatamente.  
  
#### Para alterar a informação de logon usada por um Assinante de atualização imediata ao se conectar ao publicador transacional  
  
1.  Criar uma conexão com o assinante usando o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> classe.  
  
2.  Criar uma instância do <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> classe para o banco de dados de assinatura. Especifique <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.Name%2A> e o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obter as propriedades do objeto. Se esse método retornar **false**, as propriedades do banco de dados na etapa 2 foram definidas incorretamente ou o banco de dados de assinatura não existe.  
  
4.  Chamar o <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LinkPublicationForUpdateableSubscription%2A> método, passando os seguintes parâmetros:  
  
    -   *O Publisher* -o nome do publicador.  
  
    -   *PublisherDB* -o nome do banco de dados de publicação.  
  
    -   *Publicação* - o nome da publicação à qual pertence o assinante de atualização imediato.  
  
    -   *Distribuidor* -o nome do distribuidor.  
  
    -   *PublisherSecurity* - uma <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext> objeto que especifica o tipo de modo de segurança usado pelo assinante de atualização imediata durante a conexão com as publicador e credenciais de logon para a conexão.  
  
###  <a name="PShellExample"></a> Exemplo (RMO)  
 Este exemplo verifica o valor do logon fornecido e altera todas as senhas para o logon do Windows fornecido ou o logon do SQL Server armazenado por replicação no servidor.  
  
 [!code-csharp[HowTo#rmo_ChangeServerPasswords](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changeserverpasswords)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeServerPasswords](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changeserverpasswords)]  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de modificar configurações de segurança de replicação  
 Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
## Consulte também  
 [Conceitos de Replication Management Objects](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Atualizar Scripts de replicação & #40. Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [Gerenciar logons e senhas na replicação](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de segurança do agente de replicação](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Práticas recomendadas em relação à segurança de replicação](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Segurança e proteção e 40; Replicação e 41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  