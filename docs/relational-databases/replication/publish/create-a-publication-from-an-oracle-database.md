---
title: "Criar uma publica&#231;&#227;o de um banco de dados Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "publications [SQL Server replication], Oracle databases"
  - "publicação Oracle [replicação do SQL Server], configurando"
ms.assetid: b3812746-14b0-4b22-809e-b4a95e1c8083
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Criar uma publica&#231;&#227;o de um banco de dados Oracle
  Este tópico descreve como criar uma publicação no a partir de um banco de dados Oracle no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Pré-requisitos](#Prerequisites)  
  
-   **Para criar uma publicação de um banco de dados Oracle usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Antes de criar uma publicação, você deve instalar o software Oracle no Distribuidor do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , além de configurar o banco de dados Oracle. Para obter mais informações, consulte [Configurar um editor Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Crie uma publicação de instantâneo ou transacional a partir de um banco de dados Oracle com o Assistente de Nova Publicação.  
  
 A primeira vez que você cria uma publicação de um banco de dados Oracle, você deve identificar o Editor Oracle no Distribuidor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (não é necessário fazer isso em publicações subsequentes do mesmo banco de dados). Identificação do editor Oracle pode ser realizada de Assistente de nova publicação ou o **Propriedades do distribuidor - \< distribuidor>** caixa de diálogo; Este tópico mostra o **Propriedades do distribuidor - \< distribuidor>** caixa de diálogo.  
  
#### Para identificar o Editor Oracle no Distribuidor do SQL Server  
  
1.  No [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que o Editor Oracle usará como Distribuidor e, então, expanda o nó do servidor.  
  
2.  Clique com botão direito do **replicação** pasta e clique **Propriedades do distribuidor**.  
  
3.  No **editores** página do **Propriedades do distribuidor - \< distribuidor>** caixa de diálogo, clique em **Add**, e, em seguida, clique em **Adicionar editor Oracle**.  
  
4.  Na caixa de diálogo **Conectar ao Servidor** , clique no botão **Opções** .  
  
5.  Na guia **Logon** :  
  
    1.  Insira o nome da instância do banco de dados Oracle ou selecione **Procurar mais** na caixa de combinação **Instância do servidor** .  
  
    2.  Selecione **autenticação padrão Oracle** (recomendado) ou **a autenticação do Windows**.  
  
         Se você selecionar **autenticação do Windows**: o servidor Oracle deve ser configurado para permitir conexões usando credenciais do Windows (para obter mais informações, consulte a documentação do Oracle); e você deve estar conectado no momento com o mesmo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] conta do Windows especificada para o esquema de usuário administrativo de replicação.  
  
    3.  Se você selecionou **Autenticação Padrão da Oracle**, insira o logon e a senha do esquema de usuário administrativo de replicação que você criou no Editor Oracle durante a configuração.  
  
6.  Na guia **Propriedades de Conexão** , selecione um tipo de Publicador de **Gateway** ou **Completo**.  
  
     A opção **Complete** é projetada para fornecer publicações transacionais e de instantâneo com o conjunto completo de recursos com suporte para publicações Oracle. A opção **Gateway** fornece otimizações de projeto específicas para aprimorar o desempenho de casos em que a replicação serve como um gateway entre sistemas. A opção **Gateway** não poderá ser usada se você planejar publicar a mesma tabela em várias publicações transacionais. Uma tabela pode aparecer no máximo em uma publicação transacional e em qualquer número de publicações de instantâneo se você selecionar **Gateway**.  
  
7.  Clique em **Conectar**, que cria uma conexão com o Editor Oracle e o configura para replicação. O **conectar ao servidor** caixa de diálogo é fechada e você retorna para o **Propriedades do distribuidor - \< distribuidor>** caixa de diálogo.  
  
    > [!NOTE]  
    >  Se houver qualquer problema com a configuração de rede, você receberá um aviso de erro nesse momento. Se experimentar problemas ao se conectar ao banco de dados Oracle, consulte a seção "O Distribuidor do SQL Server não pode se conectar à instância de banco de dados Oracle" em [Troubleshooting Oracle Publishers](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para criar uma publicação de um banco de dados Oracle  
  
1.  Conecte-se à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que o Editor Oracle usará como Distribuidor e, então, expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** .  
  
3.  Clique com botão direito do **publicações locais** pasta e clique **nova publicação Oracle**.  
  
4.  Na página **Editor Oracle** do Assistente de Nova Publicação, selecione o Editor Oracle. Se o Editor Oracle não estiver sendo exibido, clique em **Adicionar Editor Oracle**, que conduzirá você pelas etapas do procedimento anterior.  
  
5.  Na página **Tipo de Publicação** , selecione **Publicação de Instantâneo** ou **Publicação Transacional**.  
  
6.  Na página **Artigos** , selecione os objetos de banco de dados que você deseja publicar.  
  
     Opcionalmente, descarte colunas de tabela expandindo uma tabela e desmarcando a caixa de seleção para uma ou mais colunas. Clique em **Propriedades do Artigo** para exibir e modificar propriedades de artigo e especificar mapeamentos de tipo de dados alternativos, se necessário. Para obter mais informações sobre mapeamentos de tipo de dados, consulte [especificar mapeamentos de tipo de dados para um editor Oracle](../../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md).  
  
7.  Na página **Filtrar Linhas de Tabela** , aplique filtros para publicar um subconjunto de dados de uma ou mais tabelas.  
  
8.  Na página **Snapshot Agent** desmarque **Criar um instantâneo imediatamente** somente se você tiver criado todos os objetos e adicionado todos os dados necessários no banco de dados de assinatura.  
  
9. Sobre o **segurança do agente** página, especifique as credenciais para o Snapshot Agent (para todas as publicações) e o Log Reader Agent (para publicações transacionais). Os agentes executam e fazem conexões com o Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o contexto da conta do Windows [!INCLUDE[msCoName](../../../includes/msconame-md.md)] que você especificar. Os agentes fazem conexão com o banco de dados Oracle usando o contexto da conta que você especificou como esquema de usuário administrativo de replicação. Para obter mais informações, consulte [Configurar um editor Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
     Para obter mais informações sobre as permissões necessárias para cada agente, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) e [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
10. Na página **Ações do Assistente** , opcionalmente faça script da publicação. Para obter mais informações, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
11. Na página **Concluir o Assistente** , especifique um nome para a publicação.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Após a configuração do banco de dados Oracle como um Publicador, é possível criar uma publicação transacional ou instantânea da mesma maneira como você faria de um Editor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , usando os procedimentos armazenados do sistema.  
  
#### Para criar uma publicação Oracle  
  
1.  Configure o banco de dados Oracle como um Publicador. Para obter mais informações, consulte [Configurar um editor Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
2.  Se um Distribuidor remoto não existir, configure o Distribuidor remoto. Para obter mais informações, consulte [Configure Publishing and Distribution](../../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
3.  No distribuidor remoto que o editor Oracle usará, execute [sp_adddistpublisher & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md). Especifique o nome do substrato de rede transparente (TNS) da instância de banco de dados Oracle para **@publisher** e um valor de **ORACLE** ou **ORACLE GATEWAY** para **@publisher_type**. `Specify` o modo de segurança usado ao conectar o Publicador Oracle ao Distribuidor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] remoto como um dos seguintes:  
  
    -   Para usar a autenticação padrão da Oracle, o padrão, especifique um valor de **0** para **@security_mode**, o logon do esquema de usuário administrativo de replicação criada no editor Oracle durante a configuração de **@login**, e a senha para **@password**.  
  
        > [!IMPORTANT]  
        >  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se armazenar credenciais em um arquivo de script, proteja o arquivo para evitar acesso não autorizado.  
  
    -   Para usar a autenticação do Windows, especifique um valor de **1** para **@security_mode**.  
  
        > [!NOTE]  
        >  Para usar a Autenticação Windows, o servidor Oracle deve estar configurado para permitir conexões usando as credenciais do Windows (para obter mais informações, consulte a documentação do Oracle) e você deve estar conectado à mesma conta Microsoft Windows especificada para o esquema de replicação do usuário administrativo.  
  
4.  Crie um trabalho do Log Reader Agent para o banco de dados de publicação.  
  
    -   Se você não tiver certeza se um trabalho do Log Reader Agent existe para um banco de dados publicado, execute [sp_helplogreader_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) no distribuidor usado pelo editor Oracle no banco de dados de distribuição. Especifique o nome do Editor Oracle como **@publisher**. Se o conjunto de resultados estiver vazio, será preciso criar um trabalho do Log Reader Agent.  
  
    -   Se já houver um trabalho do Log Reader Agent no banco de dados de publicação, passe para a etapa 5.  
  
    -   No distribuidor usado pelo editor Oracle no banco de dados de distribuição, execute [sp_addlogreader_agent & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Especifique as credenciais do Windows na qual o agente é executado para **@job_login** e **@job_password**.  
  
        > [!NOTE]  
        >  O **@job_login** parâmetro deve corresponder ao logon fornecido na etapa 3. Não forneça informações de segurança do publicador. O Log Reader Agent se conecta ao Publicador usando as informações de segurança fornecidas na etapa 3.  
  
5.  No distribuidor no banco de dados de distribuição, execute [sp_addpublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) para criar a publicação. Para obter mais informações, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
6.  No distribuidor no banco de dados de distribuição, execute [sp_addpublication_snapshot & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique o nome da publicação usado na etapa 4 para **@publication** e as credenciais do Windows na qual o Snapshot Agent é executado para **@job_name** e **@password**. Para usar a autenticação padrão Oracle ao se conectar ao Editor, você também deve especificar um valor de **0** para **@publisher_security_mode** e as informações de logon do Oracle para **@publisher_login** e **@publisher_password**. Isso cria um trabalho do Agente de Instantâneo para a publicação.  
  
## Consulte também  
 [Configurar um publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Configurar o trabalho de conjunto de transação para um editor Oracle e 40; Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/administration/configure the transaction set job for an oracle publisher.md)   
 [Visão geral da Publicação Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)   
 [Script para conceder permissões da Oracle](../../../relational-databases/replication/non-sql/script-to-grant-oracle-permissions.md)  
  
  