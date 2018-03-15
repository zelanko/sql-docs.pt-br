---
title: RESTORE DATABASE (Parallel Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d915bfc1-e392-4a3a-9d94-08682cf3c864
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ba8aa12f38fce6ac00f88f0015008da25a59b88
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="restore-database-parallel-data-warehouse"></a>RESTORE DATABASE (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Restaura um banco de dados de usuário do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] por meio de um backup de banco de dados em um dispositivo do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. O banco de dados é restaurado por meio de um backup que foi criado anteriormente pelo comando [!INCLUDE[ssPDW](../../includes/sspdw-md.md)][BACKUP DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md). Use as operações de backup e restauração para criar um plano de recuperação de desastre ou mover bancos de dados de um dispositivo para outro.  
  
> [!NOTE]  
>  A restauração do mestre inclui a restauração das informações de logon do dispositivo. Para restaurar um mestre, use a página [Restaurar o banco de dados mestre &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md) da ferramenta **Configuration Manager**. Um administrador com acesso ao nó de Controle pode executar essa operação.  
  
 Para obter mais informações sobre backups de banco de dados do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], confira "Backup e restauração" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
      Restore the master database  
-- Use the Configuration Manager tool.  
  
Restore a full user database backup.  
RESTORE DATABASE database_name   
    FROM DISK = '\\UNC_path\full_backup_directory'  
[;]  
  
Restore a full user database backup and then a differential backup.  
RESTORE DATABASE database_name  
    FROM DISK = '\\UNC_path\differential_backup_directory'   
    WITH [ ( ] BASE = '\\UNC_path\full_backup_directory' [ ) ]   
[;]  
  
Restore header information for a full or differential user database backup.  
RESTORE HEADERONLY   
    FROM DISK = '\\UNC_path\backup_directory'  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 RESTORE DATABASE *database_name*  
 Especifica para restaurar um banco de dados de usuário para um banco de dados chamado *database_name*. O banco de dados restaurado pode ter um nome diferente do banco de dados de origem que foi copiado em backup. *database_name* ainda não pode existir como um banco de dados no dispositivo de destino. Para obter mais detalhes sobre nomes de banco de dados permitidos, consulte "Regras de nomenclatura de objeto" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 A restauração de um banco de dados de usuário restaura um backup de banco de dados completo e, opcionalmente, em seguida, restaura um backup diferencial no dispositivo. Uma restauração de um banco de dados de usuário inclui a restauração de usuários e funções de banco de dados.  
  
 FROM DISK = '\\\\*UNC_path*\\*backup_directory*'  
 O caminho de rede e o diretório do qual o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] restaurará os arquivos de backup. Por exemplo, FROM DISK = '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'.  
  
 *backup_directory*  
 Especifica o nome de um diretório que contém o backup completo ou diferencial. Por exemplo, você pode executar uma operação RESTORE HEADERONLY em um backup completo ou diferencial.  
  
 *full_backup_directory*  
 Especifica o nome de um diretório que contém o backup completo.  
  
 *differential_backup_directory*  
 Especifica o nome do diretório que contém o backup diferencial.  
  
-   O caminho e o diretório de backup já devem existir e devem ser especificados como um caminho UNC (convenção de nomenclatura de universal) totalmente qualificado.  
  
-   O caminho para o diretório de backup não pode ser um caminho local e não pode ser um local em um dos nós de dispositivo do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
-   O tamanho máximo do caminho UNC e do nome do diretório de backup é de 200 caracteres.  
  
-   O servidor ou o host precisa ser especificado como um endereço IP.  
  
 RESTORE HEADERONLY  
 Especifica para retornar somente as informações de cabeçalho para um backup de banco de dados de usuário. Entre os outros campos, o cabeçalho inclui a descrição do texto do backup e o nome do backup. O nome do backup não precisa ter o mesmo nome do diretório que armazena os arquivos de backup.  
  
 Os resultados de RESTORE HEADERONLY seguem o mesmo padrão dos resultados de RESTORE HEADERONLY do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O resultado tem mais de 50 colunas, e nem todas são usadas pelo [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Para obter uma descrição das colunas nos resultados de RESTORE HEADERONLY do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **CREATE ANY DATABASE**.  
  
 Exige uma conta do Windows que tem permissão para acessar e ler por meio do diretório de backup. O nome de conta do Windows e a senha também precisam ser armazenados no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
1.  Para verificar se as credenciais já estão nesse local, use [sys.dm_pdw_network_credentials &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
2.  Para adicionar ou atualizar as credenciais, use [sp_pdw_add_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
3.  Para remover credenciais do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use [sp_pdw_remove_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
## <a name="error-handling"></a>Tratamento de erros  
 O comando RESTORE DATABASE resulta em erros nas seguintes condições:  
  
-   O nome do banco de dados a ser restaurado já existe no dispositivo de destino. Para evitar isso, escolha um nome exclusivo de banco de dados ou remova o banco de dados existente antes de executar a restauração.  
  
-   Há um conjunto inválido de arquivos de backup no diretório de backup.  
  
-   As permissões de logon não são suficientes para restaurar um banco de dados.  
  
-   O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] não tem as permissões corretas para o local de rede em que os arquivos de backup estão localizados.  
  
-   O local de rede para o diretório de backup não existe ou não está disponível.  
  
-   Não há espaço em disco suficiente nos nós de Computação ou no nó de Controle. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] não confirma se o espaço em disco suficiente existe no dispositivo antes de iniciar a restauração. Portanto, é possível gerar um erro de espaço em disco insuficiente ao executar a instrução RESTORE DATABASE. Quando não há espaço em disco suficiente, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] reverte a restauração.  
  
-   O dispositivo de destino no qual o banco de dados está sendo restaurado tem menos nós de Computação que o dispositivo de origem do qual o banco de dados foi copiado em backup.  
  
-   Houve uma tentativa de restauração do banco de dados em uma transação.  
  
## <a name="general-remarks"></a>Comentários gerais  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] acompanha o êxito das restaurações do banco de dados. Antes de restaurar um backup de banco de dados diferencial, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] verifica se a restauração do banco de dados completo foi concluída com êxito.  
  
 Após uma restauração, o banco de dados de usuário terá o nível de compatibilidade 120 do banco de dados. Isso é verdadeiro para todos os bancos de dados, seja qual for seu nível de compatibilidade original.  
  
 **Restaurando para um dispositivo com um número maior de nós de Computação**  
Execute [DBCC SHRINKLOG (SQL Data Warehouse do Azure)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) depois de restaurar um banco de dados de um dispositivo menor até o maior, pois a redistribuição aumentará o log de transações.  

A restauração de um backup em um dispositivo com um número maior de nós de Computação aumenta o tamanho do banco de dados alocado proporcionalmente ao número de nós de Computação.  
  
Por exemplo, ao restaurar um banco de dados de 60 GB de um dispositivo de 2 nós (30 GB por nó) em um dispositivo de 6 nós, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] cria um banco de dados de 180 GB (6 nós com 30 GB por nó) no dispositivo de 6 nós. Inicialmente, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] restaura o banco de dados em dois nós para que isso corresponda à configuração de origem e, em seguida, redistribui os dados para todos os seis nós.  
  
 Após a redistribuição, cada nó de Computação conterá menos dados reais e mais espaço livre do que cada nó de Computação no dispositivo de origem menor. Use o espaço adicional para adicionar mais dados ao banco de dados. Se o tamanho do banco de dados restaurado for maior do que o necessário, use [ALTER DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md) para reduzir os tamanhos de arquivos de banco de dados.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Para essas limitações e restrições, o dispositivo de origem é o dispositivo por meio do qual o backup do banco de dados foi criado e o dispositivo de destino é o dispositivo no qual o banco de dados será restaurado.  
  
 A restauração de um banco de dados não recompila as estatísticas automaticamente.  
  
 Apenas uma instrução RESTORE DATABASE ou BACKUP DATABASE pode ser executada no dispositivo em determinado momento. Se várias instruções de backup e restauração forem enviadas simultaneamente, o dispositivo as colocará em uma fila e as processará uma por vez.  
  
 Apenas é possível restaurar um backup de banco de dados em um dispositivo de destino do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] que tenha o mesmo número ou mais nós de Computação do que o dispositivo de origem. O dispositivo de destino não pode ter menos nós de Computação que o dispositivo de origem.  
  
 Não é possível restaurar um backup que foi criado em um dispositivo que tem o hardware do SQL Server 2012 PDW em um dispositivo que tem o hardware do SQL Server 2008 R2. Isso se aplica mesmo se o dispositivo foi adquirido originalmente com o hardware do SQL Server 2008 R2 PDW e agora executa o software do SQL Server 2012 PDW.  
  
## <a name="locking"></a>Bloqueio  
 Usa um bloqueio exclusivo no objeto DATABASE.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-restore-examples"></a>A. Exemplos simples de RESTORE  
 O exemplo a seguir restaura um backup completo para o banco de dados do `SalesInvoices2013`. Os arquivos de backup são armazenados no diretório \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full. O banco de dados SalesInvoices2013 ainda não pode existir no dispositivo de destino ou esse comando falhará com um erro.  
  
```  
RESTORE DATABASE SalesInvoices2013  
FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="b-restore-a-full-and-differential-backup"></a>B. Restaurar um backup completo e diferencial  
 O exemplo a seguir restaura um backup completo e, em seguida, um backup diferencial para o banco de dados SalesInvoices2013  
  
 O backup completo do banco de dados é restaurado do backup completo que está armazenado no diretório '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'. Se a restauração for concluída com êxito, o backup diferencial será restaurado no banco de dados SalesInvoices2013.  O backup diferencial é armazenado no diretório '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'.  
  
```  
RESTORE DATABASE SalesInvoices2013  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH BASE = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
  
```  
  
### <a name="c-restoring-the-backup-header"></a>C. Restaurando o cabeçalho do backup  
 Este exemplo restaura as informações de cabeçalho para o backup de banco de dados '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'. Os resultados do comando em uma linha de informações para o backup de Invoices2013Full.  
  
```  
RESTORE HEADERONLY  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
```  
  
 Use as informações de cabeçalho para verificar o conteúdo de um backup ou para garantir que o dispositivo de restauração de destino é compatível com o dispositivo de backup de origem antes de tentar restaurar o backup.  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md)  
  
  
