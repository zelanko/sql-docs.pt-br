---
title: BACKUP DATABASE (Parallel Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 73c8d465-b36b-4727-b9f3-368e98677c64
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 41ad9d69b045a149bf6adad58f16f881ccc5d98e
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37783477"
---
# <a name="backup-database-parallel-data-warehouse"></a>BACKUP DATABASE (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Cria um backup de um banco de dados do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] e armazena o backup fora do dispositivo em um local de rede especificado pelo usuário. Use esta instrução com [RESTORE DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md) para recuperação de desastre ou para copiar um banco de dados de um dispositivo para outro.  
  
 **Antes de começar a**, confira "Adquirir e configurar um servidor de backup" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Há dois tipos de backup no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Um *backup completo de banco de dados* é um backup de um banco de dados inteiro do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Um *backup diferencial de banco de dados* inclui apenas as alterações feitas desde o último backup completo. Um backup de um banco de dados de usuário inclui os usuários do banco de dados e as funções do banco de dados. Um backup do banco de dados mestre inclui os logons.  
  
 Para obter mais informações sobre backups de banco de dados do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], confira "Backup e restauração" no [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
      Create a full backup of a user database or the master database.  
BACKUP DATABASE database_name  
    TO DISK = '\\UNC_path\backup_directory'  
    [ WITH [ ( ]  <with_options> [ ,...n ]  [ ) ] ]  
[;]  
  
Create a differential backup of a user database.  
BACKUP DATABASE database_name  
    TO DISK = '\\UNC_path\backup_directory'  
    WITH [ ( ] DIFFERENTIAL   
    [ , <with_options> [ ,...n ] [ ) ]  
[;]  
  
<with_options> ::=  
    DESCRIPTION = 'text'  
    | NAME = 'backup_name'  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 O nome do banco de dados no qual o backup será criado. O banco de dados pode ser o banco de dados mestre ou um banco de dados de usuário.  
  
 TO DISK = '\\\\*UNC_path*\\*backup_directory*'  
 O caminho e o diretório de rede em que o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] gravará os arquivos de backup. Por exemplo, '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'.  
  
-   O caminho para o nome do diretório de backup já precisa existir e estar especificado como um caminho UNC totalmente qualificado.  
  
-   O diretório de backup, *backup_directory*, não pode existir antes da execução do comando de backup. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] criará o diretório de backup.  
  
-   O caminho para o diretório de backup não pode ser um caminho local e não pode ser um local em um dos nós de dispositivo do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
-   O tamanho máximo do caminho UNC e do nome do diretório de backup é de 200 caracteres.  
  
-   O servidor ou o host precisa ser especificado como um endereço IP.  Não é possível especificá-lo como o nome de host ou do servidor.  
  
 DESCRIPTION = **'***text***'**  
 Especifica uma descrição textual do backup. O comprimento máximo do texto é de 255 caracteres.  
  
 A descrição é armazenada nos metadados e será exibida quando o cabeçalho do backup for restaurado com RESTORE HEADERONLY.  
  
 NAME = **'***backup _name***'**  
 Especifica o nome do backup. O nome do backup pode ser diferente do nome do banco de dados.  
  
-   Os nomes podem ter no máximo de 128 caracteres.  
  
-   Não é possível incluir um caminho.  
  
-   É necessário começar com um caractere de letra ou de número ou com um sublinhado (_). Os caracteres especiais permitidos são sublinhado (\_), hífen (-) ou espaço (). Os nomes de backup não podem terminar com um caractere de espaço.  
  
-   A instrução falhará se *backup_name* já existir no local especificado.  
  
 Esse nome é armazenado nos metadados e será exibido quando o cabeçalho do backup for restaurado com RESTORE HEADERONLY.  
  
 DIFFERENTIAL  
 Especifica a execução de um backup diferencial de um banco de dados de usuário. Se omitido, o padrão será um backup completo do banco de dados. O nome do backup diferencial não precisa corresponder ao nome do backup completo. Para controlar o diferencial e seu backup completo correspondente, considere usar o mesmo nome com 'completo' ou 'diferencial' anexado.  
  
 Por exemplo:  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerFull';`  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerDiff' WITH DIFFERENTIAL;`  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **BACKUP DATABASE** ou a associação à função de banco de dados fixa **db_backupoperator**. O banco de dados mestre não pode ser submetido a backup simplesmente por um usuário normal que tenha sido adicionado à função de banco de dados fixa **db_backupoperator**. O banco de dados mestre somente pode ser submetido a backup pela **SA**, pelo administrador da malha ou pelos membros da função de servidor fixa **sysadmin**.  
  
 Requer uma conta do Windows que tenha permissão para acessar, criar e gravar no diretório de backup. O nome de conta do Windows e a senha também precisam ser armazenados no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Para adicionar essas credenciais de rede no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o procedimento armazenado [sp_pdw_add_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
 Para obter mais informações sobre o gerenciamento de credenciais no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], confira a seção [Segurança](#Security).  
  
## <a name="error-handling"></a>Tratamento de erros  
 Erros de BACKUP DATABASE nas seguintes condições:  
  
-   As permissões de usuário não são suficientes para executar um backup.  
  
-   O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] não tem as permissões corretas para o local de rede no qual backup será armazenado.  
  
-   O banco de dados não existe.  
  
-   O diretório de destino já existe no compartilhamento de rede.  
  
-   O compartilhamento de rede de destino não está disponível.  
  
-   O compartilhamento de rede de destino não tem espaço suficiente para o backup. O comando BACKUP DATABASE não confirma a existência de espaço em disco suficiente antes de iniciar o backup, possibilitando a geração de um erro de falta de espaço em disco durante a execução de BACKUP DATABASE. Quando ocorrer falta de espaço em disco suficiente, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] reverterá o comando BACKUP DATABASE. Para diminuir o tamanho do banco de dados, execute [DBCC SHRINKLOG (SQL Data Warehouse do Azure)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)  
  
-   Tentativa de iniciar um backup em uma transação.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Antes de executar um backup de banco de dados, use [DBCC SHRINKLOG (SQL Data Warehouse do Azure)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) para diminuir o tamanho do banco de dados. 
 
 Um backup do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] é armazenado como um conjunto de vários arquivos no mesmo diretório.  
  
 Um backup diferencial geralmente leva menos tempo do que um backup completo e pode ser executado com mais frequência. Quando vários backups diferenciais se baseiam no mesmo backup completo, cada diferencial inclui todas as alterações do backup diferencial anterior.  
  
 Se você cancelar um comando BACKUP, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] removerá o diretório de destino e todos os arquivos criados para o backup. Se o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] perder a conectividade de rede com o compartilhamento, não será possível concluir a reversão.  
  
 Os backups completos e os backups diferenciais são armazenados em diretórios separados. Não são impostas convenções de nomenclatura para especificar que um backup completo e um backup diferencial se pertencem. Controle isso usando suas próprias convenções de nomenclatura. Como alternativa, você pode controlar isso usando a opção WITH DESCRIPTION para adicionar uma descrição e, em seguida, usando a instrução RESTORE HEADERONLY para recuperar a descrição.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Não é possível executar um backup diferencial do banco de dados mestre. Apenas os backups completos do banco de dados mestre são compatíveis.  
  
 Os arquivos de backup são armazenados em um formato adequado para a restauração do backup em um dispositivo do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] usando a instrução [RESTORE DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md).  
  
 O backup com a instrução BACKUP DATABASE não pode ser usado para transferir dados ou informações de usuário para bancos de dados de SMP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para essa funcionalidade, você pode usar o recurso de cópia de tabela remota. Para obter mais informações, consulte "Cópia de tabela remota" na [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] usa a tecnologia de backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer backup e restaurar bancos de dados. As opções de backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são pré-configuradas para usar a compactação de backup. Não é possível definir as opções de backup, como compactação, soma de verificação, tamanho de bloco e contagem de buffer.  
  
 Apenas um backup de banco de dados ou uma restauração pode ser executada no dispositivo de cada vez. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] coloca os comandos de backup ou restauração na fila até que o comando de backup ou de restauração atual seja concluído.  
  
 O dispositivo de destino para restaurar o backup precisa ter pelo menos o mesmo número de nós de computação que o dispositivo de origem. O destino pode ter mais nós de computação do que o dispositivo de origem, mas não pode ter menos.  
  
 O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] não rastreia o local e os nomes de backups, pois os backups são armazenados fora do dispositivo.  
  
 O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] acompanha o êxito ou a falha dos backups de banco de dados.  
  
 Um backup diferencial só será permitido se o último backup completo tiver sido concluído com êxito. Por exemplo, suponha que na segunda-feira você crie um backup completo do banco de dados de vendas e o backup seja concluído com êxito. Na terça-feira, você cria um backup completo do banco de dados de vendas e ele falha. Após essa falha, não será possível criar um backup diferencial com base no backup completo de segunda-feira. Primeiro você deverá criar um backup completo com êxito antes de criar um backup diferencial.  
  
## <a name="metadata"></a>Metadados  
 Essas exibições de gerenciamento dinâmico contêm informações sobre todos os backup, as restauração e as operações de carregamento. As informações persistem entre os reinícios do sistema.  
  
-   [sys.pdw_loader_backup_runs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="performance"></a>Desempenho  
 Para executar um backup, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] primeiro faz backup dos metadados e, em seguida, executa um backup paralelo dos dados do banco de dados armazenados nos nós de computação. Os dados são copiados diretamente de cada nó de computação para o diretório de backup. Para obter o melhor desempenho para mover dados dos nós de computação para o diretório de backup, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] controla o número de nós de computação que estão copiando dados simultaneamente.  
  
## <a name="locking"></a>Bloqueio  
 Coloca um bloqueio ExclusiveUpdate no objeto DATABASE.  
  
##  <a name="Security"></a> Segurança  
 Os backups do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] não são armazenados no dispositivo. Portanto, sua equipe de TI é responsável por gerenciar todos os aspectos de segurança do backup. Por exemplo, isso inclui gerenciar a segurança dos dados de backup, a segurança do servidor usado para armazenar os backups e a segurança da infraestrutura de rede que conecta o servidor de backup ao dispositivo do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 **Gerenciar credenciais de rede**  
  
 O acesso da rede ao diretório de backup baseia-se na segurança de compartilhamento de arquivos padrão do Windows. Antes de executar um backup, você precisa criar ou designar uma conta do Windows que será usada para autenticar o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] no diretório de backup. Essa conta do Windows precisa ter permissão para acessar, criar e gravar no diretório de backup.  
  
> [!IMPORTANT]  
>  Para reduzir os riscos de segurança para seus dados, é recomendável designar uma conta do Windows exclusivamente para a finalidade de executar operações de backup e restauração. Permita que essa conta tenha permissões para o local de backup e não tenha para nenhum outro lugar.  
  
 Você precisa armazenar o nome de usuário e a senha no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] executando o procedimento armazenado [sp_pdw_add_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md). O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] usa o Gerenciador de Credenciais do Windows para armazenar e criptografar os nomes de usuário e as senhas no nó de controle e nos nós de computação. As credenciais não são submetidas a backup com o comando BACKUP DATABASE.  
  
 Para remover as credenciais de rede do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], confira [sp_pdw_remove_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
 Para listar todas as credenciais de rede armazenadas no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use a exibição de gerenciamento dinâmico [sys.dm_pdw_network_credentials &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-add-network-credentials-for-the-backup-location"></a>A. Adicionar as credenciais de rede para o local de backup  
 Para criar um backup, o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] precisa ter permissão de leitura/gravação para o diretório de backup. O exemplo a seguir mostra como adicionar as credenciais para um usuário. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] armazenará essas credenciais e as usará para as operações de backup e restauração.  
  
> [!IMPORTANT]  
>  Por motivos de segurança, é recomendável criar uma conta de domínio exclusivamente para a finalidade de executar backups.  
  
```  
EXEC sp_pdw_add_network_credentials 'xxx.xxx.xxx.xxx', 'domain1\backupuser', '*****';  
```  
  
### <a name="b-remove-network-credentials-for-the-backup-location"></a>B. Remover as credenciais de rede do local de backup  
 O exemplo a seguir mostra como remover as credenciais de um usuário de domínio do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
```  
EXEC sp_pdw_remove_network_credentials 'xxx.xxx.xxx.xxx';  
```  
  
### <a name="c-create-a-full-backup-of-a-user-database"></a>C. Criar um backup completo de um banco de dados de usuário  
 O exemplo a seguir cria um backup completo do banco de dados de usuário de faturas. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] criará o diretório Invoices2013 e salvará os arquivos de backup no diretório \\\10.192.63.147\backups\yearly\Invoices2013Full.  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="d-create-a-differential-backup-of-a-user-database"></a>D. Criar um backup diferencial de um banco de dados de usuário  
 O exemplo a seguir cria um backup diferencial, que inclui todas as alterações feitas desde o último backup completo do banco de dados de faturas. O [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] criará o diretório \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff no qual armazenará os arquivos. A descrição 'Invoices 2013 differential backup' será armazenada com as informações de cabeçalho do backup.  
  
 O backup diferencial só será executado com êxito se o último backup completo do banco de dados de faturas for concluído com êxito.  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH DIFFERENTIAL,   
    DESCRIPTION = 'Invoices 2013 differential backup';  
```  
  
### <a name="e-create-a-full-backup-of-the-master-database"></a>E. Criar um backup completo do banco de dados mestre  
 O exemplo a seguir cria um backup completo do banco de dados mestre e armazena-o no diretório '\\\10.192.63.147\backups\2013\daily\20130722\master'.  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master';  
```  
  
### <a name="f-create-a-backup-of-appliance-login-information"></a>F. Criar um backup das informações de logon do dispositivo.  
 O banco de dados mestre armazena as informações de logon do dispositivo. Para fazer backup das informações de logon do dispositivo é necessário fazer o backup do mestre.  
  
 O exemplo a seguir cria um backup completo do banco de dados mestre.  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master'  
WITH (   
    DESCRIPTION = 'Master Backup 20130722',  
    NAME = 'login-backup'  
)  
;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [RESTORE DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
  
