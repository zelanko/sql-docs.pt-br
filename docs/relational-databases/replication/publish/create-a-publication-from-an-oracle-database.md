---
title: Criar uma publicação de um banco de dados Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], Oracle databases
- Oracle publishing [SQL Server replication], configuring
ms.assetid: b3812746-14b0-4b22-809e-b4a95e1c8083
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2edf3cf1f23b8a18f2fc2b7586d22b7d46bb7226
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67580110"
---
# <a name="create-a-publication-from-an-oracle-database"></a>Criar uma publicação de um banco de dados Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como criar uma publicação no a partir de um banco de dados Oracle no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Pré-requisitos](#Prerequisites)  
  
-   **Para criar uma publicação de um banco de dados Oracle usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Antes de criar uma publicação, você deve instalar o software Oracle no Distribuidor do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , além de configurar o banco de dados Oracle. Para obter mais informações, consulte [Configure an Oracle Publisher](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md) (Configurar um publicador do Oracle).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Crie uma publicação de instantâneo ou transacional a partir de um banco de dados Oracle com o Assistente de Nova Publicação.  
  
 A primeira vez que você cria uma publicação de um banco de dados Oracle, você deve identificar o Editor Oracle no Distribuidor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (não é necessário fazer isso em publicações subsequentes do mesmo banco de dados). A identificação do publicador Oracle pode ser realizada usando o Assistente para Nova Publicação ou a caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>** . Este tópico mostra a caixa de diálogo **Propriedades do Distribuidor – \<Distributor>** .  
  
#### <a name="to-identify-the-oracle-publisher-at-the-sql-server-distributor"></a>Para identificar o Editor Oracle no Distribuidor do SQL Server  
  
1.  No [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que o Editor Oracle usará como Distribuidor e, então, expanda o nó do servidor.  
  
2.  Clique com o botão direito do mouse na pasta **Replicação** e em seguida clique em **Propriedades do Distribuidor**.  
  
3.  Na página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor – \<Distributor>** , clique em **Adicionar** e, em seguida, em **Adicionar Publicador Oracle**.  
  
4.  Na caixa de diálogo **Conectar ao Servidor** , clique no botão **Opções** .  
  
5.  Na guia **Logon** :  
  
    1.  Insira o nome da instância do banco de dados Oracle ou selecione **Procurar mais** na caixa de combinação **Instância do servidor** .  
  
    2.  Selecione **Autenticação Padrão da Oracle** (recomendado) ou **Autenticação do Windows**.  
  
         Se você selecionar **Autenticação do Windows**: o servidor Oracle deve estar configurado para permitir conexões usando credenciais do Windows (para obter mais informações, consulte a documentação do Oracle) e você deve estar atualmente conectado à mesma conta do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows especificada para o esquema de usuário administrativo de replicação.  
  
    3.  Se você selecionou **Autenticação Padrão da Oracle**, insira o logon e a senha do esquema de usuário administrativo de replicação que você criou no Editor Oracle durante a configuração.  
  
6.  Na guia **Propriedades de Conexão** , selecione um tipo de Publicador de **Gateway** ou **Completo**.  
  
     A opção **Complete** é projetada para fornecer publicações transacionais e de instantâneo com o conjunto completo de recursos com suporte para publicações Oracle. A opção **Gateway** fornece otimizações de projeto específicas para aprimorar o desempenho de casos em que a replicação serve como um gateway entre sistemas. A opção **Gateway** não poderá ser usada se você planejar publicar a mesma tabela em várias publicações transacionais. Uma tabela pode aparecer no máximo em uma publicação transacional e em qualquer número de publicações de instantâneo se você selecionar **Gateway**.  
  
7.  Clique em **Conectar**, que cria uma conexão com o Editor Oracle e o configura para replicação. A caixa de diálogo **Conectar ao Servidor** é fechada e você retorna para a caixa de diálogo **Propriedades do Distribuidor – \<Distributor>** .  
  
    > [!NOTE]  
    >  Se houver qualquer problema com a configuração de rede, você receberá um aviso de erro nesse momento. Se experimentar problemas ao se conectar ao banco de dados Oracle, consulte a seção "O Distribuidor do SQL Server não pode se conectar à instância de banco de dados Oracle" em [Troubleshooting Oracle Publishers](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

#### <a name="to-create-a-publication-from-an-oracle-database"></a>Para criar uma publicação de um banco de dados Oracle  
  
1.  Conecte-se à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que o Editor Oracle usará como Distribuidor e, então, expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** .  
  
3.  Expanda a pasta **Publicações Locais** e em seguida clique em **Nova Publicação Oracle**.  
  
4.  Na página **Editor Oracle** do Assistente de Nova Publicação, selecione o Editor Oracle. Se o Editor Oracle não estiver sendo exibido, clique em **Adicionar Editor Oracle**, que conduzirá você pelas etapas do procedimento anterior.  
  
5.  Na página **Tipo de Publicação** , selecione **Publicação de Instantâneo** ou **Publicação Transacional**.  
  
6.  Na página **Artigos** , selecione os objetos de banco de dados que você deseja publicar.  
  
     Opcionalmente, descarte colunas de tabela expandindo uma tabela e desmarcando a caixa de seleção para uma ou mais colunas. Clique em **Propriedades do Artigo** para exibir e modificar propriedades de artigo e especificar mapeamentos de tipo de dados alternativos, se necessário. Para obter mais informações sobre mapeamentos de tipo de dados, consulte [Especificar mapeamentos de tipo de dados para um Publicador Oracle](../../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md).  
  
7.  Na página **Filtrar Linhas de Tabela** , aplique filtros para publicar um subconjunto de dados de uma ou mais tabelas.  
  
8.  Na página **Snapshot Agent** desmarque **Criar um instantâneo imediatamente** somente se você tiver criado todos os objetos e adicionado todos os dados necessários no banco de dados de assinatura.  
  
9. Na página **Segurança do Agente** especifique as credenciais para o Snapshot Agent (para todas as publicações) e Log Reader Agent (para publicações transacionais). Os agentes executam e fazem conexões com o Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o contexto da conta do Windows [!INCLUDE[msCoName](../../../includes/msconame-md.md)] que você especificar. Os agentes fazem conexão com o banco de dados Oracle usando o contexto da conta que você especificou como esquema de usuário administrativo de replicação. Para obter mais informações, consulte [Configure an Oracle Publisher](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md) (Configurar um publicador do Oracle).  
  
     Para obter mais informações sobre as permissões necessárias para cada agente, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) e [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
10. Na página **Ações do Assistente** , opcionalmente faça script da publicação. Para obter mais informações, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
11. Na página **Concluir o Assistente** , especifique um nome para a publicação.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Após a configuração do banco de dados Oracle como um Publicador, é possível criar uma publicação transacional ou instantânea da mesma maneira como você faria de um Editor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , usando os procedimentos armazenados do sistema.  
  
#### <a name="to-create-an-oracle-publication"></a>Para criar uma publicação Oracle  
  
1.  Configure o banco de dados Oracle como um Publicador. Para obter mais informações, consulte [Configure an Oracle Publisher](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md) (Configurar um publicador do Oracle).  
  
2.  Se um Distribuidor remoto não existir, configure o Distribuidor remoto. Para obter mais informações, consulte [Configure Publishing and Distribution](../../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
3.  No Distribuidor remoto que o Publicador Oracle usará, execute [sp_adddistpublisher &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md). Especifique o nome TNS (Transparent Network Substrate) da instância do banco de dados Oracle para **@publisher** e um valor de **ORACLE** ou **ORACLE GATEWAY** para **@publisher_type** . `Specify` o modo de segurança usado ao conectar o Publicador Oracle ao Distribuidor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] remoto como um dos seguintes:  
  
    -   Para usar a Autenticação Padrão Oracle, o padrão, especifique um valor **0** para **@security_mode** , o logon do esquema de replicação do usuário administrativo criado no Editor Oracle durante a configuração para **@login** e a senha para **@password** .  
  
        > [!IMPORTANT]  
        >  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se armazenar credenciais em um arquivo de script, proteja o arquivo para evitar acesso não autorizado.  
  
    -   Para usar a Autenticação do Windows, especifique um valor de **1** para **@security_mode** .  
  
        > [!NOTE]  
        >  Para usar a Autenticação Windows, o servidor Oracle deve estar configurado para permitir conexões usando as credenciais do Windows (para obter mais informações, consulte a documentação do Oracle) e você deve estar conectado à mesma conta Microsoft Windows especificada para o esquema de replicação do usuário administrativo.  
  
4.  Crie um trabalho do Log Reader Agent para o banco de dados de publicação.  
  
    -   Se você não tiver certeza se um trabalho do Agente de Leitor de Log existe para um banco de dados publicado, execute [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) no Distribuidor usado pelo Publicador Oracle no banco de dados de distribuição. Especifique o nome do Publicador Oracle para **@publisher** . Se o conjunto de resultados estiver vazio, será preciso criar um trabalho do Log Reader Agent.  
  
    -   Se já houver um trabalho do Log Reader Agent no banco de dados de publicação, passe para a etapa 5.  
  
    -   No Distribuidor usado pelo Publicador Oracle no banco de dados de distribuição, execute [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Especifique as credenciais do Windows sob as quais o agente será executado para **@job_login** e **@job_password** .  
  
        > [!NOTE]  
        >  A opção **@job_login** deve corresponder ao logon fornecido na etapa 3. Não forneça informações de segurança do publicador. O Log Reader Agent se conecta ao Publicador usando as informações de segurança fornecidas na etapa 3.  
  
5.  No Distribuidor no banco de dados de distribuição, execute [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) para criar a publicação. Para obter mais informações, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
6.  No Distribuidor no banco de dados de distribuição, execute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique o nome da publicação usada na etapa 4 para **@publication** e as credenciais do Windows com as quais o Snapshot Agent será executado para **@job_name** e **@password** . Para usar a Autenticação Padrão Oracle ao se conectar ao Publicador, especifique também um valor **0** para **@publisher_security_mode** e as informações de logon do Oracle para **@publisher_login** e **@publisher_password** . Isso cria um trabalho do Agente de Instantâneo para a publicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar um Publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Configurar o trabalho do conjunto de transações para um Publicador Oracle &#40;programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [Visão geral da publicação do Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)   
 [Script to Grant Oracle Permissions](../../../relational-databases/replication/non-sql/script-to-grant-oracle-permissions.md)  
  
  
