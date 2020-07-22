---
title: Conceitos de procedimentos armazenados do sistema de replicação | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- stored procedures [SQL Server replication], programming
- programming [SQL Server replication], system stored procedures
- programming interfaces [SQL Server replication]
- system stored procedures [SQL Server replication]
- replication [SQL Server], how-to topics
ms.assetid: 816d2bda-ed72-43ec-aa4d-7ee3dc25fd8a
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 2387a1ffa414feae48c52bbfcdcfc5a104e9ffe8
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914686"
---
# <a name="replication-system-stored-procedures-concepts"></a>Replication System Stored Procedures Concepts
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]

  Em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o acesso programático a toda a funcionalidade configurável pelo usuário em uma topologia de replicação é fornecido por procedimentos armazenados do sistema. Embora os procedimentos armazenados possam ser executados individualmente por meio do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou do utilitário de linha de comando sqlcmd, pode ser útil gravar arquivos de script [!INCLUDE[tsql](../../../includes/tsql-md.md)] que possam ser executados para a criação de uma sequência lógica de tarefas de replicação.  
  
 A criação de scripts para as tarefas de replicação oferece os seguintes benefícios:  
  
-   Mantém uma cópia permanente das etapas usadas na implantação da sua topologia de replicação.  
  
-   Usa um único script para configurar vários Assinantes.  
  
-   Educa rapidamente os administradores de banco de dados novos, permitindo que eles avaliem, compreendam, alterem o código ou solucionem seus problemas.  
  
    > [!IMPORTANT]  
    >  Os scripts podem ser a fonte de vulnerabilidades de segurança; podem invocar funções de sistema sem o conhecimento ou a intervenção do usuário e conter credenciais de segurança em texto sem-formatação. Analise os scripts para procurar problemas de segurança antes de usá-los.  
  
## <a name="creating-replication-scripts"></a>Criando scripts de replicação  
 Do ponto de vista de replicação, um script é uma série de uma ou mais instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)], onde cada instrução executa um procedimento armazenado de replicação. Os scripts são arquivos de texto, geralmente com uma extensão de arquivo .sql, que podem ser executados com o utilitário sqlcmd. Quando um arquivo de script é executado, o utilitário executa as instruções SQL armazenadas nele. De forma similar, um script pode ser armazenado como um objeto de consulta em um projeto do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 os scripts de replicação podem ser criados das seguintes formas:  
  
-   Crie o script manualmente.  
  
-   Use os recursos de geração de script fornecidos nos assistentes de replicação ou  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
-   Use os RMOs (Replication Management Objects) para gerar o script programaticamente e criar um objeto de RMO.  
  
 Quando você cria scripts de replicação manualmente, tenha em mente as seguintes considerações:  
  
-   Os scripts [!INCLUDE[tsql](../../../includes/tsql-md.md)] têm um ou mais lotes. O comando GO sinaliza o término de um lote. Se um script [!INCLUDE[tsql](../../../includes/tsql-md.md)] não tiver nenhum comando GO, ele será executado como um único lote.  
  
-   Na execução de vários procedimentos armazenados de replicação em um único lote, após o primeiro procedimento, todos os procedimentos subsequentes do lote terão de ser precedidos pela palavra-chave EXECUTE.  
  
-   Todos os procedimentos armazenados de um lote devem ser compilados antes da execução do lote. No entanto, após a compilação do lote, e após a criação do plano de execução, poderá ou não ocorrer um erro em tempo de execução.  
  
-   Ao criar scripts para configurar a replicação, use a Autenticação do Windows para evitar o armazenamento de credenciais de segurança no arquivo de script. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
## <a name="sample-replication-script"></a>Script de replicação de exemplo  
 O script a seguir pode ser executado para configurar a publicação e a distribuição em um servidor.  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Install the Distributor and the distribution database.  
DECLARE @distributor AS sysname;  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @directory AS nvarchar(500);  
DECLARE @publicationDB AS sysname;  
-- Specify the Distributor name.  
SET @distributor = $(DistPubServer);  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
-- Specify the replication working directory.  
SET @directory = N'\\' + $(DistPubServer) + '\repldata';  
-- Specify the publication database.  
SET @publicationDB = N'AdventureWorks2012';   
  
-- Install the server MYDISTPUB as a Distributor using the defaults,  
-- including autogenerating the distributor password.  
USE master  
EXEC sp_adddistributor @distributor = @distributor;  
  
-- Create a new distribution database using the defaults, including  
-- using Windows Authentication.  
USE master  
EXEC sp_adddistributiondb @database = @distributionDB,   
    @security_mode = 1;  
GO  
  
-- Create a Publisher and enable AdventureWorks2012 for replication.  
-- Add MYDISTPUB as a publisher with MYDISTPUB as a local distributor  
-- and use Windows Authentication.  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
  
USE [distribution]  
EXEC sp_adddistpublisher @publisher=@publisher,   
    @distribution_db=@distributionDB,   
    @security_mode = 1;  
GO  
  
```  
  
 Dessa forma, esse script poderá ser salvo localmente como `instdistpub.sql`, para que possa ser executado ou executado novamente quando necessário.  
  
 O script anterior inclui variáveis de script **sqlcmd**, usadas em muitos dos códigos de replicação de exemplo dos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. As variáveis de script são definidas por meio da sintaxe `$(MyVariable)`. Os valores das variáveis podem ser transmitidos para um script na linha de comando ou no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte a próxima seção deste tópico, "Executando scripts de replicação".  
  
## <a name="executing-replication-scripts"></a>Executando scripts de replicação  
 Uma vez criado, um script de replicação pode ser executado de uma das seguintes formas:  
  
### <a name="creating-a-sql-query-file-in-sql-server-management-studio"></a>Criando um arquivo de consulta SQL no SQL Server Management Studio  
 Um arquivo de script de replicação [!INCLUDE[tsql](../../../includes/tsql-md.md)] pode ser criado como um arquivo SQL Query em um projeto do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Após a gravação do script, pode ser feita uma conexão ao banco de dados para que esse arquivo de consulta e o script possam ser executados. Para obter mais informações sobre como criar scripts do [!INCLUDE[tsql](../../../includes/tsql-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], veja [Editores de Consultas e de Texto &#40;SQL Server Management Studio&#41;](../../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md).  
  
 Para usar um script que inclua variáveis de script, o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] deve ser executado em modo **sqlcmd**. Em modo **sqlcmd**, o Editor de Consultas aceita sintaxe adicional específica do **sqlcmd**, como `:setvar`, usado para um valor de uma variável. Para obter mais informações sobre o modo **sqlcmd**, consulte [Editar scripts SQLCMD com o Editor de Consultas](../../../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md). No script a seguir, `:setvar` é usado para fornecer um valor para a variável `$(DistPubServer)`.  
  
```  
:setvar DistPubServer N'MyPublisherAndDistributor';  
  
-- Install the Distributor and the distribution database.  
DECLARE @distributor AS sysname;  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @directory AS nvarchar(500);  
DECLARE @publicationDB AS sysname;  
-- Specify the Distributor name.  
SET @distributor = $(DistPubServer);  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
  
--  
-- Additional code goes here  
--  
```  
  
### <a name="using-the-sqlcmd-utility-from-the-command-line"></a>Usando o utilitário sqlcmd na linha de comando  
 O exemplo a seguir mostra como a linha de comando é usada para executar o arquivo de script `instdistpub.sql` por meio do [utilitário sqlcmd](../../../tools/sqlcmd-utility.md):  
  
```  
sqlcmd.exe -E -S sqlserverinstance -i C:\instdistpub.sql -o C:\output.log -v DistPubServer="N'MyDistributorAndPublisher'"  
```  
  
 Neste exemplo, a opção `-E` indica que a Autenticação do Windows será usada na conexão ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Quando a Autenticação do Windows for usada, não haverá necessidade de armazenar um nome de usuário e uma senha no arquivo de script. O nome e o caminho do arquivo de script são especificados pela opção `-i` e o nome do arquivo de saída é especificado pela opção `-o` (a saída do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será gravada nesse arquivo em vez de no console quando essa opção for usada). O utilitário `sqlcmd` permite que você transmita variáveis de script para um script [!INCLUDE[tsql](../../../includes/tsql-md.md)] em runtime por meio da opção `-v`. Neste exemplo, `sqlcmd` substitui todas as instâncias de `$(DistPubServer)` do script pela valor `N'MyDistributorAndPublisher'` antes da execução.  
  
> [!NOTE]  
>  A opção `-X` desabilita variáveis de script.  
  
### <a name="automating-tasks-in-a-batch-file"></a>Automatizando tarefas em um arquivo em lotes  
 Com a utilização de um arquivo em lotes, as tarefas de administração de replicação, as tarefas de sincronização de replicação e outras tarefas podem ser automatizadas no mesmo arquivo em lotes. O arquivo em lotes a seguir usa o utilitário **sqlcmd** para remover e recriar o banco de dados de assinatura e para adicionar uma assinatura pull de mesclagem. Em seguida, o arquivo invocará o agente de mesclagem para sincronizar a assinatura nova:  
  
```  
REM ----------------------Script to synchronize merge subscription ----------------------  
REM -- Creates subscription database and   
REM -- synchronizes the subscription to MergeSalesPerson.  
REM -- Current computer acts as both Publisher and Subscriber.  
REM -------------------------------------------------------------------------------------  
  
SET Publisher=%computername%  
SET Subscriber=%computername%  
SET PubDb=AdventureWorks  
SET SubDb=AdventureWorksReplica  
SET PubName=AdvWorksSalesOrdersMerge  
  
REM -- Drop and recreate the subscription database at the Subscriber  
sqlcmd /S%Subscriber% /E /Q"USE master IF EXISTS (SELECT * FROM sysdatabases WHERE name='%SubDb%' ) DROP DATABASE %SubDb%"  
sqlcmd /S%Subscriber% /E /Q"USE master CREATE DATABASE %SubDb%"  
  
REM -- Add a pull subscription at the Subscriber  
sqlcmd /S%Subscriber% /E /Q"USE %SubDb% EXEC sp_addmergepullsubscription @publisher = %Publisher%, @publication = %PubName%, @publisher_db = %PubDb%"  
sqlcmd /S%Subscriber% /E /Q"USE %SubDb%  EXEC sp_addmergepullsubscription_agent @publisher = %Publisher%, @publisher_db = %PubDb%, @publication = %PubName%, @subscriber = %Subscriber%, @subscriber_db = %SubDb%, @distributor = %Publisher%"  
  
REM -- This batch file starts the merge agent at the Subscriber to   
REM -- synchronize a pull subscription to a merge publication.  
REM -- The following must be supplied on one line.  
"\Program Files\Microsoft SQL Server\130\COM\REPLMERG.EXE"  -Publisher  %Publisher% -Subscriber  %Subscriber%  -Distributor %Publisher%  -PublisherDB  %PubDb% -SubscriberDB %SubDb% -Publication %PubName% -PublisherSecurityMode 1 -OutputVerboseLevel 1  -Output  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1 -Validate 3  
  
```  
  
## <a name="scripting-common-replication-tasks"></a>Gerando scripts de tarefas comuns de replicação  
 A seguir, algumas das tarefas de replicação mais comuns que podem ser incluídas em um script por meio de procedimentos armazenados do sistema:  
  
-   Configurando a publicação e a distribuição  
  
-   Modificando as propriedades do Publicador e do Distribuidor  
  
-   Desabilitando a publicação e a distribuição  
  
-   Criando publicações e definindo artigos  
  
-   Excluindo publicações e artigos  
  
-   Criando uma assinatura pull  
  
-   Modificando uma assinatura pull  
  
-   Excluindo uma assinatura pull  
  
-   Criando uma assinatura push  
  
-   Modificando uma assinatura push  
  
-   Excluindo uma assinatura push  
  
-   Sincronizando uma assinatura pull  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos de programação da replicação](../../../relational-databases/replication/concepts/replication-programming-concepts.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Replicação de script](../../../relational-databases/replication/scripting-replication.md)  
  
  
