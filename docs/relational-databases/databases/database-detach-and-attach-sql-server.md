---
title: Anexar e desanexar bancos de dados (SQL Server) | Microsoft Docs
description: Você pode desanexar e reanexar os arquivos de log de transações e de dados de um banco do SQL Server a fim de alterar o banco de dados para outra instância ou movê-lo.
ms.custom: ''
ms.date: 11/26/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- databases [SQL Server], detaching
- detach database [SQL Server]
- databases [SQL Server], attaching
- removing databases
- transaction logs [SQL Server], detaching
- databases [SQL Server], removing
- restoring [SQL Server], attached databases
- transaction logs [SQL Server], attaching
- differential backups, after detaching
- moving databases
- attach database [SQL Server]
- detaching databases [SQL Server]
- differential base [SQL Server]
- attaching databases [SQL Server]
- databases [SQL Server], moving
ms.assetid: d0de0639-bc54-464e-98b1-6af22a27eb86
author: stevestein
ms.author: sstein
ms.openlocfilehash: a43fcc0dade0c030546e76bf36f242973f918d2e
ms.sourcegitcommit: e922721431d230c45bbfb5dc01e142abbd098344
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82138140"
---
# <a name="database-detach-and-attach-sql-server"></a>Anexar e desanexar bancos de dados (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Os dados e os arquivos de log de transações de um banco de dados podem ser desanexados e, em seguida, reanexados à mesma ou a outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Desanexar e anexar um banco de dados é útil se você deseja alterar o banco de dados a uma instância diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no mesmo computador ou mover o banco de dados.  
  
  
##  <a name="security"></a><a name="Security"></a> Segurança  
As permissões de acesso ao arquivo são definidas durante algumas operações de banco de dados, inclusive desanexar ou anexar um banco de dados.  
  
> [!IMPORTANT]  
> Não é recomendável anexar ou restaurar bancos de dados de origem desconhecida ou não confiável. Esses bancos de dados podem conter um código mal-intencionado que pode executar um código [!INCLUDE[tsql](../../includes/tsql-md.md)] inesperado ou provocar erros modificando o esquema ou a estrutura física do banco de dados.   
> Antes de usar um banco de dados de origem desconhecida ou não confiável, execute [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) no banco de dados, em um servidor que não seja de produção. Além disso, examine o código, como procedimentos armazenados ou outro código definido pelo usuário, no banco de dados.  
  
##  <a name="detaching-a-database"></a><a name="DetachDb"></a> Desanexando um banco de dados  
Desanexar um banco de dados remove-o da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mas deixa intacto o banco de dados, com seus arquivos de dados e arquivos de log de transações. Esses arquivos podem então ser usados para anexar o banco de dados a qualquer instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], inclusive o servidor do qual o banco de dados foi desanexado.  
  
Você não poderá desanexar um banco de dados se alguma das seguintes opções for verdadeira:  
  
-   O banco de dados está replicado e publicado. Se replicado, o banco de dados não pode estar publicado. Antes de poder desanexá-lo, é necessário desabilitar a publicação executando [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md).  
  
    > [!NOTE]  
    > Se não for possível usar **sp_replicationdboption**, você poderá remover a replicação executando [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
-   Há um instantâneo do banco de dados no banco de dados.  
  
    Antes de poder desanexar o banco de dados, você deve descartar todos os seus instantâneos. Para obter mais informações, veja [Remover um instantâneo do banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md).  
  
    > [!NOTE]  
    > Um instantâneo do banco de dados não pode ser desanexado ou anexado.  
  
-   O banco de dados está sendo espelhado em uma sessão de espelhamento de banco de dados.  
  
    O banco de dados não pode ser desanexado, a menos que a sessão seja encerrada. Para obter mais informações, veja [Removendo o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
-   O banco de dados é suspeito. Um banco de dados suspeito não pode ser desanexado. Para poder desanexá-lo, você deve colocá-lo em modo de emergência. Para obter mais informações sobre como colocar um banco de dados em modo de emergência, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
-  O banco de dados é um banco de dados de sistema.  
  
### <a name="backup-and-restore-and-detach"></a>Backup e restauração e desanexação  
A desanexação de um banco de dados somente leitura perde informações sobre as bases diferenciais de backups diferenciais. Para obter mais informações, veja [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
### <a name="responding-to-detach-errors"></a>Respondendo a erros de desanexação  
Os erros produzidos ao desanexar um banco de dados podem impedir que o banco de dados seja desligado corretamente e que o log de transações seja reconstruído. Se você receber uma mensagem de erro, execute as ações corretivas a seguir:  
  
1.  Reanexe todos os arquivos associados ao banco de dados, e não apenas o arquivo primário.  
  
2.  Resolva o problema que causou a mensagem de erro.  
  
3.  Desanexe o banco de dados novamente.  
  
##  <a name="attaching-a-database"></a><a name="AttachDb"></a> Anexando um banco de dados  
Você pode anexar um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] copiado ou desanexado. Quando você anexa um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que contém arquivos de catálogo de texto completo a uma instância de servidor do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , os arquivos de catálogo são anexados de seus locais anteriores junto com os outros arquivos de banco de dados, assim como ocorre no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obter mais informações, veja [Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
Quando você anexa um banco de dados, todos os arquivos de dados (arquivos MDF e NDF) devem estar disponíveis. Se algum arquivo de dados tiver um caminho diferente de quando o banco de dados foi inicialmente criado ou anexado pela última vez, você deverá especificar o caminho atual do arquivo.  
  
> [!NOTE]  
> Se o arquivo de dados primário que está sendo anexado for somente leitura, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] presumirá que o banco de dados é somente leitura.  
  
Quando um banco de dados criptografado é anexado primeiro a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o proprietário do banco de dados deve abrir a chave mestra do banco de dados executando a instrução seguinte: `OPEN MASTER KEY DECRYPTION BY PASSWORD = 'password'`. É recomendável que você habilite a descriptografia automática da chave mestra executando a seguinte instrução: `ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY`. Para obter mais informações, veja [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md) e [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md).  
  
 O requisito para anexar arquivos de log depende, em parte, de o banco de dados ser de leitura e gravação ou apenas leitura:  
  
-   Para um banco de dados de leitura e gravação, você pode geralmente anexar um arquivo de log em um novo local. No entanto, em alguns casos, a reanexação de um banco de dados exige seus arquivos de log existentes. Portanto, é importante sempre conservar todos os arquivos de log desanexados, até que o banco de dados tenha sido anexado com êxito sem eles.  
  
    Se um banco de dados de leitura e gravação tiver um único arquivo de log e você não especificar um novo local para o arquivo de log, a operação de anexação procurará o arquivo no local antigo. Se for achado, o arquivo de log antigo será usado, independentemente de o banco de dados ter sido desligado corretamente. No entanto, se o arquivo de log antigo não for encontrado e se o banco de dados tiver sido desligado corretamente e não tiver nenhuma cadeia de logs ativa, a operação de anexação tentará criar um novo arquivo de log para o banco de dados.  
  
-   Se o arquivo de dados primário que está sendo anexado for somente leitura, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] presumirá que o banco de dados é somente leitura. Para um banco de dados somente leitura, o arquivo ou arquivos de log devem estar disponíveis no local especificado no arquivo primário do banco de dados. Um novo arquivo de log não pode ser criado porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode atualizar o local de log armazenado no arquivo primário.  
 
###  <a name="metadata-changes-on-attaching-a-database"></a><a name="Metadata"></a> Alterações de metadados na anexação de um banco de dados  
Quando um banco de dados somente leitura é desanexado e reanexado, as informações de backup sobre a base diferencial atual são perdidas. A *base diferencial* é o backup completo mais recente de todos os dados no banco de dados ou em um subconjunto dos arquivos ou de grupos de arquivos do banco de dados. Sem a informações de backup de base, o banco de dados **master** se torna não sincronizado com o banco de dados somente leitura, portanto backups diferenciais utilizados posteriormente podem fornecer resultados inesperados. Portanto, se você estiver usando backups diferenciais com um banco de dados somente leitura, deverá estabelecer uma nova base diferencial obtendo um backup completo após reanexar o banco de dados. Para obter informações sobre backups diferenciais, veja [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
Na anexação, ocorre inicialização do banco de dados. Geralmente, a anexação de um banco de dados coloca-o no mesmo estado em que estava quando foi desanexado ou copiado. No entanto, as operações de anexação e desanexação desabilitam o encadeamento de propriedades de bancos de dados para o banco de dados. Para obter informações sobre como habilitar o encadeamento, veja [Opção cross db ownership chaining de configuração de servidor](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md). 

 > [!IMPORTANT]
 > Por padrão e por segurança, as opções para *is_broker_enabled*, *is_honor_broker_priority_on* e *is_db_trustworthy_on* são definidas como OFF sempre que o banco de dados está anexado. Para obter informações sobre como definir essas opções como ON, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  Para obter mais informações sobre metadados, veja [Gerenciar metadados ao disponibilizar um banco de dados em outro servidor](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).
  
### <a name="backup-and-restore-and-attach"></a>Backup e restauração e anexação  
Como qualquer banco de dados que esteja offline total ou parcialmente, um banco de dados com arquivos de restauração não pode ser anexado. Se você interromper a sequência de restauração, poderá anexar o banco de dados. Em seguida, você poderá reiniciar a sequência de restauração.  
  
###  <a name="attaching-a-database-to-another-server-instance"></a><a name="OtherServerInstance"></a> Anexando um banco de dados a outra instância do servidor  
  
> [!IMPORTANT]  
> Um banco de dados criado por uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode ser anexado em versões anteriores. Isso impede o banco de dados seja usado fisicamente com uma versão anterior do [!INCLUDE[ssde_md](../../includes/ssde_md.md)]. No entanto, isso se relaciona com o estado dos metadados e não afeta o [nível de compatibilidade do banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md). Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).   
  
Quando você anexa um banco de dados a outra instância do servidor, para oferecer uma experiência consistente aos usuários e aplicativos, talvez precise recriar alguns ou todos os metadados para o banco de dados, como logons e trabalhos, na outra instância de servidor. Para obter mais informações, confira [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
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
  
## <a name="see-also"></a>Consulte Também  
 [Arquivos e grupos de arquivos do banco de dados](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
