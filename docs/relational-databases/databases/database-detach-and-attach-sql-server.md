---
title: "Anexar e desanexar bancos de dados (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "atualizando bancos de dados"
  - "bancos de dados [SQL Server], desanexando"
  - "desanexar banco de dados [SQL Server]"
  - "bancos de dados [SQL Server], anexando"
  - "removendo bancos de dados"
  - "logs de transação [SQL Server], desanexando"
  - "bancos de dados [SQL Server], removendo"
  - "restaurando [SQL Server], bancos de dados anexados"
  - "logs de transação [SQL Server], anexando"
  - "backups diferenciais, após desanexar"
  - "movendo bancos de dados"
  - "anexar banco de dados [SQL Server]"
  - "desanexando bancos de dados [SQL Server]"
  - "base diferencial [SQL Server]"
  - "anexando bancos de dados [SQL Server]"
  - "banco de dados [SQL Server], movendo"
ms.assetid: d0de0639-bc54-464e-98b1-6af22a27eb86
caps.latest.revision: 98
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 97
---
# Anexar e desanexar bancos de dados (SQL Server)
  Os dados e os arquivos de log de transações de um banco de dados podem ser desanexados e, em seguida, reanexados à mesma ou a outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Desanexar e anexar um banco de dados é útil se você deseja alterar o banco de dados a uma instância diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no mesmo computador ou mover o banco de dados.  
  
  
##  <a name="Security"></a> Segurança  
 As permissões de acesso ao arquivo são definidas durante algumas operações de banco de dados, inclusive desanexar ou anexar um banco de dados.  
  
> [!IMPORTANT]  
>  Não é recomendável anexar ou restaurar bancos de dados de origem desconhecida ou não confiável. Esses bancos de dados podem conter um código mal-intencionado que pode executar um código [!INCLUDE[tsql](../../includes/tsql-md.md)] inesperado ou provocar erros modificando o esquema ou a estrutura física do banco de dados. Antes de usar um banco de dados de origem desconhecida ou não confiável, execute [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) no banco de dados, em um servidor que não seja de produção. Além disso, examine o código, como procedimentos armazenados ou outro código definido pelo usuário, no banco de dados.  
  
##  <a name="DetachDb"></a> Desanexando um banco de dados  
 Desanexar um banco de dados remove-o da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mas deixa intacto o banco de dados, com seus arquivos de dados e arquivos de log de transações. Esses arquivos podem então ser usados para anexar o banco de dados a qualquer instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], inclusive o servidor do qual o banco de dados foi desanexado.  
  
 Você não poderá desanexar um banco de dados se alguma das seguintes opções for verdadeira:  
  
-   O banco de dados está replicado e publicado. Se replicado, o banco de dados não pode estar publicado. Antes de poder desanexá-lo, é necessário desabilitar a publicação executando [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md).  
  
    > [!NOTE]  
    >  Se não for possível usar **sp_replicationdboption**, você poderá remover a replicação executando [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
-   Há um instantâneo do banco de dados no banco de dados.  
  
     Antes de poder desanexar o banco de dados, você deve descartar todos os seus instantâneos. Para obter mais informações, veja [Remover um instantâneo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md).  
  
    > [!NOTE]  
    >  Um instantâneo do banco de dados não pode ser desanexado ou anexado.  
  
-   O banco de dados está sendo espelhado em uma sessão de espelhamento de banco de dados.  
  
     O banco de dados não pode ser desanexado, a menos que a sessão seja encerrada. Para obter mais informações, veja [Removendo o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
-   O banco de dados é suspeito. Um banco de dados suspeito não pode ser desanexado. Para poder desanexá-lo, você deve colocá-lo em modo de emergência. Para obter mais informações sobre como colocar um banco de dados em modo de emergência, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
-   O banco de dados é um banco de dados de sistema.  
  
### Backup e restauração e desanexação  
 A desanexação de um banco de dados somente leitura perde informações sobre as bases diferenciais de backups diferenciais. Para obter mais informações, veja [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
### Respondendo a erros de desanexação  
 Os erros produzidos ao desanexar um banco de dados podem impedir que o banco de dados seja desligado corretamente e que o log de transações seja reconstruído. Se você receber uma mensagem de erro, execute as ações corretivas a seguir:  
  
1.  Reanexe todos os arquivos associados ao banco de dados, e não apenas o arquivo primário.  
  
2.  Resolva o problema que causou a mensagem de erro.  
  
3.  Desanexe o banco de dados novamente.  
  
##  <a name="AttachDb"></a> Anexando um banco de dados  
 Você pode anexar um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] copiado ou desanexado. Quando você anexa um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que contém arquivos de catálogo de texto completo a uma instância de servidor do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], os arquivos de catálogo são anexados de seus locais anteriores junto com os outros arquivos de banco de dados, assim como ocorre no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obter mais informações, veja [Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
 Quando você anexa um banco de dados, todos os arquivos de dados (arquivos MDF e NDF) devem estar disponíveis. Se algum arquivo de dados tiver um caminho diferente de quando o banco de dados foi inicialmente criado ou anexado pela última vez, você deverá especificar o caminho atual do arquivo.  
  
> [!NOTE]  
>  Se o arquivo de dados primário que está sendo anexado for somente leitura, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] presumirá que o banco de dados é somente leitura.  
  
 Quando um banco de dados criptografado é anexado primeiro a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o proprietário do banco de dados deve abrir a chave mestra do banco de dados executando a instrução seguinte: OPEN MASTER KEY DECRYPTION BY PASSWORD = **'***password***'**. Recomendamos habilitar a descriptografia automática da chave mestra executando a instrução seguinte: ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY. Para obter mais informações, veja [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md) e [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md).  
  
 O requisito para anexar arquivos de log depende, em parte, de o banco de dados ser de leitura e gravação ou apenas leitura:  
  
-   Para um banco de dados de leitura e gravação, você pode geralmente anexar um arquivo de log em um novo local. No entanto, em alguns casos, a reanexação de um banco de dados exige seus arquivos de log existentes. Portanto, é importante sempre conservar todos os arquivos de log desanexados, até que o banco de dados tenha sido anexado com êxito sem eles.  
  
     Se um banco de dados de leitura e gravação tiver um único arquivo de log e você não especificar um novo local para o arquivo de log, a operação de anexação procurará o arquivo no local antigo. Se for achado, o arquivo de log antigo será usado, independentemente de o banco de dados ter sido desligado corretamente. No entanto, se o arquivo de log antigo não for encontrado e se o banco de dados tiver sido desligado corretamente e não tiver nenhuma cadeia de logs ativa, a operação de anexação tentará criar um novo arquivo de log para o banco de dados.  
  
-   Se o arquivo de dados primário que está sendo anexado for somente leitura, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] presumirá que o banco de dados é somente leitura. Para um banco de dados somente leitura, o arquivo ou arquivos de log devem estar disponíveis no local especificado no arquivo primário do banco de dados. Um novo arquivo de log não pode ser criado porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode atualizar o local de log armazenado no arquivo primário.  
  
 **Nesta seção:**  
  
-   [Alterações de metadados na anexação de um banco de dados](#Metadata)  
  
-   [Backup e restauração e anexação](#BnR)  
  
-   [Anexando um banco de dados a outra instância do servidor](#OtherServerInstance)  
  
###  <a name="Metadata"></a> Alterações de metadados na anexação de um banco de dados  
 Quando um banco de dados somente leitura é desanexado e reanexado, as informações de backup sobre a base diferencial atual são perdidas. A *base diferencial* é o backup completo mais recente de todos os dados no banco de dados ou em um subconjunto dos arquivos ou de grupos de arquivos do banco de dados. Sem a informações de backup de base, o banco de dados **master** se torna não sincronizado com o banco de dados somente leitura, portanto backups diferenciais utilizados posteriormente podem fornecer resultados inesperados. Portanto, se você estiver usando backups diferenciais com um banco de dados somente leitura, deverá estabelecer uma nova base diferencial obtendo um backup completo após reanexar o banco de dados. Para obter informações sobre backups diferenciais, veja [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
 Na anexação, ocorre inicialização do banco de dados. Geralmente, a anexação de um banco de dados coloca-o no mesmo estado em que estava quando foi desanexado ou copiado. No entanto, as operações de anexação e desanexação desabilitam o encadeamento de propriedades de bancos de dados para o banco de dados. Para obter informações sobre como habilitar o encadeamento, veja [Opção cross db ownership chaining de configuração de servidor](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md). Além disso, TRUSTWORTHY é definido como OFF sempre que o banco de dados for anexado. Para obter informações sobre como definir TRUSTWORTHY como ON, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
### Backup e restauração e anexação  
 Como qualquer banco de dados que esteja offline total ou parcialmente, um banco de dados com arquivos de restauração não pode ser anexado. Se você interromper a sequência de restauração, poderá anexar o banco de dados. Em seguida, você poderá reiniciar a sequência de restauração.  
  
###  <a name="OtherServerInstance"></a> Anexando um banco de dados a outra instância do servidor  
  
> [!IMPORTANT]  
>  Um banco de dados criado por uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode ser anexado em versões anteriores.  
  
 Quando você anexa um banco de dados a outra instância do servidor, para oferecer uma experiência consistente aos usuários e aplicativos, talvez precise recriar alguns ou todos os metadados para o banco de dados, como logons e trabalhos, na outra instância de servidor. Para obter mais informações, consulte [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage metadata when making a database available on another server.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para desanexar um banco de dados**  
  
-   [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)  
  
-   [Desanexar um banco de dados](../../relational-databases/databases/detach-a-database.md)  
  
 **Para anexar um banco de dados**  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
-   [Anexar um banco de dados](../../relational-databases/databases/attach-a-database.md)  
  
-   [sp_attach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-db-transact-sql.md)  
  
-   [sp_attach_single_file_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql.md)  
  
 **Para atualizar um banco de dados usando as operações de anexação e desanexação**  
  
-   [Atualizar um banco de dados usando Desanexar e Anexar &#40;Transact-SQL&#41;](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md)  
  
 **Para mover um banco de dados usando as operações de anexação e desanexação**  
  
-   [Mover um banco de dados usando Desanexar e Anexar &#40;Transact-SQL&#41;](../../relational-databases/databases/move-a-database-using-detach-and-attach-transact-sql.md)  
  
 **Para excluir um instantâneo do banco de dados**  
  
-   [Remover um instantâneo do banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
## Consulte também  
 [Arquivos e grupos de arquivos do banco de dados](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  