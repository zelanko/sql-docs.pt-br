---
title: Criar um backup completo de banco de dados | Microsoft Docs
ms.custom: sqlfreshmay19
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: carlrab
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
ms.openlocfilehash: fe0c9a950221317cb4a9088bae7629fc0c894165
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71710318"
---
# <a name="create-a-full-database-backup"></a>Criar um backup de banco de dados completo

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este tópico descreve como criar um backup de banco de dados completo no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou PowerShell.

Para obter informações sobre o backup do SQL Server no serviço do Armazenamento de Blobs do Azure, confira [Backup e restauração do SQL Server com o serviço de Armazenamento de Blobs do Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) e [Backup do SQL Server para URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).

## <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições

- A instrução `BACKUP` não é permitida em uma transação explícita ou implícita.
- Os backups criados por uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem ser restaurados em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Antes de prosseguir, confira uma visão geral e aprofundamento sobre os conceitos e tarefas de backup em [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).

## <a name="recommendations"></a><a name="Recommendations"></a> Recomendações

- À medida que um banco de dados aumenta de tamanho, os backups completos do banco de dados levam mais tempo para serem concluídos e exigem mais espaço de armazenamento. Para bancos de dados grandes, considere complementar backups de banco de dados completos com uma série de [backups de bancos de dados diferenciais](../../relational-databases/backup-restore/differential-backups-sql-server.md).
- Estime o tamanho de um backup de banco de dados completo usando o procedimento armazenado do sistema [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) .
- Por padrão, toda operação de backup bem-sucedida acrescenta uma entrada ao log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao log de eventos do sistema. Se você fizer backup com frequência, essas mensagens de êxito acumularão rapidamente, resultando em logs de erro grandes. Isso pode dificultar a localização de outras mensagens. Em tais situações, você pode suprimir essas entradas de log de backup usando o sinalizador de rastreamento 3226, caso nenhum dos seus scripts dependa dessas entradas. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).

## <a name="security"></a><a name="Security"></a> Segurança

**TRUSTWORTHY** é definido como OFF em um backup de banco de dados. Para obter informações sobre como definir **TRUSTWORTHY** como ON, confira [Opções de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).

Começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], as opções **PASSWORD** e **MEDIAPASSWORD** foram descontinuadas para a criação de backups. Você ainda poderá restaurar os backups criados com senhas.

## <a name="permissions"></a><a name="Permissions"></a> Permissões

As permissões `BACKUP DATABASE` e `BACKUP LOG` usam como padrão os membros da função de servidor fixa **sysadmin** e as funções de banco de dados fixas **db_owner** e **db_backupoperator**.

 Os problemas de propriedade e permissão no arquivo físico do dispositivo de backup podem interferir em uma operação de backup. O serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisa ter a capacidade de leitura e gravação no dispositivo, o que significa que a conta na qual o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado precisa ter as permissões de gravação no dispositivo de backup. No entanto, [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), que adiciona uma entrada para um dispositivo de backup nas tabelas do sistema, não verifica permissões de acesso a arquivos. Como resultado, os problemas no arquivo físico do dispositivo de backup podem não aparecer até que o recurso físico seja acessado quando o backup ou restauração é tentado.

## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio

> [!NOTE]
> Ao especificar uma tarefa de backup usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], é possível gerar o script [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) correspondente, clicando no botão **Script** e selecionando um destino para o script.

1. Depois de se conectar à instância adequada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no **Pesquisador de Objetos**, expanda a árvore do servidor.

1. Expanda **Bancos de Dados**e selecione um banco de dados de usuário ou expanda **Bancos de Dados de Sistema** e selecione um banco de dados de sistema.

1. Clique com o botão direito do mouse no banco de dados do qual deseja fazer backup, aponte para **Tarefas** e clique em **Fazer Backup...** .

1. Na caixa de diálogo **Fazer Backup do Banco de Dados**, o banco de dados selecionado aparece na lista suspensa (que você pode alterar para qualquer outro banco de dados no servidor).

1. Na lista suspensa **Tipo de backup**, selecione o tipo de backup desejado, o padrão é **Completo**.

   > [!IMPORTANT]
   > É necessário executar pelo menos um backup de banco de dados completo antes de ser possível executar um backup diferencial ou de log de transações.
   
1. Em **Componente de Backup**, clique em **Banco de Dados**.

1. Na seção **Destino**, examine a localização padrão para o arquivo de backup (na pasta ../mssql/data).

   Para fazer backup em um dispositivo diferente, altere a seleção usando a lista suspensa **Fazer backup em**. Para distribuir o conjunto de backup em vários arquivos para aumentar a velocidade do backup, clique em **Adicionar** para adicionar objetos e/ou destinos adicionais.
 
   Para remover um destino de backup, selecione-o e clique em **Remover**. Para exibir o conteúdo de um destino de backup existente, selecione-o e clique em **Conteúdo**.

1. (opcional) Examine as outras configurações disponíveis nas páginas **Opções de Mídia** e **Opções de Backup**.

   Para saber mais sobre as várias opções de backup, confira a [página Geral](back-up-database-general-page.md), a [página Opções de Mídia](back-up-database-media-options-page.md) e a [página Opções de Backup](back-up-database-backup-options-page.md).

1. Clique em **OK** para iniciar o backup.

1. Quando o backup for concluído com êxito, clique em **OK** para fechar a caixa de diálogo do SQL Server Management Studio.

### <a name="additional-information"></a>Informações adicionais

- Após criar um backup de banco de dados completo, você pode criar um [backup de banco de dados diferencial](create-a-differential-database-backup-sql-server.md) ou um [backup de log de transações](back-up-a-transaction-log-sql-server.md).

- (opcional) Marque a caixa de seleção **Backup somente cópia** para criar um backup somente cópia. Um *backup somente cópia* é um backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não depende da sequência de backups convencionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Backups somente cópia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md). Um backup somente cópia não está disponível para o tipo de backup **Diferencial**.

- A opção **Substituir mídia** estará desabilitada na página **Opções de Mídia** se você estiver fazendo backup para URL.

### <a name="examples"></a>Exemplos

Para os exemplos a seguir, crie um banco de dados de teste com o código Transact-SQL a seguir:

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest
   (
      ID INT NOT NULL PRIMARY KEY,
      c1 VARCHAR(100) NOT NULL,
      dt1 DATETIME NOT NULL DEFAULT getdate()
   );
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

#### <a name="a-full-back-up-to-disk-to-default-location"></a>a. Backup completo em disco em local padrão

Neste exemplo, será feito backup do banco de dados `SQLTestDB` em disco no local de backup padrão.

1. Depois de se conectar à instância adequada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no **Pesquisador de Objetos**, expanda a árvore do servidor.

1. Expanda **Banco de Dados**, clique com o botão direito do mouse em `SQLTestDB`, aponte para **Tarefas**e clique em **Fazer Backup...** .

1. Clique em **OK**.

1. Quando o backup for concluído com êxito, clique em **OK** para fechar a caixa de diálogo do SQL Server Management Studio.

![Fazer backup do SQL](media/quickstart-backup-restore-database/backup-db-ssms.png)

#### <a name="b-full-back-up-to-disk-to-non-default-location"></a>B. Backup completo em disco em local não padrão

Neste exemplo, o banco de dados `SQLTestDB` terá o backup feito em um disco em uma localização de sua escolha.

1. Depois de se conectar à instância adequada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no **Pesquisador de Objetos**, expanda a árvore do servidor.

1. Expanda **Banco de Dados**, clique com o botão direito do mouse em `SQLTestDB`, aponte para **Tarefas**e clique em **Fazer Backup...** .

1. Na página **Geral** , na seção **Destino** , selecione a opção **Disco** na lista suspensa **Fazer backup em:** .

1. Clique em **Remover** até que todos os arquivos de backup existentes sejam removidos.

1. Clique em **Adicionar** e a caixa de diálogo **Selecionar Destino do Backup** será aberta.

1. Insira um caminho e um nome de arquivo válidos na caixa de texto **Nome do arquivo** e use **.bak** como extensão para simplificar a classificação desse arquivo.

1. Clique em **OK** e em **OK** novamente para iniciar o backup.

1. Quando o backup for concluído com êxito, clique em **OK** para fechar a caixa de diálogo do SQL Server Management Studio.

![Alterar local do BD](media/create-a-full-database-backup-sql-server/change-db-location.png)

#### <a name="c-create-an-encrypted-backup"></a>C. Criar um backup criptografado

Neste exemplo, será feito backup do banco de dados `SQLTestDB` com criptografia no local de backup padrão.

1. Depois de se conectar à instância adequada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no **Pesquisador de Objetos**, expanda a árvore do servidor.

1. Expanda **Bancos de dados**, **Bancos de Dados do Sistema**, clique com o botão direito do mouse em `master` e clique em **Nova Consulta** para abrir uma janela de consulta com uma conexão com seu banco de dados `SQLTestDB`.

1. Execute os seguintes comandos para criar uma [**chave mestra do banco de dados**](../../relational-databases/security/encryption/create-a-database-master-key.md) e um [**certificado**](../../t-sql/statements/create-certificate-transact-sql.md) no banco de dados `master`.  

   ```sql
   -- Create the master key
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  

   -- If the master key already exists, open it in the same session that you create the certificate (see next step)
   OPEN MASTER KEY DECRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe'

   -- Create the certificate encrypted by the master key
   CREATE CERTIFICATE MyCertificate
   WITH SUBJECT = 'Backup Cert', EXPIRY_DATE = '20201031';  
   ```

1. No **Pesquisador de Objetos**, no nó **Banco de Dados**, clique com o botão direito do mouse em `SQLTestDB`, aponte para **Tarefas** e clique em **Fazer Backup...** .

1. Na página **Opções de Mídia** da seção **Substituir mídia**, clique em **Fazer backup em um novo conjunto de mídias e apagar todos os conjuntos de backup existentes**.

1. Na página **Opções de Backup** da seção **Criptografia** , marque a caixa de seleção **Criptografar backup** .

1. Na lista suspensa Algoritmo, clique em **AES 256**.

1. Na lista suspensa **Certificado ou Chave Assimétrica** , selecione `MyCertificate`.

1. Selecione **OK**.

![Backup criptografado](media/create-a-full-database-backup-sql-server/encrypted-backup.png)

#### <a name="d-back-up-to-the-azure-blob-storage-service"></a>D. Fazer backup no serviço de Armazenamento de Blobs do Azure

O exemplo abaixo faz um backup completo de banco de dados do `SQLTestDB` no serviço de Armazenamento de Blobs do Azure. Esse exemplo assume que você já tem uma conta de armazenamento com um contêiner de blobs. Esse exemplo cria uma assinatura de acesso compartilhado para você. Esse exemplo falha se o contêiner tiver uma assinatura de acesso compartilhado existente.

Se você não tiver um contêiner de blobs do Azure em uma conta de armazenamento, crie um antes de continuar. Para obter mais informações, confira [Criar uma conta de armazenamento de uso geral](https://docs.microsoft.com/azure/storage/common/storage-quickstart-create-account?tabs=azure-portal) e [Criar um contêiner](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal#create-a-container).

1. Depois de se conectar à instância adequada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no **Pesquisador de Objetos**, expanda a árvore do servidor.

1. Expanda **Banco de Dados**, clique com o botão direito do mouse em `SQLTestDB`, aponte para **Tarefas**e clique em **Fazer Backup...** .

1. Na página **Geral** , na seção **Destino** , selecione a opção **URL** na lista suspensa **Fazer backup em:** .

1. Clique em **Adicionar** e a caixa de diálogo **Selecionar Destino do Backup** será aberta.

1. Se você tiver registrado anteriormente o contêiner de armazenamento do Azure que deseja usar com o SQL Server Management Studio, selecione-o. Caso contrário, clique em **Novo contêiner** para registrar um novo contêiner.

1. Na caixa de diálogo **Conectar-se a uma Assinatura da Microsoft**, entre na sua conta.

1. Na caixa de texto suspensa **Selecionar Conta de Armazenamento**, selecione sua conta de armazenamento.

1. Na caixa de texto suspensa **Selecionar Contêiner de Blobs**, selecione seu contêiner de blobs.

1. Na caixa de calendário suspensa **Expiração da Política de Acesso Compartilhado**, selecione uma data de validade para a política de acesso compartilhado que você criou nesse exemplo.

1. Clique em **Criar Credencial** para gerar uma assinatura de acesso compartilhado e uma credencial no SQL Server Management Studio.

1. Clique em **OK** para fechar a caixa de diálogo **Conectar-se a uma Assinatura da Microsoft**.

1. Na caixa de texto **Arquivo de Backup**, modifique o nome do arquivo de backup (opcional).

1. Clique em **OK** para fechar a caixa de diálogo **Selecionar um destino de backup**.

1. Clique em **OK** para iniciar o backup.

1. Quando o backup for concluído com êxito, clique em **OK** para fechar a caixa de diálogo do SQL Server Management Studio.

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL

Crie um backup completo de banco de dados executando a instrução `BACKUP DATABASE` especificando:

- O nome do banco de dados do qual fazer backup.
- O dispositivo de backup em que o backup completo do banco de dados será gravado.

A sintaxe básica [!INCLUDE[tsql](../../includes/tsql-md.md)] para o backup de banco de dados completo é:

 BACKUP DATABASE *database* TO *backup_device* [ **,** ...*n* ] [ WITH *with_options* [ **,** ...*o* ] ] ;

|Opção|Descrição|
|------------|-----------------|
|*database*|É o banco de dados do qual fazer backup.|
|*backup_device* [ **,** ...*n* ]|Especifica uma lista de 1 a 64 dispositivos de backup a serem usados para a operação de backup. Você pode especificar um dispositivo de backup físico ou pode especificar um dispositivo de backup lógico correspondente, se já definido. Para especificar um dispositivo de backup físico, use a opção DISK ou TAPE:<br /><br /> { DISK &#124; TAPE } **=** _physical\_backup\_device\_name_<br /><br /> Para obter mais informações, consulte [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).|
|WITH *with_options* [ **,** ...*o* ]|Opcionalmente, especifica uma ou mais opções adicionais, *o*. Para obter informações sobre os fundamentos de opções, consulte a etapa 2.|
|||

Opcionalmente, especifique uma ou mais opções **WITH**. Algumas opções **WITH** básicas são descritas aqui. Para obter informações sobre todas as opções **WITH**, confira [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).

Opções **WITH** básicas do conjunto de backup:

- **{ COMPRESSION | NO_COMPRESSION }** : No [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e versões posteriores somente, especifica se [compressão de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md) é executada neste backup, substituindo o padrão de nível de servidor.
- **ENCRYPTION (ALGORITHM, SERVER CERTIFICATE | ASYMMETRIC KEY)** : No SQL Server 2014 ou em versões posteriores somente, especifique o algoritmo de criptografia a ser usado, e o certificado ou chave assimétrica usada para proteger a criptografia.
- **DESCRIPTION** **=** { **'** _text_ **'**  |  **@** _text\_variable_ }: Especifica o texto de forma livre que descreve o conjunto de backup. A cadeia de caracteres pode conter um máximo de 255 caracteres.
- **NAME = { *backup_set_name* |  **@** _backup\_set\_name\_var_ }** : Especifica o nome do conjunto de backup. Os nomes podem ter no máximo de 128 caracteres. Se NAME não estiver especificado, ele estará em branco.

Por padrão, `BACKUP` acrescenta o backup a um conjunto de mídias existente, preservando os conjuntos de backup existentes. Para especificar isso explicitamente, use a opção `NOINIT`. Para obter informações sobre o acréscimo a conjuntos de backup existentes, consulte [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).

Como alternativa, para formatar a mídia de backup, use a opção **FORMAT**:

 FORMAT [ **,** MEDIANAME **=** { *media_name* |  **@** _media\_name\_variable_ } ] [ **,** MEDIADESCRIPTION **=** { *text* |  **@** _text\_variable_ } ]

 Use a cláusula **FORMAT** quando estiver usando a mídia pela primeira vez ou quando quiser substituir todos os dados existentes. Opcionalmente, atribua à nova mídia um nome e uma descrição.

 > [!IMPORTANT]
 > Tenha muito cuidado ao usar a cláusula **FORMAT** da instrução `BACKUP`, pois isso destrói qualquer backup previamente armazenado na mídia de backup.

### <a name="examples"></a><a name="TsqlExample"></a> Exemplos

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
   dt1 DATETIME NOT NULL DEFAULT GETDATE()
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

#### <a name="a-back-up-to-a-disk-device"></a>a. Fazer backup em um dispositivo de disco

O exemplo a seguir faz backup de banco de dados completo `SQLTestDB` em um disco, usando `FORMAT` para criar um novo conjunto de mídia.

```sql
USE SQLTestDB;
GO
BACKUP DATABASE SQLTestDB
TO DISK = 'c:\tmp\SQLTestDB.bak'
   WITH FORMAT,
      MEDIANAME = 'SQLServerBackups',
      NAME = 'Full Backup of SQLTestDB';
GO
```

#### <a name="b-back-up-to-a-tape-device"></a>B. Fazer backup em um dispositivo de fita

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

#### <a name="c-back-up-to-a-logical-tape-device"></a>C. Fazer backup em um dispositivo de fita lógico

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

## <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o PowerShell

Use o cmdlet **Backup-SqlDatabase** . Para indicar explicitamente que este é um backup completo de banco de dados, especifique o parâmetro **-BackupAction** com seu valor padrão **Database**. Esse parâmetro é opcional para backups completos de banco de dados.

> [!NOTE]
> Esses exemplos exigem o módulo SqlServer. Para determinar se ele está instalado, execute `Get-Module -Name SqlServer`. Para instalar esse módulo, execute `Install-Module -Name SqlServer` em uma sessão de administrador do PowerShell.
>
> Para obter mais informações, consulte [SQL Server PowerShell Provider](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider).

> [!IMPORTANT]
> Se estiver abrindo uma janela do PowerShell no SQL Server Management Studio para se conectar a uma instalação do SQL Server, você poderá omitir a parte da credencial desse exemplo, pois sua credencial no SSMS é usada automaticamente para estabelecer a conexão entre o PowerShell e sua instância do SQL Server.

### <a name="examples"></a>Exemplos

#### <a name="a-full-backup-local"></a>a. Backup completo (local)

O exemplo a seguir cria um backup de banco de dados completo do banco de dados `<myDatabase>` para o local de backup padrão da instância de servidor `Computer\Instance`. Como opção, esse exemplo especifica **-BackupAction Database**.

Para obter a sintaxe completa e os exemplos adicionais, confira [Backup-SqlDatabase](https://docs.microsoft.com/powershell/module/sqlserver/backup-sqldatabase).

```powershell
$credential = Get-Credential

Backup-SqlDatabase -ServerInstance Computer[\Instance] -Database <myDatabase> -BackupAction Database -Credential $credential
```

#### <a name="b-full-backup-to-azure"></a>B. Backup completo no Azure

O exemplo a seguir cria um backup completo do banco de dados `<myDatabase>` na instância `<myServer>` no serviço de Armazenamento de Blobs do Azure. Uma política de acesso armazenado foi criada com direitos de leitura, gravação e listagem. A credencial do SQL Server, `https://<myStorageAccount>.blob.core.windows.net/<myContainer>`, foi criada usando uma Assinatura de Acesso Compartilhado associada à política de acesso armazenado. O comando do PowerShell usa o parâmetro **BackupFile** para especificar o local (URL) e o nome do arquivo de backup.

```powershell
$credential = Get-Credential
$container = 'https://<myStorageAccount>blob.core.windows.net/<myContainer>'
$fileName = '<myDatabase>.bak'
$server = '<myServer>'
$database = '<myDatabase>
$backupFile = $container + '/' + $fileName

Backup-SqlDatabase -ServerInstance $server -Database $database -BackupFile $backupFile -Credential $credential
```

## <a name="related-tasks"></a><a name="RelatedTasks"></a> Related tasks

- [Fazer backup de um banco de dados (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
- [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)
- [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)
- [Restaurar um backup de banco de dados no modelo de recuperação simples &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)
- [Restaurar um banco de dados até o ponto de falha no modelo de recuperação completa &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)
- [Restaurar um banco de dados em um novo local &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)
- [Usar o Assistente de Plano de Manutenção](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)

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
