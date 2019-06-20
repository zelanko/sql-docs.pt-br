---
title: Criar uma assinatura para um assinante que não é do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], non-SQL Server Subscribers
- Subscribers [SQL Server replication], non-SQL Server Subscribers
- non-SQL Server Subscribers, subscriptions
ms.assetid: 5020ee68-b988-4d57-8066-67d183e61237
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: be2568e0a99ff21280388bd309a1e49bdec7e072
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721668"
---
# <a name="create-a-subscription-for-a-non-sql-server-subscriber"></a>Criar uma assinatura para um Assinante não SQL Server
  Este tópico descreve como criar uma assinatura para um Assinante não SQL Server no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)]. Dados de publicação de suporte a replicação transacional e de instantâneo para Assinantes não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações sobre plataformas de Assinantes com suporte, consulte [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md).  
  
 **Neste tópico**  
  
-   **Para criar uma assinatura para um Assinante não SQL Server, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Para criar uma assinatura para um Assinante não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
1.  Instale e configure o software de cliente Oracle e o provedor OLE DB apropriados no Distribuidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Oracle Subscribers](non-sql/oracle-subscribers.md) e [IBM DB2 Subscribers](non-sql/ibm-db2-subscribers.md).  
  
2.  Crie uma publicação usando o Assistente para Nova Publicação. Para obter mais informações sobre a criação de publicações, consulte [Create a Publication](publish/create-a-publication.md) (Criar uma publicação) e [Criar uma publicação de um banco de dados Oracle](publish/create-a-publication-from-an-oracle-database.md). Especifique as opções a seguir no Assistente para Nova Publicação:  
  
    -   Na página **Tipo de Publicação** , selecione **Publicação de Instantâneo** ou **Publicação Transacional**.  
  
    -   Na página **Snapshot Agent** , desmarque **Criar um instantâneo imediatamente.**  
  
         Você cria o instantâneo após a publicação estar habilitada para Assinantes não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para garantir que o Snapshot Agent gere scripts de instantâneo e de inicialização adequados para os Assinantes não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
3.  Habilite a publicação para Assinantes não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a caixa de diálogo **Propriedades da Publicação – \<PublicationName>** . Consulte [Publication Properties, Subscription Options](publication-properties-subscription-options.md) para obter mais informações sobre essa etapa.  
  
4.  Crie uma assinatura usando o Assistente para Nova Assinatura. Esse tópico proporciona mais informações sobre essa etapa.  
  
5.  (Opcional) Altere a propriedade do artigo **de pre_creation_cmd** para reter as tabelas no Assinante. Esse tópico proporciona mais informações sobre essa etapa.  
  
6.  Gere um instantâneo para a publicação. Esse tópico proporciona mais informações sobre essa etapa.  
  
7.  Sincronize a assinatura. Para obter mais informações, consulte [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
#### <a name="to-enable-a-publication-for-non-sql-server-subscribers"></a>Para habilitar uma publicação para Assinantes não SQL Server  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó de servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com o botão direito do mouse na publicação, em clique em **Propriedades**.  
  
4.  Na página **Opções de Assinatura** , selecione um valor de **Verdadeiro** para a opção **Permitir Assinantes não SQL Server**. A seleção dessa opção altera várias propriedades de forma que a publicação seja compatível com Assinantes não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    > [!NOTE]  
    >  Selecionando **Verdadeiro** define o valor da propriedade do artigo **pre_creation_cmd** para 'descartar'. Essa definição especifica que a replicação deve descartar uma tabela no Assinante se coincidir com o nome de tabela no artigo. Se tiver tabelas existentes no Assinante que deseja manter, use o procedimento armazenado [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql) para cada artigo, especifique o valor 'nenhum' para **pre_creation_cmd**: `sp_changearticle @publication= 'MyPublication', @article= 'MyArticle', @property='pre_creation_cmd', @value='none'`.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Você será solicitado a criar um novo instantâneo para a publicação. Se não quiser criar um neste momento, use mais tarde as etapas descritas no próximo procedimento “Como”.  
  
#### <a name="to-create-a-subscription-for-a-non-sql-server-subscriber"></a>Para criar uma assinatura para um Assinante não SQL Server  
  
1.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
2.  Clique com o botão direito do mouse em uma publicação adequada e clique em **Novas Assinaturas**.  
  
3.  Na página **Local do Distribution Agent** , certifique-se de que **Executar todos os agentes no Distribuidor** esteja selecionado. Assinantes não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não têm suporte para os agentes executando no Assinante.  
  
4.  Na página **Assinantes** , clique em **Adicionar Assinante** e clique em **Adicionar Assinante não SQL Server**.  
  
5.  Na caixa de diálogo **Adicionar Assinante Não SQL Server** , selecione o tipo de Assinante.  
  
6.  Digite um valor no **Nome da fonte de dados**:  
  
    -   Para o Oracle, esse é o nome do substrato transparente de rede (TNS) que você configurou.  
  
    -   Para a IBM, esse pode ser qualquer nome. É comum especificar o endereço de rede do Assinante.  
  
     O nome da fonte de dados digitado nesta etapa e as credenciais especificadas na etapa 9 não são validados por este assistente. Não são usados pela replicação até que o Distribution Agent execute para uma assinatura. Certifique-se de que todos os valores tenham sido testados por meio de conexão ao Assinante usando uma ferramenta de cliente (como **sqlplus** para o Oracle). Para obter mais informações, consulte [Oracle Subscribers](non-sql/oracle-subscribers.md) e [IBM DB2 Subscribers](non-sql/ibm-db2-subscribers.md).  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Na página **Assinantes** do assistente, o Assinante é agora exibido na coluna **Assinante** com um somente leitura **(destino padrão)** na coluna **Banco de Dados da Assinatura** :  
  
    -   Para o Oracle, um servidor tem, no máximo, um banco de dados, assim não é necessário especificar o banco de dados.  
  
    -   Para a IBM DB2, o banco de dados é especificado na propriedade **Catálogo Inicial** da cadeia de caracteres da conexão DB2, que pode ser digitada no campo **Opções de conexões adicionais** descrito mais adiante neste processo.  
  
8.  Na página **Segurança do Agente de Distribuição**, clique no botão de propriedades ( **...** ) próximo ao Assinante para acessar a caixa de diálogo **Segurança do Agente de Distribuição**.  
  
9. Na caixa de diálogo **Segurança do Distribution Agent** :  
  
    -   Nos campos **Processar conta**, **Senha**e **Confirmar senha** , digite a conta e a senha do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows sob as quais o Distribution Agent deve executar e realizar conexões locais ao Distribuidor.  
  
         A conta requer, no mínimo, as seguintes permissões: membro da função de banco de dados fixa **db_owner** no banco de dados de distribuição, membro da lista de acesso à publicação (PAL); permissões de leitura no compartilhamento do instantâneo e permissão de leitura no diretório instalado do provedor OLE DB. Para obter mais informações sobre a PAL, consulte [Secure the Publisher](security/secure-the-publisher.md) (Proteger o publicador).  
  
    -   No **Conectar ao Assinante**, nos campos **Logon**, **Senha**e **Confirmar senha** , digite o logon e a senha que devem ser usados para se conectar ao Assinante. Esse logon já deverá estar configurado e ter permissões suficientes para criar objetos no banco de dados de assinatura.  
  
    -   No campo **Opções de conexões adicionais** , especifique as opções de conexão para o Assinante na forma de uma cadeia de caracteres para conexão (Oracle não necessita de opções adicionais). Cada opção deverá estar separada por um ponto-e-vírgula. A seguir um exemplo de uma cadeia de conexão DB2 (as quebras de linha são para facilitar a leitura):  
  
        ```  
        Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
        PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
        Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
        Persist Security Info=False;Connection Pooling=True;  
        ```  
  
         A maioria das opções na cadeia de caracteres é específica do servidor DB2 que você está configurando, mas a opção **Processar Binário como Caractere** sempre deve ser definida como **False**. Um valor é necessário para a opção **Catálogo Inicial** para identificar o banco de dados de assinatura.  
  
10. Na página **Agenda de Sincronização** , selecione uma agenda para o Distribution Agent no menu **Agenda do Agente** (a agenda é tipicamente **Executar continuamente**).  
  
11. Na página **Inicializar Assinaturas** , especifique se a assinatura deve ser inicializada e caso positivo, onde deve ser inicializada.  
  
    -   Desmarque **Inicializar** só se você criou todos os objetos e adicionou todos os dados necessários no banco de dados de assinatura.  
  
    -   Selecione **Imediatamente** na lista suspensa na coluna **Inicializar Quando** para que o Distribution Agent transfira os arquivos de instantâneos para o Assinante após a conclusão desse assistente. Selecione **Na primeira sincronização** para que o agente transfira os arquivos da próxima vez em que for agendado para executar.  
  
12. Na página **Ações do Assistente** , opcionalmente faça o script da assinatura. Para obter mais informações, consulte [Scripting Replication](scripting-replication.md).  
  
#### <a name="to-retain-tables-at-the-subscriber"></a>Para reter tabelas no Assinante  
  
-   Por padrão, habilitando uma publicação para Assinantes não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define o valor da propriedade do artigo **de pre_creation_cmd** para 'descartar' Essa definição especifica que a replicação deve descartar uma tabela no Assinante se coincidir com o nome de tabela no artigo. Se tiver tabelas existentes no Assinante que deseja manter, use o procedimento armazenado [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql) para cada artigo, especifique um valor 'nenhum' para **pre_creation_cmd**. `sp_changearticle @publication= 'MyPublication', @article= 'MyArticle', @property='pre_creation_cmd', @value='none'`.  
  
#### <a name="to-generate-a-snapshot-for-the-publication"></a>Para gerar um instantâneo para a publicação  
  
1.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
2.  Clique com o botão direito do mouse em uma publicação e clique em **Exibir Status do Snapshot Agent**.  
  
3.  Na caixa de diálogo **Exibir Status do Snapshot Agent – \<Publicação>** , clique em **Iniciar**.  
  
 Quando o Agente de Instantâneo terminar de gerar o instantâneo, uma mensagem será exibida, como "[100%] Um instantâneo de 17 artigos foi gerado".  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Crie assinaturas push para Assinantes não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de forma programática, usando procedimentos armazenados de replicação.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
#### <a name="to-create-a-push-subscription-for-a-transactional-or-snapshot-publication-to-a-non-sql-server-subscriber"></a>Para criar uma assinatura push para uma publicação transacional ou de instantâneo para um assinante não SQL Server  
  
1.  Instale o mais recente provedor OLE DB para o Assinante não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Publicador e no Distribuidor. Para os requisitos de replicação de um fornecedor OLE DB, consulte [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md), [Oracle Subscribers](non-sql/oracle-subscribers.md), [IBM DB2 Subscribers](non-sql/ibm-db2-subscribers.md).  
  
2.  No Publicador do banco de dados de publicação, verifique se a publicação dá suporte a assinantes não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], executando [sp_helppublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql).  
  
    -   Se o valor de `enabled_for_het_sub` for 1, os Assinantes não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] terão suporte.  
  
    -   Se o valor de `enabled_for_het_sub` é 0, execute [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql), especificando `enabled_for_het_sub` para **@property** e `true` para  **@value** .  
  
        > [!NOTE]  
        >  Antes de alterar `enabled_for_het_sub` para `true`, é preciso ignorar todas as assinaturas existentes para a publicação. Não é possível definir  `enabled_for_het_sub` como `true` quando a publicação oferecer suporte também a assinaturas de atualização. Alterar `enabled_for_het_sub` afetará outras propriedades de publicação. Para obter mais informações, consulte [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md).  
  
3.  No Publicador do banco de dados de publicação, execute [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Especifique **@publication** , **@subscriber** ; um valor de **(destino padrão)** para **@destination_db** ; um valor de **push** para **@subscription_type** , e um valor de 3 para **@subscriber_type** (especifica um provedor OLE DB).  
  
4.  No Publicador do banco de dados de publicação, execute [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql). Especifique o seguinte:  
  
    -   Os parâmetros **@subscriber** e **@publication** .  
  
    -   Um valor de **(destino padrão)** para **@subscriber_db** ,  
  
    -   As propriedades de fonte de dados não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para **@subscriber_provider** , **@subscriber_datasrc** , **@subscriber_location** , **@subscriber_provider_string** e **@subscriber_catalog** .  
  
    -   Os parâmetros [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows com as quais o Distribution Agent do Distribuidor é executado para **@job_login** e **@job_password** .  
  
        > [!NOTE]  
        >  As conexões realizadas com Autenticação Integrada do Windows sempre usam as credenciais do Windows especificadas por **@job_login** e **@job_password** . O Distribution Agent sempre faz a conexão local com o Distribuidor usando a Autenticação Integrada do Windows. Por padrão, o agente se conecta ao Assinante usando a Autenticação Integrada do Windows.  
  
    -   Um valor de **0** para **@subscriber_security_mode** e informações de logon do provedor OLE DB para **@subscriber_login** e **@subscriber_password** .  
  
    -   Agenda para o trabalho do Distribution Agent para essa assinatura. Para obter mais informações, consulte [Specify Synchronization Schedules](specify-synchronization-schedules.md).  
  
    > [!IMPORTANT]  
    >  Ao criar uma assinatura push em um Publicador com um Distribuidor remoto, os valores especificados para todos os parâmetros, inclusive *job_login* e *job_password*são enviados para o Distribuidor como texto sem-formatação. Você deve criptografar a conexão entre o Publicador e seu Distribuidor remoto antes de executar esse procedimento armazenado. Para obter mais informações, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
## <a name="see-also"></a>Consulte também  
 [IBM DB2 Subscribers](non-sql/ibm-db2-subscribers.md)   
 [Oracle Subscribers](non-sql/oracle-subscribers.md)   
 [Outros assinantes não SQL Server](non-sql/other-non-sql-server-subscribers.md)   
 [Replication System Stored Procedures Concepts](concepts/replication-system-stored-procedures-concepts.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)  
  
  
