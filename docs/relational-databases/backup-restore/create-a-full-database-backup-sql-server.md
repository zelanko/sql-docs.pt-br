---
title: Criar um backup completo do banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
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
ms.openlocfilehash: f82b79c8f5484a10e59827b7821038d93142e664
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51677627"
---
# <a name="create-a-full-database-backup-sql-server"></a>Criar um backup completo de banco de dados (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > Para o SQL Server 2014, acesse [Criar um backup completo de banco de dados (SQL Server)](create-a-full-database-backup-sql-server.md).

  Este tópico descreve como criar um backup de banco de dados completo no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou PowerShell.  
  
>  Para obter informações sobre o backup do SQL Server no serviço de armazenamento de Blobs do Azure, veja [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) e [Backup do SQL Server para URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).  
  
##  <a name="BeforeYouBegin"></a> Antes de começar. 
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   A instrução BACKUP não é permitida em uma transação explícita ou implícita.  
  
-   Os backups criados por uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem ser restaurados em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Para ter uma visão geral e aprofundar-se nos conceitos e tarefas de backup, consulte [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md) antes de prosseguir.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   À medida que um banco de dados aumenta de tamanho, os backups completos do banco de dados levam mais tempo para serem concluídos e exigem mais espaço de armazenamento. Para um banco de dados grande, considere complementar um backup de banco de dados completo com uma série de [backups de bancos de dados diferenciais](../../relational-databases/backup-restore/differential-backups-sql-server.md). Para saber mais, confira [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).  
  
-   Estime o tamanho de um backup de banco de dados completo usando o procedimento armazenado do sistema [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) .  
  
-   Por padrão, toda operação de backup bem-sucedida acrescenta uma entrada ao log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao log de eventos do sistema. Se você fizer backup com frequência, essas mensagens de êxito acumularão rapidamente, resultando em logs de erro grandes. Isso pode dificultar a localização de outras mensagens. Em tais situações, você pode suprimir essas entradas de log de backup usando o sinalizador de rastreamento 3226, caso nenhum dos seus scripts dependa dessas entradas. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
###  <a name="Security"></a> Segurança  
 TRUSTWORTHY é definido como OFF em um backup de banco de dados. Para obter informações sobre como definir TRUSTWORTHY como ON, veja [Opções do ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , as opções **PASSWORD** e **MEDIAPASSWORD** foram descontinuadas para a criação de backups. Você ainda poderá restaurar os backups criados com senhas.  
  
####  <a name="Permissions"></a> Permissões  
 As permissões BACKUP DATABASE e BACKUP LOG usam como padrão os membros da função de servidor fixa **sysadmin** e as funções de banco de dados fixas **db_owner** e **db_backupoperator** .  
  
 Os problemas de propriedade e permissão no arquivo físico do dispositivo de backup podem interferir em uma operação de backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser capaz de ler e gravar no dispositivo; a conta sob a qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa **deve** ter permissões de gravação. No entanto, [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), que adiciona uma entrada para um dispositivo de backup nas tabelas do sistema, não verifica permissões de acesso a arquivos. Esses problemas no arquivo físico do dispositivo de backup podem não aparecer até que o recurso físico seja acessado quando o backup ou restauração é tentado.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
>  Ao especificar uma tarefa de backup usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], é possível gerar o script [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) correspondente, clicando no botão **Script** e selecionando um destino para o script.  
  
### <a name="back-up-a-database"></a>Fazer o backup de um banco de dados  
  
1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], em **Pesquisador de Objetos**, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados**e selecione um banco de dados de usuário ou expanda **Bancos de Dados de Sistema** e selecione um banco de dados de sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**e clique em **Backup**. Será exibida a caixa de diálogo **Backup de Banco de Dados** .  

  #### <a name="general-page"></a>**Página Geral**
  
4.  Na lista suspensa **Banco de Dados** , verifique o nome do banco de dados. Opcionalmente, você pode selecionar um banco de dados diferente na lista.  
  
5.  A caixa de texto **Modelo de recuperação** serve apenas para referência.  Você pode executar um backup de banco de dados para qualquer modelo de recuperação (**FULL**, **BULK_LOGGED**ou **SIMPLE**).  
  
6.  Na lista suspensa **Tipo de backup** , selecione **Completo**.  
  
     Observe que depois de criar um backup de banco de dados completo, é possível criar um backup de banco de dados diferencial. Para obter mais informações, consulte [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md).  
  
7.  Opcionalmente, você pode marcar a caixa de seleção **Backup somente cópia** para criar um backup somente cópia. Um *backup somente cópia* é um backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não depende da sequência de backups convencionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Backups somente cópia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  Um backup somente cópia não está disponível para o tipo de backup **Diferencial**.  

8.  Em **Componente de backup**, selecione o botão de opção **Banco de dados** .  
  
9. Na seção **Destino** , use a lista suspensa **Fazer backup em** para selecionar o destino do backup. Clique em **Adicionar** para adicionar outros objetos e/ou destinos de backup.
  
     Para remover um destino de backup, selecione-o e clique em **Remover**. Para exibir o conteúdo de um destino de backup existente, selecione-o e clique em **Conteúdo**.  

  #### <a name="media-options-page"></a>**Página Opções de Mídia**  
10. Para exibir ou selecionar as opções de mídia, clique em **Opções de Mídia** no painel **Selecionar uma página** .   
    
11. Selecione uma opção **Substituir Mídia** , com um clique em uma das opções a seguir: 

    > [!IMPORTANT]  
    >  A opção **Substituir mídia** será desabilitada se você selecionou **URL** como destino de backup na página **Geral**. Para saber mais, confira [Fazer backup do banco de dados &#40;página Opções de Mídia&#41;](../../relational-databases/backup-restore/back-up-database-media-options-page.md)  


  -   **Fazer backup no conjunto de mídias existente**  
  
      > [!IMPORTANT]  
      >  Se você planeja usar criptografia, não selecione essa opção. Se você selecionar esta opção, as opções de criptografia na página **Opções de Backup** serão desabilitadas. A criptografia não tem suporte ao anexar ao conjunto de backup existente.  
  
         Para essa opção, clique em **Anexar ao conjunto de backup existente** ou **Substituir todos os conjuntos de backup existentes**. Para obter mais informações, veja [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
         Opcionalmente, selecione **Verificar nome do conjunto de mídias e validade do conjunto de backup** para que a operação de backup verifique a data e a hora em que o conjunto de mídias e de backup expiram.  
  
         Como opção, digite um nome na caixa de texto **Nome do conjunto de mídias** . Se nenhum nome for especificado, um conjunto de mídias com um nome em branco será criado. Se você especificar um nome de conjunto de mídias, a mídia (fita ou disco) é verificada para ver se o nome real corresponde ao nome digitado.  
  
-   **Fazer backup em um novo conjunto de mídias e apagar todos os conjuntos de backup existentes**  
  
    Para essa opção, digite um nome na caixa de texto **Nome do novo conjunto de mídias** e, opcionalmente, descreva o conjunto de mídias na caixa de texto **Descrição do novo conjunto de mídias** .  
  
14. Na seção **Confiabilidade** , como opção, marque:  
  
    -   **Verificar backup quando concluído**  
  
    -   **Executar soma de verificação antes de gravar na mídia**.  Para obter informações sobre somas de verificação, veja [Erros de mídia possíveis durante backup e restauração &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
    
    -   **Continuar se houver erro**. 

15. A seção **Log de transações** estará inativa exceto se o backup estiver sendo feito em um log de transações (como especificado na seção **Tipo de backup** da página **Geral** ).  
      
16. Na seção **Unidade de fita** , a opção **Descarregar a fita após o backup** estará ativa se você estiver fazendo backup em uma unidade de fita (como especificado na seção **Destino** da página **Geral** ). Clicar nessa opção ativa a opção **Rebobinar a fita antes de descarregar** .   

  #### <a name="backup-options-page"></a>**Página Opções de Backup**  

17. Para exibir ou selecionar as opções de backup, clique em **Opções de Backup** no painel **Selecionar uma página** .  
  
18. Na caixa de texto **Nome** , aceite o nome do conjunto de backup padrão ou insira um nome diferente para o conjunto de backup.  
  
19. Opcionalmente, na caixa de texto **Descrição** , você pode inserir uma descrição do conjunto de backup.  
  
20. Especifique quando o conjunto de backup irá expirar e pode ser substituído sem ignorar explicitamente a verificação dos dados de expiração:  
  
    -   Para que o conjunto de backup expire depois de um número específico de dias, clique em **Depois** (a opção padrão) e digite quantos dias depois da criação do conjunto ele deve expirar. Esse valor pode ser de 0 a 99999 dias; 0 dia significa que o conjunto de backup nunca vai expirar.  
  
         O valor padrão é definido na opção **Retenção de mídia de backup padrão (em dias)** da caixa de diálogo **Propriedades do Servidor** (página Configurações do Banco de Dados). Para acessar, clique com o botão direito do mouse no nome do servidor em Pesquisador de Objetos e selecione propriedades. Depois, selecione a página **Configurações de Banco de Dados** .  
  
    -   Para que o conjunto de backup expire em uma data específica, clique no campo **Em**e digite a data de expiração do conjunto.  
  
         Para obter mais informações sobre datas de validade de backup, consulte [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
21. Na seção **Compactação** , use a lista suspensa **Definir compactação de backup** para selecionar o nível de compactação desejado.  [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e posteriores dão suporte para [compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md). Por padrão, a compactação de um backup depende do valor da opção de configuração de servidor **padrão de compactação de backup**. Porém, independentemente do padrão atual do nível do servidor, é possível compactar um backup, marcando a opção **Compactar backup**e evitar a compactação marcando **Não compactar o backup**.  
  
     Para obter mais informações sobre configurações de compactação de backup, consulte [Exibir ou configurar a Opção de Configuração de Servidor backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
22. Na seção **criptografia** , use a caixa de seleção **Criptografar backup** para decidir se deverá ser usada criptografia para o backup. Use a lista suspensa **Algoritmo** para selecionar um algoritmo de criptografia.  Use a lista suspensa **Certificado ou Chave Assimétrica** para selecionar um Certificado ou Chave Assimétrica existente. A criptografia tem suporte no SQL Server 2014 ou posterior. Para obter mais detalhes sobre as opções de criptografia, consulte [Fazer backup do banco de dados &#40;página Opções de Backup&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md).  
  
  
É possível usar o [Assistente de Plano de Manutenção](../maintenance-plans/use-the-maintenance-plan-wizard.md) para criar backups de bancos de dados. 

### <a name="examples"></a>Exemplos  
#### <a name="a--full-back-up-to-disk-to-default-location"></a>**A.  Backup completo no disco no local padrão**
Neste exemplo, será feito backup do banco de dados `Sales` em disco no local de backup padrão.  Nunca foi feito backup do `Sales` .
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do Mecanismo de Banco de Dados do SQL Server e expanda-a.

2.  Expanda **Banco de Dados**, clique com o botão direito do mouse em `Sales`, aponte para **Tarefas**e clique em **Fazer Backup...**.

3.  Clique em **OK**.

#### <a name="b--full-back-up-to-disk-to-non-default-location"></a>**B.  Backup completo no disco em local não padrão**
Neste exemplo, será feito backup do banco de dados `Sales` em disco em `E:\MSSQL\BAK`.  Já foram feitos backups anteriores do `Sales` .
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do Mecanismo de Banco de Dados do SQL Server e expanda-a.

2.  Expanda **Banco de Dados**, clique com o botão direito do mouse em `Sales`, aponte para **Tarefas**e clique em **Fazer Backup...**.

3.  Na página **Geral** , na seção **Destino** , selecione a opção **Disco** na lista suspensa **Fazer backup em:** .

4.  Clique em **Remover** até que todos os arquivos de backup existentes sejam removidos.

5.  Clique em **Adicionar** e a caixa de diálogo **Selecionar Destino do Backup** será aberta.

6.  Insira `E:\MSSQL\BAK\Sales_20160801.bak` na caixa de texto **Nome de arquivo** .

7.  Clique em **OK**.

8.  Clique em **OK**.

#### <a name="c--create-an-encrypted-backup"></a>**C.  Criar um backup criptografado**
Neste exemplo, será feito backup do banco de dados `Sales` com criptografia no local de backup padrão.  Uma  [**chave mestra do banco de dados**](../../relational-databases/security/encryption/create-a-database-master-key.md) já foi criada.  Um  [**certificado**](../../t-sql/statements/create-certificate-transact-sql.md) chamado `MyCertificate`já foi criado. Um exemplo de T-SQL de como criar uma **chave mestra do banco de dados** e um **certificado** pode ser visto em [Criar um backup criptografado](../../relational-databases/backup-restore/create-an-encrypted-backup.md).  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do Mecanismo de Banco de Dados do SQL Server e expanda-a.

2.  Expanda **Banco de Dados**, clique com o botão direito do mouse em `Sales`, aponte para **Tarefas**e clique em **Fazer Backup...**.

3.  Na página **Opções de Mídia** da seção **Substituir mídia** , selecione **Fazer backup em um novo conjunto de mídias e apagar todos os conjuntos de backup existentes**.

4.  Na página **Opções de Backup** da seção **Criptografia** , marque a caixa de seleção **Criptografar backup** .

5.  Na lista suspensa **Algoritmo** , selecione **AES 256**.

6.  Na lista suspensa **Certificado ou Chave Assimétrica** , selecione `MyCertificate`.

7.  Clique em **OK**.

#### <a name="d--back-up-to-the-azure-blob-storage-service"></a>**D.  Fazer backup no serviço de armazenamento de Blobs do Azure**
#### <a name="common-steps"></a>**Etapas comuns**  
Os três exemplos abaixo executam um backup completo do banco de dados do `Sales` no serviço de Armazenamento de Blobs do Microsoft Azure.  O nome da Conta de armazenamento é `mystorageaccount`.  O contêiner é chamado `myfirstcontainer`.  Para resumir, as quatro primeiras etapas são listadas aqui uma vez e todos os exemplos serão iniciados na **Etapa 5**.
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do Mecanismo de Banco de Dados do SQL Server e expanda-a.

2.  Expanda **Banco de Dados**, clique com o botão direito do mouse em `Sales`, aponte para **Tarefas**e clique em **Fazer Backup...**.

3.  Na página **Geral** , na seção **Destino** , selecione a opção **URL** na lista suspensa **Fazer backup em:** .

4.  Clique em **Adicionar** e a caixa de diálogo **Selecionar Destino do Backup** será aberta.

    **D1.  Já existe um backup distribuído para URL e uma credencial do SQL Server**  
Uma política de acesso armazenado foi criada com direitos de leitura, gravação e listagem.  A credencial do SQL Server, `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`, foi criada usando uma Assinatura de Acesso Compartilhado associada à política de acesso armazenado.  
*
    5.  Selecione `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` do **contêiner de armazenamento do Azure:** caixa de texto

    6.  Na caixa de texto **Arquivo de Backup:** , digite `Sales_stripe1of2_20160601.bak`.

    7.  Clique em **OK**.

    8.  Repita as etapas de **4** e **5**.

    9.  Na caixa de texto **Arquivo de Backup:** , digite `Sales_stripe2of2_20160601.bak`.

    10.  Clique em **OK**.

    11.   Clique em **OK**.

    **D2.  Existe uma assinatura de acesso compartilhado e não existe uma credencial do SQL Server**
  5.    Digite `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` na caixa de texto **Contêiner de armazenamento do Azure:**
  
  6.    Insira a assinatura de acesso compartilhado na caixa de texto **Política de Acesso Compartilhado:** .
  
  7.    Clique em **OK**.
  
  8.    Clique em **OK**.

    **D3.  Não há uma assinatura de acesso compartilhado**
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
  
     TO *backup_device* [ **,**...*n* ]  
  
     [ WITH *com_opções* [ **,**...*o* ] ] ;  
  
    |Opção|Descrição|  
    |------------|-----------------|  
    |*database*|É o banco de dados do qual fazer backup.|  
    |*backup_device* [ **,**...*n* ]|Especifica uma lista de 1 a 64 dispositivos de backup a serem usados para a operação de backup. Você pode especificar um dispositivo de backup físico ou pode especificar um dispositivo de backup lógico correspondente, se já definido. Para especificar um dispositivo de backup físico, use a opção DISK ou TAPE:<br /><br /> { DISK &#124; TAPE } **=**_physical\_backup\_device\_name_<br /><br /> Para obter mais informações, consulte [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).|  
    |WITH *with_options* [ **,**...*o* ]|Opcionalmente, especifica uma ou mais opções adicionais, *o*. Para obter informações sobre os fundamentos de opções, consulte a etapa 2.|  
  
2.  Opcionalmente, especifique uma ou mais opções WITH. Algumas opções WITH básicas são descritas aqui. Para obter informações sobre todas as opções WITH, consulte [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
    -   Opções WITH do conjunto de backup básico:  
  
         { COMPRESSION | NO_COMPRESSION }  
         No [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e versões posteriores somente, especifica se [compressão de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md) é executada neste backup, substituindo o padrão de nível de servidor.  
  
         ENCRYPTION (ALGORITHM, SERVER CERTIFICATE |ASYMMETRIC KEY)  
         No SQL Server 2014 ou em versões posteriores somente, especifique o algoritmo de criptografia a ser usado, e o certificado ou chave assimétrica usada para proteger a criptografia.  
  
         DESCRIPTION **=** { **'**_text_**'** | **@**_text\_variable_ }  
         Especifica o texto de forma livre que descreve o conjunto de backup. A cadeia de caracteres pode conter um máximo de 255 caracteres.  
  
         NAME **=** { *backup_set_name* | **@**_backup\_set\_name\_var_ }  
         Especifica o nome do conjunto de backup. Os nomes podem ter no máximo de 128 caracteres. Se NAME não estiver especificado, ele estará em branco.  
  
    -   Opções WITH do conjunto de backup básico:  
  
         Por padrão, BACKUP anexa o backup a um conjunto de mídias existente, preservando conjuntos de backup existentes. Para especificar isso explicitamente, use a opção NOINIT. Para obter informações sobre o acréscimo a conjuntos de backup existentes, consulte [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
         Alternativamente, para formatar a mídia de backup, use a opção FORMAT:  
  
         FORMAT [ **,** MEDIANAME**=** { *media_name* | **@**_media\_name\_variable_ } ] [ **,** MEDIADESCRIPTION **=** { *text* | **@**_text\_variable_ } ]  
         Use a cláusula FORMAT quando estiver usando a mídia pela primeira vez ou quando quiser sobrescrever todos os dados existentes Opcionalmente, atribua à nova mídia um nome e uma descrição.  
  
        > [!IMPORTANT]  
        >  Tenha muito cuidado ao usar a cláusula FORMAT ou a instrução BACKUP, pois isso destrói qualquer backup previamente armazenado na mídia de backup.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
  
#### <a name="a-back-up-to-a-disk-device"></a>**A. Fazer backup em um dispositivo de disco**  
 O exemplo a seguir faz backup de banco de dados completo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] em um disco, usando `FORMAT` para criar um novo conjunto de mídia.  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
   WITH FORMAT,  
      MEDIANAME = 'Z_SQLServerBackups',  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="b-back-up-to-a-tape-device"></a>**B. Fazer backup em um dispositivo de fita**  
 O exemplo a seguir faz backup do banco de dados completo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] em fita, anexando o backup aos backups anteriores.  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO TAPE = '\\.\Tape0'  
   WITH NOINIT,  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="c-back-up-to-a-logical-tape-device"></a>**C. Fazer backup em um dispositivo de fita lógico**  
 O exemplo a seguir cria um dispositivo de backup lógico para uma unidade de fita. O exemplo faz backup completo do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] nesse dispositivo.  
  
```sql  
-- Create a logical backup device,   
-- AdventureWorks2012_Bak_Tape, for tape device \\.\tape0.  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'AdventureWorks2012_Bak_Tape', '\\.\tape0'; USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO AdventureWorks2012_Bak_Tape  
   WITH FORMAT,  
      MEDIANAME = 'AdventureWorks2012_Bak_Tape',  
      MEDIADESCRIPTION = '\\.\tape0',   
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
Use o cmdlet **Backup-SqlDatabase** . Para indicar explicitamente que este é um backup completo de banco de dados, especifique o parâmetro **-BackupAction**  com seu valor padrão **Database**. Esse parâmetro é opcional para backups completos de banco de dados.  

### <a name="examples"></a>Exemplos
#### <a name="a--full-local-backup"></a>**A.  Backup completo local**  
O exemplo a seguir cria um backup de banco de dados completo do banco de dados `MyDB` para o local de backup padrão da instância de servidor `Computer\Instance`. Como opção, esse exemplo especifica **-BackupAction Database**.  
```powershell 
Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Database  
```
 
#### <a name="b--full-backup-to-microsoft-azure"></a>**B.  Backup completo para o Microsoft Azure**  
O exemplo a seguir cria um backup completo do banco de dados `Sales` na instância `MyServer` para o serviço de Armazenamento de Blobs do Microsoft Azure.  Uma política de acesso armazenado foi criada com direitos de leitura, gravação e listagem.  A credencial do SQL Server, `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`, foi criada usando uma Assinatura de Acesso Compartilhado associada à política de acesso armazenado.  O comando do PowerShell usa o parâmetro **BackupFile** para especificar o local (URL) e o nome do arquivo de backup.

```powershell  
import-module sqlps;
$container = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer';
$FileName = 'Sales.bak';
$database = 'Sales';
$BackupFile = $container + '/' + $FileName ;
  
Backup-SqlDatabase -ServerInstance "MyServer" –Database $database -BackupFile $BackupFile;
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
**[Solução de problemas de operações de backup e restauração do SQL Server](https://support.microsoft.com/kb/224071)**          
[Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Fazer backup do banco de dados &#40;página Geral&#41;](../../relational-databases/backup-restore/back-up-database-general-page.md)   
 [Fazer backup do banco de dados &#40;página Opções de Backup&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)   
 [Backups diferenciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [Backups de bancos de dados completos &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)  
  
  
