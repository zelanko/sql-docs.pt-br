---
title: RESTAURAR banco de dados (Parallel Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d915bfc1-e392-4a3a-9d94-08682cf3c864
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ba8aa12f38fce6ac00f88f0015008da25a59b88
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="restore-database-parallel-data-warehouse"></a>RESTAURAR o banco de dados (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Restaura um [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] banco de dados de usuário de um backup de banco de dados para um [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dispositivo. O banco de dados é restaurado de um backup que foi criado anteriormente a [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] [BACKUP de banco de dados &#40; Parallel Data Warehouse &#41; ](../../t-sql/statements/backup-database-parallel-data-warehouse.md) comando. Use o backup e restaurar operações para criar um plano de recuperação de desastres, ou mover bancos de dados de um dispositivo para outro.  
  
> [!NOTE]  
>  Restaurar mestre inclui restaurar informações de logon de dispositivo. Para restaurar um mestre, use o [restaurar o banco de dados mestre &#40; Transact-SQL &#41; ](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md) página o **do Configuration Manager** ferramenta. Um administrador com acesso ao nó de controle pode executar esta operação.  
  
 Para obter mais informações sobre [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] backups de banco de dados, consulte "Backup e restauração" o [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 RESTAURAR banco de dados *database_name*  
 Especifica para restaurar um banco de dados do usuário para um banco de dados chamado *database_name*. O banco de dados restaurado pode ter um nome diferente do banco de dados de origem que foi feito o backup. *Database_Name* não pode existir como um banco de dados no dispositivo de destino. Para obter mais detalhes sobre permitidos nomes de banco de dados, consulte "Regras de nomenclatura de objeto" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Restaurar um banco de dados de usuário restaura um backup de banco de dados completo e, opcionalmente, restaura um backup diferencial para o dispositivo. Uma restauração de um banco de dados do usuário inclui a restauração de usuários de banco de dados e funções de banco de dados.  
  
 FROM DISK = '\\\\*UNC_path*\\*backup_directory*'  
 O caminho de rede e o diretório do qual [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] irá restaurar os arquivos de backup. Por exemplo, do disco = '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'.  
  
 *backup_directory*  
 Especifica o nome de um diretório que contém o backup completo ou diferencial. Por exemplo, você pode executar uma operação de RESTORE HEADERONLY em um backup completo ou diferencial.  
  
 *full_backup_directory*  
 Especifica o nome de um diretório que contém o backup completo.  
  
 *differential_backup_directory*  
 Especifica o nome do diretório que contém o backup diferencial.  
  
-   O diretório de backup e caminho já deve existir e deve ser especificado como um caminho UNC (convenção) de nomenclatura de universal totalmente qualificado.  
  
-   O caminho para o diretório de backup não pode ser um caminho local e não pode ser um local em qualquer uma da [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] nós de dispositivo.  
  
-   O comprimento máximo do caminho UNC e o nome do diretório de backup é de 200 caracteres.  
  
-   O host ou servidor deve ser especificado como um endereço IP.  
  
 RESTORE HEADERONLY  
 Especifica para retornar somente as informações de cabeçalho de backup de banco de dados de um usuário. Entre os outros campos, o cabeçalho inclui a descrição de texto do backup e o nome do backup. O nome do backup não precisa ser o mesmo que o nome do diretório que armazena os arquivos de backup.  
  
 Resultados de RESTORE HEADERONLY em conformidade com a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resultados de RESTORE HEADERONLY. O resultado tem mais de 50 colunas, o que nem todos os usados pelo [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Para obter uma descrição das colunas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resultados de RESTORE HEADERONLY, consulte [RESTORE HEADERONLY &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-headeronly-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer o **CREATE ANY DATABASE** permissão.  
  
 Requer uma conta do Windows que tenha permissão para acessar e ler da pasta de backup. Você também deve armazenar o nome de conta do Windows e a senha em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
1.  Para verificar as credenciais são já nesse local, use [sys.dm_pdw_network_credentials &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
2.  Para adicionar ou atualizar as credenciais, use [sp_pdw_add_network_credentials &#40; SQL Data Warehouse &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
3.  Para remover as credenciais de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use [sp_pdw_remove_network_credentials &#40; SQL Data Warehouse &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
## <a name="error-handling"></a>Tratamento de erros  
 O comando RESTAURAR banco de dados resulta em erros nas seguintes condições:  
  
-   O nome do banco de dados para restaurar já existe no dispositivo de destino. Para evitar isso, escolha um nome exclusivo do banco de dados ou descartar o banco de dados existente antes de executar a restauração.  
  
-   Há um conjunto de arquivos de backup no diretório de backup inválido.  
  
-   As permissões de logon não são suficientes para restaurar um banco de dados.  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]não tem as permissões corretas para o local de rede onde se encontram os arquivos de backup.  
  
-   O local de rede para o diretório de backup não existe ou não está disponível.  
  
-   Não há espaço em disco insuficiente em nós de computação ou nó de controle. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]não confirma se o espaço em disco suficiente existe no dispositivo antes de iniciar a restauração. Portanto, é possível gerar um erro de limite de espaço em disco ao executar a instrução RESTORE DATABASE. Quando ocorre a espaço em disco insuficiente, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] reverte a restauração.  
  
-   O dispositivo de destino ao qual o banco de dados está sendo restaurado tem menos nós de computação que o dispositivo de origem do qual o banco de dados foi feito backup.  
  
-   Uma tentativa de restauração de banco de dados de dentro de uma transação.  
  
## <a name="general-remarks"></a>Comentários gerais  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]rastreia o sucesso da restauração do banco de dados. Antes de restaurar um backup de banco de dados diferencial, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] verifica a restauração completa do banco de dados foi concluída com êxito.  
  
 Após uma restauração, o banco de dados de usuário terá o nível de compatibilidade 120 do banco de dados. Isso é verdadeiro para todos os bancos de dados, independentemente de seu nível de compatibilidade original.  
  
 **Restaurando para um dispositivo com um número maior de nós de computação**  
Executar [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) depois de restaurar um banco de dados de um dispositivo do menor ao maior desde redistribuição aumentará o log de transações.  

Restaurar um backup para um dispositivo com um número maior de nós de computação aumenta o tamanho alocado do banco de dados proporcionalmente ao número de nós de computação.  
  
Por exemplo, quando restaurar 60 GB de banco de dados de um dispositivo de 2 nós (30 GB por nó) a um dispositivo de nó de 6, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] cria um banco de dados de 180 GB (6 nós com 30 GB por nó) no dispositivo do nó de 6. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]inicialmente restaura o banco de dados para 2 nós para corresponder à configuração de fonte e, em seguida, redistribui os dados para todos os nós de 6.  
  
 Após a redistribuição cada nó de computação contém menos dados reais e mais espaço livre do que cada nó de computação no dispositivo de origem menor. Use o espaço adicional para adicionar mais dados ao banco de dados. Se o tamanho do banco de dados restaurado é maior do que o necessário, você pode usar [ALTER DATABASE &#40; Parallel Data Warehouse &#41; ](../../t-sql/statements/alter-database-parallel-data-warehouse.md) para reduzir o tamanho dos arquivos de banco de dados.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Para essas limitações e restrições, o dispositivo de origem é o dispositivo do qual o backup do banco de dados foi criado e o dispositivo de destino é o dispositivo para o qual o banco de dados será restaurado.  
  
 Restaurar um banco de dados não recompilar estatísticas automaticamente.  
  
 Instrução apenas uma restauração do banco de dados ou banco de dados de BACKUP pode ser executado no dispositivo em um determinado momento. Se várias instruções de backup e restauração forem enviadas simultaneamente, o dispositivo será colocá-los em uma fila e processá-los um por vez.  
  
 Você só pode restaurar um backup de banco de dados para um [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dispositivo de destino que tenha o mesmo número ou mais nós de computação do que o dispositivo de origem. O dispositivo de destino não pode ter menos nós de computação que o dispositivo de origem.  
  
 Você não pode restaurar um backup que foi criado em um dispositivo que tem o hardware do PDW do SQL Server 2012 em um dispositivo que tem o hardware do SQL Server 2008 R2. Isso se aplica mesmo se o dispositivo foi adquirido originalmente com o hardware do PDW do SQL Server 2008 R2 e agora está executando o software do SQL Server 2012 PDW.  
  
## <a name="locking"></a>Bloqueio  
 Possui um bloqueio exclusivo no objeto de banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-restore-examples"></a>A. Exemplos de restauração simples  
 O exemplo a seguir restaura um backup completo para o `SalesInvoices2013` banco de dados. Os arquivos de backup são armazenados no \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full directory. O banco de dados SalesInvoices2013 não pode já existir no dispositivo de destino ou o comando falhará com um erro.  
  
```  
RESTORE DATABASE SalesInvoices2013  
FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="b-restore-a-full-and-differential-backup"></a>B. Restaurar um backup completo e diferencial  
 O exemplo a seguir restaura um completo e, em seguida, um backup diferencial para o banco de dados SalesInvoices2013  
  
 O backup completo do banco de dados é restaurado do backup completo que é armazenado no '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full' directory. Se a restauração for concluída com êxito, o backup diferencial é restaurado no banco de dados SalesInvoices2013.  O backup diferencial é armazenado no '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff' directory.  
  
```  
RESTORE DATABASE SalesInvoices2013  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH BASE = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
  
```  
  
### <a name="c-restoring-the-backup-header"></a>C. Restaurando o cabeçalho do backup  
 Este exemplo restaura as informações de cabeçalho para o backup do banco de dados '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'. Os resultados do comando em uma linha de informações para o backup de Invoices2013Full.  
  
```  
RESTORE HEADERONLY  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
```  
  
 Você pode usar as informações de cabeçalho para verificar o conteúdo de um backup ou para certificar-se de que o dispositivo de restauração de destino é compatível com o dispositivo de backup de origem antes de tentar restaurar o backup.  
  
## <a name="see-also"></a>Consulte também  
 [Banco de dados de BACKUP &#40; Parallel Data Warehouse &#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md)  
  
  
