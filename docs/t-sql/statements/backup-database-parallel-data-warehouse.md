---
title: Banco de dados de BACKUP (Parallel Data Warehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
ms.assetid: 73c8d465-b36b-4727-b9f3-368e98677c64
caps.latest.revision: 11
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4fb36fd89c02ff9ddd5bc33825a387b53ab6e174
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="backup-database-parallel-data-warehouse"></a>Banco de dados de BACKUP (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Cria um backup de um [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] de banco de dados e armazena o backup de desativar o dispositivo em um local de rede especificado pelo usuário. Use esta instrução com [RESTAURAR banco de dados &#40; Parallel Data Warehouse &#41; ](../../t-sql/statements/restore-database-parallel-data-warehouse.md) para recuperação de desastres, ou para copiar um banco de dados de um dispositivo para outro.  
  
 **Antes de começar a**, consulte "Adquirir e configurar um servidor de Backup" o [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Há dois tipos de backups em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Um *backup completo do banco de dados* é um backup de todo um [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] banco de dados. Um *backup de banco de dados diferencial* inclui apenas as alterações feitas desde o último backup completo. Um backup de um banco de dados do usuário inclui usuários de banco de dados e funções de banco de dados. Um backup do banco de dados mestre inclui logons.  
  
 Para obter mais informações sobre [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] backups de banco de dados, consulte "Backup e restauração" o [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 O nome do banco de dados no qual criar um backup. O banco de dados pode ser o banco de dados mestre ou um banco de dados do usuário.  
  
 PARA o disco = '\\\\*UNC_path*\\*backup_directory*'  
 O caminho de rede e o diretório no qual [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] gravará os arquivos de backup. Por exemplo, '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'.  
  
-   O caminho para o nome do diretório de backup já deve existir e deve ser especificado como um caminho UNC (convenção) de nomenclatura de universal totalmente qualificado.  
  
-   O diretório de backup, *backup_directory*, não deve existir antes de executar o comando de backup. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]criará o diretório de backup.  
  
-   O caminho para o diretório de backup não pode ser um caminho local e não pode ser um local em qualquer uma da [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] nós de dispositivo.  
  
-   O comprimento máximo do caminho UNC e o nome do diretório de backup é de 200 caracteres.  
  
-   O host ou servidor deve ser especificado como um endereço IP.  Não é possível especificá-lo como o nome de host ou servidor.  
  
 Descrição = **'***texto***'**  
 Especifica uma descrição textual do backup. O comprimento máximo do texto é de 255 caracteres.  
  
 A descrição é armazenada nos metadados e será exibida quando o cabeçalho do backup é restaurado com RESTORE HEADERONLY.  
  
 NOME = **'***Name backup***'**  
 Especifica o nome do backup. O nome do backup pode ser diferente do nome do banco de dados.  
  
-   Os nomes podem ter no máximo de 128 caracteres.  
  
-   Não é possível incluir um caminho.  
  
-   Deve começar com uma letra ou número de caracteres ou um sublinhado (_). Caracteres especiais permitidos são o sublinhado (\_), hífen (-) ou espaço (). Nomes de backup não podem terminar com um caractere de espaço.  
  
-   A instrução falhará se *backup_name* já existe no local especificado.  
  
 Esse nome é armazenado nos metadados e será exibida quando o cabeçalho do backup é restaurado com RESTORE HEADERONLY.  
  
 DIFFERENTIAL  
 Especifica para executar um backup diferencial de um banco de dados do usuário. Se omitido, o padrão é um backup de banco de dados completo. O nome do backup diferencial não precisa corresponder ao nome do backup completo. Para controlar o diferencial e seu backup completo correspondente, considere usando o mesmo nome com 'completo' ou 'diferença' anexada.  
  
 Por exemplo:  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerFull';`  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerDiff' WITH DIFFERENTIAL;`  
  
## <a name="permissions"></a>Permissões  
 Requer o **banco de dados de BACKUP** permissão ou associação no **db_backupoperator** função fixa de banco de dados. O banco de dados mestre não pode ser feito backup, mas por um usuário normal que foi adicionado para o **db_backupoperator** função fixa de banco de dados. O banco de dados mestre só pode ser feito por **sa**, o administrador de malha, ou membros do **sysadmin** função de servidor fixa.  
  
 Requer uma conta do Windows que tenha permissão para acessar, criar e gravar no diretório de backup. Você também deve armazenar o nome de conta do Windows e a senha em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Para adicionar essas credenciais de rede para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o [sp_pdw_add_network_credentials &#40; SQL Data Warehouse &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) procedimento armazenado.  
  
 Para obter mais informações sobre o gerenciamento de credenciais no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], consulte o [segurança](#Security) seção.  
  
## <a name="error-handling"></a>Tratamento de erros  
 Erros de banco de dados de BACKUP nas seguintes condições:  
  
-   Permissões de usuário não são suficientes para executar um backup.  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]não tem as permissões corretas para o local de rede onde o backup será armazenado.  
  
-   O banco de dados não existe.  
  
-   O diretório de destino já existe no compartilhamento de rede.  
  
-   O compartilhamento de rede de destino não está disponível.  
  
-   O compartilhamento de rede de destino não tem espaço suficiente para o backup. O comando de banco de dados de BACKUP não confirme a existência de espaço em disco suficiente antes de iniciar o backup, tornando possível gerar um erro de limite de espaço em disco durante a execução de BACKUP de banco de dados. Quando ocorre a espaço em disco insuficiente, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] reverte o comando de banco de dados de BACKUP. Para diminuir o tamanho do banco de dados, execute [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)  
  
-   Tentativa de iniciar um backup em uma transação.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Antes de executar um backup de banco de dados, use [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) para diminuir o tamanho do banco de dados. 
 
 Um [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] backup é armazenado como um conjunto de vários arquivos no mesmo diretório.  
  
 Um backup diferencial geralmente leva menos tempo que um backup completo e pode ser executado com mais frequência. Quando vários backups diferenciais se baseiam no mesmo backup completo, cada diferencial inclui todas as alterações no backup diferencial anterior.  
  
 Se você cancelar um comando BACKUP, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] removerá o diretório de destino e todos os arquivos criados para o backup. Se [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] perde a conectividade de rede para o compartilhamento, não é possível concluir a reversão.  
  
 Backups completos e backups diferenciais são armazenados em diretórios separados. Convenções de nomenclatura não são impostas para especificar que um backup completo e backup diferencial pertencem juntos. Você pode controlar isso por meio de suas próprias convenções de nomenclatura. Como alternativa, você pode controlar isso usando a opção de descrição com para adicionar uma descrição e, em seguida, usando a instrução RESTORE HEADERONLY para recuperar a descrição.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Não é possível executar um backup diferencial do banco de dados mestre. Há suporte para apenas backups completos de banco de dados mestre.  
  
 Os arquivos de backup são armazenados em um formato adequado para a restauração do backup para um [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dispositivo usando o [RESTAURAR banco de dados &#40; Parallel Data Warehouse &#41; ](../../t-sql/statements/restore-database-parallel-data-warehouse.md) instrução.  
  
 O backup com a instrução BACKUP DATABASE não pode ser usado para transferir informações de dados ou usuário para SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados. Para essa funcionalidade, você pode usar o recurso de cópia da tabela remota. Para obter mais informações, consulte "Cópia de tabela remota" a [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tecnologia para fazer backup e restaurar bancos de dados de backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Opções de backup são pré-configurados para usar a compactação de backup. Você não pode definir opções de backup, como compactação, soma de verificação, o tamanho de bloco e contagem do buffer.  
  
 Apenas um backup de banco de dados ou restauração pode executar no dispositivo em um determinado momento. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]comandos de backup ou restauração ficarão na fila até que o backup atual ou comando de restauração foi concluída.  
  
 O dispositivo de destino para restaurar o backup deve ter pelo menos o mesmo número de nós de computação como o dispositivo de origem. O destino pode ter mais nós de computação do que o dispositivo de origem, mas não pode ter menos nós de computação.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]Não rastrear o local e nomes de backups, desde que os backups são armazenados off o dispositivo.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]acompanhar o êxito ou falha de backups de banco de dados.  
  
 Um backup diferencial só será permitido se o último backup completo foi concluída com êxito. Por exemplo, suponha que na segunda-feira, você cria um backup completo do banco de dados de vendas e o backup for concluído com êxito. Em seguida, na terça-feira, você cria um backup completo do banco de dados de vendas e ele falhar. Após essa falha, em seguida, você não pode criar um backup diferencial com base no backup completo de segunda-feira. Primeiro você deve criar um backup completo com êxito antes de criar um backup diferencial.  
  
## <a name="metadata"></a>Metadados  
 Essas exibições de gerenciamento dinâmico contêm informações sobre todos os backup, restauração e operações de carregamento. As informações persistem entre as reinicializações do sistema.  
  
-   [sys.pdw_loader_backup_runs &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="performance"></a>Desempenho  
 Para executar um backup, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] primeiro faz backup dos metadados e, em seguida, ele executa um backup paralelo do banco de dados armazenados em nós de computação. Dados são copiados diretamente de cada nós de computação para o diretório de backup. Para obter o melhor desempenho para mover dados de nós de computação para o diretório de backup, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] controla o número de nós de computação que está copiando dados simultaneamente.  
  
## <a name="locking"></a>Bloqueio  
 Obtém um bloqueio de ExclusiveUpdate o objeto de banco de dados.  
  
##  <a name="Security"></a> Segurança  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]os backups não são armazenados no dispositivo. Portanto, sua equipe de TI é responsável por gerenciar todos os aspectos de segurança do backup. Por exemplo, isso inclui a gerenciar a segurança dos dados de backup, a segurança do servidor usado para armazenar backups e a segurança da infraestrutura de rede que conecta o servidor de backup para o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dispositivo.  
  
 **Gerenciar credenciais de rede**  
  
 Acesso à rede para o diretório de backup baseia-se a segurança de compartilhamento de arquivos de Windows padrão. Antes de executar um backup, você precisa criar ou designar uma conta do Windows que será usada para autenticar [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] para o diretório de backup. Essa conta do windows deve ter permissão para acessar, criar e gravar no diretório de backup.  
  
> [!IMPORTANT]  
>  Para reduzir os riscos de segurança com seus dados, é recomendável que você designa uma conta do Windows exclusivamente para fins de execução de backups e operações de restauração. Permitir que essa conta tem permissões para o local de backup e em nenhum outro lugar.  
  
 Você precisa armazenar o nome de usuário e senha na [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] executando o [sp_pdw_add_network_credentials &#40; SQL Data Warehouse &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) procedimento armazenado. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]usa o Gerenciador de credenciais do Windows para armazenar e criptografar os nomes de usuário e senhas no nó de controle e nós de computação. As credenciais não contam com o comando de banco de dados de BACKUP.  
  
 Para remover as credenciais de rede do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], consulte [sp_pdw_remove_network_credentials &#40; SQL Data Warehouse &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
 Para listar todas as credenciais de rede armazenados em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o [sys.dm_pdw_network_credentials &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) exibição de gerenciamento dinâmico.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-add-network-credentials-for-the-backup-location"></a>A. Adicionar as credenciais de rede para o local de backup  
 Para criar um backup, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] deve ter permissão de leitura/gravação para o diretório de backup. O exemplo a seguir mostra como adicionar as credenciais para um usuário. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]armazenará essas credenciais e usá-los para o backup e restaurar operações.  
  
> [!IMPORTANT]  
>  Por motivos de segurança, é recomendável criar uma conta de domínio exclusivamente para fins de execução de backups.  
  
```  
EXEC sp_pdw_add_network_credentials 'xxx.xxx.xxx.xxx', 'domain1\backupuser', '*****';  
```  
  
### <a name="b-remove-network-credentials-for-the-backup-location"></a>B. Remover as credenciais de rede para o local de backup  
 O exemplo a seguir mostra como remover as credenciais para um usuário de domínio de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
```  
EXEC sp_pdw_remove_network_credentials 'xxx.xxx.xxx.xxx';  
```  
  
### <a name="c-create-a-full-backup-of-a-user-database"></a>C. Criar um backup completo de um banco de dados do usuário  
 O exemplo a seguir cria um backup completo do banco de dados de usuário de faturas. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]criará o diretório Invoices2013 e salvará os arquivos de backup para o \\\10.192.63.147\backups\yearly\Invoices2013Full directory.  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="d-create-a-differential-backup-of-a-user-database"></a>D. Criar um backup diferencial de um banco de dados do usuário  
 O exemplo a seguir cria um backup diferencial, o que inclui todas as alterações feitas desde o último backup completo do banco de dados de faturas. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]criará o \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff diretório ao qual irá armazenar os arquivos. A descrição 'backup diferencial de faturas 2013' será armazenada com as informações de cabeçalho para o backup.  
  
 O backup diferencial só será executada com êxito se o último backup completo de faturas concluída com êxito.  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH DIFFERENTIAL,   
    DESCRIPTION = 'Invoices 2013 differential backup';  
```  
  
### <a name="e-create-a-full-backup-of-the-master-database"></a>E. Criar um backup completo do banco de dados mestre  
 O exemplo a seguir cria um backup completo do banco de dados mestre e o armazena no diretório '\\\10.192.63.147\backups\2013\daily\20130722\master'.  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master';  
```  
  
### <a name="f-create-a-backup-of-appliance-login-information"></a>F. Crie um backup das informações de logon de dispositivo.  
 O banco de dados mestre armazena as informações de logon de dispositivo. Para as informações de logon de dispositivo de backup é necessário backup master.  
  
 O exemplo a seguir cria um backup completo do banco de dados mestre.  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master'  
WITH (   
    DESCRIPTION = 'Master Backup 20130722',  
    NAME = 'login-backup'  
)  
;  
```  
  
## <a name="see-also"></a>Consulte também  
 [RESTAURAR banco de dados &#40; Parallel Data Warehouse &#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
  

