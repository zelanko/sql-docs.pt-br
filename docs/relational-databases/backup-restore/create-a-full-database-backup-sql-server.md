---
title: Criar um backup completo do banco de dados (SQL Server) | Microsoft Docs
ms.custom: sqlfreshmay19
ms.date: 05/29/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [SQL Server], full backups
- backing up databases [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- database backups [SQL Server], SQL Server Management Studio
ms.assetid: 586561fc-dfbb-4842-84f8-204a9100a534
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c90a3cf1f74eb588bd6faa657a3f47d7e57df453
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66403059"
---
# <a name="create-a-full-database-backup-sql-server"></a>Criar um backup completo de banco de dados (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este tópico descreve como criar um backup de banco de dados completo no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou PowerShell.  
  

Para obter informações sobre o backup do SQL Server no serviço de armazenamento de Blobs do Azure, veja [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) e [Backup do SQL Server para URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).  
  
##  <a name="Restrictions"></a> Limitações e restrições  
  
-   A instrução BACKUP não é permitida em uma transação explícita ou implícita.    
-   Os backups criados por uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem ser restaurados em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].   
-   Antes de prosseguir, confira uma visão geral e aprofundamento sobre os conceitos e tarefas de backup em [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
## <a name="Recommendations"></a> Recomendações  
  
-   À medida que um banco de dados aumenta de tamanho, os backups completos do banco de dados levam mais tempo para serem concluídos e exigem mais espaço de armazenamento. Para um banco de dados grande, considere complementar um backup de banco de dados completo com uma série de [backups de bancos de dados diferenciais](../../relational-databases/backup-restore/differential-backups-sql-server.md). Para saber mais, confira [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).    
-   Estime o tamanho de um backup de banco de dados completo usando o procedimento armazenado do sistema [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) .    
-   Por padrão, toda operação de backup bem-sucedida acrescenta uma entrada ao log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao log de eventos do sistema. Se você fizer backup com frequência, essas mensagens de êxito acumularão rapidamente, resultando em logs de erro grandes. Isso pode dificultar a localização de outras mensagens. Em tais situações, você pode suprimir essas entradas de log de backup usando o sinalizador de rastreamento 3226, caso nenhum dos seus scripts dependa dessas entradas. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
##  <a name="Security"></a> Segurança  
 TRUSTWORTHY é definido como OFF em um backup de banco de dados. Para obter informações sobre como definir TRUSTWORTHY como ON, veja [Opções do ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , as opções **PASSWORD** e **MEDIAPASSWORD** foram descontinuadas para a criação de backups. Você ainda poderá restaurar os backups criados com senhas.  
  
##  <a name="Permissions"></a> Permissões  
 As permissões BACKUP DATABASE e BACKUP LOG usam como padrão os membros da função de servidor fixa **sysadmin** e as funções de banco de dados fixas **db_owner** e **db_backupoperator** .  
  
 Os problemas de propriedade e permissão no arquivo físico do dispositivo de backup podem interferir em uma operação de backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser capaz de ler e gravar no dispositivo; a conta sob a qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa **deve** ter permissões de gravação. No entanto, [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), que adiciona uma entrada para um dispositivo de backup nas tabelas do sistema, não verifica permissões de acesso a arquivos. Esses problemas no arquivo físico do dispositivo de backup podem não aparecer até que o recurso físico seja acessado quando o backup ou restauração é tentado.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
>  Ao especificar uma tarefa de backup usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], é possível gerar o script [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) correspondente, clicando no botão **Script** e selecionando um destino para o script.  
  
### <a name="back-up-a-database"></a>Fazer o backup de um banco de dados  
  
1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], em **Pesquisador de Objetos**, clique no nome do servidor para expandir a árvore do servidor.    
1.  Expanda **Bancos de Dados**e selecione um banco de dados de usuário ou expanda **Bancos de Dados de Sistema** e selecione um banco de dados de sistema.    
1.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**e clique em **Backup**. Será exibida a caixa de diálogo **Backup de Banco de Dados** .  
1. Clique em **Banco de Dados** na lista suspensa. 
1. Na lista suspensa **Tipo de backup** , selecione **Completo**. 
1. Em **Componente de Backup**, clique em **Banco de Dados**. 
1. Na seção **Destino** , use a lista suspensa **Fazer backup em** para selecionar o destino do backup. Clique em **Adicionar** para adicionar outros objetos e/ou destinos de backup. Para remover um destino de backup, selecione-o e clique em **Remover**. Para exibir o conteúdo de um destino de backup existente, selecione-o e clique em **Conteúdo**.
1. (Opcionalmente) Examine as outras configurações disponíveis nas páginas **Opções de Mídia** e **Opções de Backup**. Para saber mais sobre as várias opções de backup, confira a [página Geral](back-up-database-general-page.md), a [página Opções de Mídia](back-up-database-media-options-page.md) e a [página Opções de Backup](back-up-database-backup-options-page.md). 



### <a name="additional-information"></a>Informações adicionais
- Depois de criar um backup de banco de dados completo, é possível criar um backup diferencial de banco de dados. Para saber mais, confira [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md).  
- Opcionalmente, você pode marcar a caixa de seleção **Backup somente cópia** para criar um backup somente cópia. Um *backup somente cópia* é um backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não depende da sequência de backups convencionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Backups somente cópia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  Um backup somente cópia não está disponível para o tipo de backup **Diferencial**.  
- A opção **Substituir mídia** poderá ser desabilitada na página **Opções de Mídia** se você estiver fazendo backup para URL. 


## <a name="ssms-examples"></a>Exemplos do SSMS  

Para os exemplos a seguir, crie um banco de dados de teste com o código Transact-SQL a seguir:

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest (
    ID INT NOT NULL PRIMARY KEY,
    c1 VARCHAR(100) NOT NULL,
    dt1 DATETIME NOT NULL DEFAULT getdate()
)
GO


USE [SQLTestDB]
GO

INSERT INTO SQLTest (ID, c1) VALUES (1, 'test1')
INSERT INTO SQLTest (ID, c1) VALUES (2, 'test2')
INSERT INTO SQLTest (ID, c1) VALUES (3, 'test3')
INSERT INTO SQLTest (ID, c1) VALUES (4, 'test4')
INSERT INTO SQLTest (ID, c1) VALUES (5, 'test5')
GO

SELECT * FROM SQLTest
GO
```

### <a name="a-full-back-up-to-disk-to-default-location"></a>A. Backup completo em disco em local padrão
Neste exemplo, será feito backup do banco de dados `SQLTestDB` em disco no local de backup padrão.  Nunca foi feito backup do `SQLTestDB`.
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do Mecanismo de Banco de Dados do SQL Server e expanda-a.
2.  Expanda **Banco de Dados**, clique com o botão direito do mouse em `SQLTestDB`, aponte para **Tarefas**e clique em **Fazer Backup...** .
3.  Escolha **OK**.

![Fazer backup do SQL](media/quickstart-backup-restore-database/backup-db-ssms.png) 
 

### <a name="b--full-back-up-to-disk-to-non-default-location"></a>**B.  Backup completo no disco em local não padrão**
Neste exemplo, será feito backup do banco de dados `SQLTestDB` em disco em `F:\MSSQL\BAK`.  Já foram feitos backups anteriores do `SQLTestDB` .
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do Mecanismo de Banco de Dados do SQL Server e expanda-a.
2.  Expanda **Banco de Dados**, clique com o botão direito do mouse em `Sales`, aponte para **Tarefas**e clique em **Fazer Backup...** .
3.  Na página **Geral** , na seção **Destino** , selecione a opção **Disco** na lista suspensa **Fazer backup em:** .
4.  Clique em **Remover** até que todos os arquivos de backup existentes sejam removidos.
5.  Clique em **Adicionar** e a caixa de diálogo **Selecionar Destino do Backup** será aberta.
6.  Insira `F:\MSSQL\BAK\Sales_20160801.bak` na caixa de texto **Nome de arquivo** .
7.  Escolha **OK**.
8.  Escolha **OK**.

![Alterar local do BD](media/create-a-full-database-backup-sql-server/change-db-location.png)

### <a name="c--create-an-encrypted-backup"></a>**C.  Criar um backup criptografado**
Neste exemplo, será feito backup do banco de dados `SQLTestDB` com criptografia no local de backup padrão.  

1.  No **Pesquisador de Objetos**, conecte-se a uma instância do Mecanismo de Banco de Dados do SQL Server e expanda-a.
1. Abra uma janela **Nova Consulta** e execute os seguintes comandos para criar uma [**chave mestra do banco de dados**](../../relational-databases/security/encryption/create-a-database-master-key.md) e um [**certificado**](../../t-sql/statements/create-certificate-transact-sql.md) no `SQLTestDB` banco de dados. 

    ```sql
    USE [SQLTestDB]
        
    -- Create the database master key
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
    
    
    -- Create the certificate
    CREATE CERTIFICATE MyCertificate   
    ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
    EXPIRY_DATE = '20201031';  
    GO  
    ```

1.  No **Pesquisador de Objetos**, expanda **Banco de Dados**, clique com o botão direito do mouse em `SQLTestDB`, aponte para **Tarefas** e clique em **Fazer Backup...** .
1.  Na página **Opções de Mídia** da seção **Substituir mídia**, clique em **Fazer backup em um novo conjunto de mídias e apagar todos os conjuntos de backup existentes**.
1.  Na página **Opções de Backup** da seção **Criptografia** , marque a caixa de seleção **Criptografar backup** .
1.  Na lista suspensa Algoritmo, clique em **AES 256**.
1.  Na lista suspensa **Certificado ou Chave Assimétrica** , selecione `MyCertificate`.
1.  Escolha **OK**.

![Backup criptografado](media/create-a-full-database-backup-sql-server/encrypted-backup.png)

### <a name="d--back-up-to-the-azure-blob-storage-service"></a>**D.  Fazer backup no serviço de armazenamento de Blobs do Azure**


Os três exemplos abaixo executam um backup completo do banco de dados do `Sales` no serviço de Armazenamento de Blobs do Microsoft Azure.  O nome da Conta de armazenamento é `mystorageaccount`.  O contêiner é chamado `myfirstcontainer`.  Para resumir, as quatro primeiras etapas são listadas aqui uma vez e todos os exemplos serão iniciados na **Etapa 5**.

1.  No **Pesquisador de Objetos**, conecte-se a uma instância do Mecanismo de Banco de Dados do SQL Server e expanda-a.
2.  Expanda **Banco de Dados**, clique com o botão direito do mouse em `Sales`, aponte para **Tarefas**e clique em **Fazer Backup...** .
3.  Na página **Geral** , na seção **Destino** , selecione a opção **URL** na lista suspensa **Fazer backup em:** .
4.  Clique em **Adicionar** e a caixa de diálogo **Selecionar Destino do Backup** será aberta.

#### <a name="striped-backup-to-url-and-a-sql-server-credential-already-exists"></a>Já existe um backup distribuído para URL e uma credencial do SQL Server

Uma política de acesso armazenado foi criada com direitos de leitura, gravação e listagem.  A credencial do SQL Server, `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`, foi criada usando uma Assinatura de Acesso Compartilhado associada à política de acesso armazenado.  

   5.   Selecione `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` do **contêiner de armazenamento do Azure:** caixa de texto
   6.  Na caixa de texto **Arquivo de Backup:** , digite `Sales_stripe1of2_20160601.bak`.
   7.  Clique em **OK**.
   8.  Repita as etapas de **4** e **5**.
   9.  Na caixa de texto **Arquivo de Backup:** , digite `Sales_stripe2of2_20160601.bak`.
   10.  Clique em **OK**.
   11.   Clique em **OK**.

#### <a name="a-shared-access-signature-exists-and-a-sql-server-credential-does-not-exist"></a>Existe uma assinatura de acesso compartilhado e não existe uma credencial do SQL Server

  5.    Digite `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` na caixa de texto **Contêiner de armazenamento do Azure:**  
  6.    Insira a assinatura de acesso compartilhado na caixa de texto **Política de Acesso Compartilhado:** .  
  7.    Clique em **OK**.  
  8.    Clique em **OK**.


#### <a name="a-shared-access-signature-does-not-exist"></a>Não há uma assinatura de acesso compartilhado

  5.    Clique no botão **Novo contêiner** e a caixa de diálogo **Conectar-se a uma Assinatura da Microsoft** será aberta.   
  6.    Conclua a caixa de diálogo **Conectar-se a uma Assinatura da Microsoft** e clique em **OK** para retornar à caixa de diálogo **Selecionar um destino de backup** .  Veja [Conectar-se a uma assinatura do Microsoft Azure](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md) para obter mais informações.  
  7.    Clique em **OK** na caixa de diálogo **Selecionar Destino do Backup** .  
  8.    Clique em **OK**.

  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
### <a name="create-a-full-database-backup"></a>Criar um backup de banco de dados completo  
  
1.  Execute a instrução BACKUP DATABASE para criar o backup do banco de dados completo, especificando:  
  
    -   O nome do banco de dados do qual fazer backup.   
    -   O dispositivo de backup em que o backup completo do banco de dados será gravado.    
     A sintaxe básica [!INCLUDE[tsql](../../includes/tsql-md.md)] para o backup de banco de dados completo é:  
  
     BACKUP DATABASE *database*  
       TO *backup_device* [ **,** ...*n* ]    
     [ WITH *com_opções* [ **,** ...*o* ] ] ;  
  
    |Opção|Descrição|  
    |------------|-----------------|  
    |*database*|É o banco de dados do qual fazer backup.|  
    |*backup_device* [ **,** ...*n* ]|Especifica uma lista de 1 a 64 dispositivos de backup a serem usados para a operação de backup. Você pode especificar um dispositivo de backup físico ou pode especificar um dispositivo de backup lógico correspondente, se já definido. Para especificar um dispositivo de backup físico, use a opção DISK ou TAPE:<br /><br /> { DISK &#124; TAPE } **=** _physical\_backup\_device\_name_<br /><br /> Para obter mais informações, consulte [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).|  
    |WITH *with_options* [ **,** ...*o* ]|Opcionalmente, especifica uma ou mais opções adicionais, *o*. Para obter informações sobre os fundamentos de opções, consulte a etapa 2.|  
  
2.  Opcionalmente, especifique uma ou mais opções WITH. Algumas opções WITH básicas são descritas aqui. Para obter informações sobre todas as opções WITH, consulte [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  

Opções WITH do conjunto de backup básico:

- **{ COMPRESSION | NO_COMPRESSION }** : No [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e versões posteriores somente, especifica se [compressão de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md) é executada neste backup, substituindo o padrão de nível de servidor. 
- **ENCRYPTION (ALGORITHM, SERVER CERTIFICATE |ASYMMETRIC KEY)** : No SQL Server 2014 ou em versões posteriores somente, especifique o algoritmo de criptografia a ser usado, e o certificado ou chave assimétrica usada para proteger a criptografia.
- **DESCRIPTION** **=** { **'** _text_ **'**  |  **@** _text\_variable_ }: Especifica o texto de forma livre que descreve o conjunto de backup. A cadeia de caracteres pode conter um máximo de 255 caracteres.  
- **NAME = { *backup_set_name* |  **@** _backup\_set\_name\_var_ }** : Especifica o nome do conjunto de backup. Os nomes podem ter no máximo de 128 caracteres. Se NAME não estiver especificado, ele estará em branco. 
  
 
Por padrão, BACKUP anexa o backup a um conjunto de mídias existente, preservando conjuntos de backup existentes. Para especificar isso explicitamente, use a opção NOINIT. Para obter informações sobre o acréscimo a conjuntos de backup existentes, consulte [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  

Alternativamente, para formatar a mídia de backup, use a opção FORMAT:  

FORMAT [ **,** MEDIANAME **=** { *media_name* |  **@** _media\_name\_variable_ } ] [ **,** MEDIADESCRIPTION **=** { *text* |  **@** _text\_variable_ } ]  
Use a cláusula FORMAT quando estiver usando a mídia pela primeira vez ou quando quiser sobrescrever todos os dados existentes Opcionalmente, atribua à nova mídia um nome e uma descrição.  

> [!IMPORTANT]  
>  Tenha muito cuidado ao usar a cláusula FORMAT ou a instrução BACKUP, pois isso destrói qualquer backup previamente armazenado na mídia de backup.  
  
##  <a name="TsqlExample"></a> Exemplos de Transact-SQL  
Para os exemplos a seguir, crie um banco de dados de teste com o código Transact-SQL a seguir:

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest (
    ID INT NOT NULL PRIMARY KEY,
    c1 VARCHAR(100) NOT NULL,
    dt1 DATETIME NOT NULL DEFAULT getdate()
)
GO


USE [SQLTestDB]
GO

INSERT INTO SQLTest (ID, c1) VALUES (1, 'test1')
INSERT INTO SQLTest (ID, c1) VALUES (2, 'test2')
INSERT INTO SQLTest (ID, c1) VALUES (3, 'test3')
INSERT INTO SQLTest (ID, c1) VALUES (4, 'test4')
INSERT INTO SQLTest (ID, c1) VALUES (5, 'test5')
GO

SELECT * FROM SQLTest
GO
```
  
#### <a name="a-back-up-to-a-disk-device"></a>**A. Fazer backup em um dispositivo de disco**  
 O exemplo a seguir faz backup de banco de dados completo `SQLTestDB` em um disco, usando `FORMAT` para criar um novo conjunto de mídia.  
  
```sql  
USE SQLTestDB;  
GO  
BACKUP DATABASE SQLTestDB  
TO DISK = 'Z:\SQLServerBackups\SQLTestDB.Bak'  
   WITH FORMAT,  
      MEDIANAME = 'Z_SQLServerBackups',  
      NAME = 'Full Backup of SQLTestDB';  
GO  
```  
  
#### <a name="b-back-up-to-a-tape-device"></a>**B. Fazer backup em um dispositivo de fita**  
 O exemplo a seguir faz backup do banco de dados completo `SQLTestDB` em fita, anexando o backup aos backups anteriores.  
  
```sql  
USE SQLTestDB;  
GO  
BACKUP DATABASE SQLTestDB  
   TO TAPE = '\\.\Tape0'  
   WITH NOINIT,  
      NAME = 'Full Backup of SQLTestDB';  
GO  
```  
  
#### <a name="c-back-up-to-a-logical-tape-device"></a>**C. Fazer backup em um dispositivo de fita lógico**  
 O exemplo a seguir cria um dispositivo de backup lógico para uma unidade de fita. Em seguida, o exemplo faz backup completo do banco de dados SQLTestDB nesse dispositivo.  
  
```sql  
-- Create a logical backup device,   
-- SQLTestDB_Bak_Tape, for tape device \\.\tape0.  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'SQLTestDB_Bak_Tape', '\\.\tape0'; USE SQLTestDB;  
GO  
BACKUP DATABASE SQLTestDB  
   TO SQLTestDB_Bak_Tape  
   WITH FORMAT,  
      MEDIANAME = 'SQLTestDB_Bak_Tape',  
      MEDIADESCRIPTION = '\\.\tape0',   
      NAME = 'Full Backup of SQLTestDB';  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
Use o cmdlet **Backup-SqlDatabase** . Para indicar explicitamente que este é um backup completo de banco de dados, especifique o parâmetro **-BackupAction**  com seu valor padrão **Database**. Esse parâmetro é opcional para backups completos de banco de dados.  

## <a name="powershell-examples"></a>Exemplos do PowerShell

### <a name="a--full-local-backup"></a>A.  Backup completo local 
O exemplo a seguir cria um backup de banco de dados completo do banco de dados `MyDB` para o local de backup padrão da instância de servidor `Computer\Instance`. Como opção, esse exemplo especifica **-BackupAction Database**.  
```powershell 
Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Database  
```
 
### <a name="b--full-backup-to-microsoft-azure"></a>B.  Backup completo para o Microsoft Azure 
O exemplo a seguir cria um backup completo do banco de dados `Sales` na instância `MyServer` para o serviço de Armazenamento de Blobs do Microsoft Azure.  Uma política de acesso armazenado foi criada com direitos de leitura, gravação e listagem.  A credencial do SQL Server, `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`, foi criada usando uma Assinatura de Acesso Compartilhado associada à política de acesso armazenado.  O comando do PowerShell usa o parâmetro **BackupFile** para especificar o local (URL) e o nome do arquivo de backup.

```powershell  
import-module sqlps;
$container = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer';
$FileName = 'Sales.bak';
$database = 'Sales';
$BackupFile = $container + '/' + $FileName ;
  
Backup-SqlDatabase -ServerInstance "MyServer" -Database $database -BackupFile $BackupFile;
```
 
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Fazer backup de um banco de dados (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
-   [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)
-   [Restaurar um backup de banco de dados no modelo de recuperação simples &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)
-   [Restaurar um banco de dados até o ponto de falha no modelo de recuperação completa &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)
-   [Restaurar um banco de dados em um novo local &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)
-   [Usar o Assistente de Plano de Manutenção](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>Confira também  
- [Solução de problemas de operações de backup e restauração do SQL Server](https://support.microsoft.com/kb/224071)
- [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)
- [Backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)
- [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)
- [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)
- [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
- [Fazer backup do banco de dados &#40;página Geral&#41;](../../relational-databases/backup-restore/back-up-database-general-page.md)
- [Fazer backup do banco de dados &#40;página Opções de Backup&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)
- [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)
- [Backups de bancos de dados completos &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)  
  
  
