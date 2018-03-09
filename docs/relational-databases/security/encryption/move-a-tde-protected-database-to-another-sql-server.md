---
title: Mover um banco de dados protegido por TDE para outro SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Transparent Data Encryption, moving
- TDE, moving a database
ms.assetid: fb420903-df54-4016-bab6-49e6dfbdedc7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: df6d9dfb912e4a425f44008a982b8c18fdc54f7c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="move-a-tde-protected-database-to-another-sql-server"></a>Mover um banco de dados protegido por TDE para outro SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como proteger um banco de dados usando a TDE (Transparent Data Encryption) e, em seguida, mover o banco de dados para outra instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. A TDE realiza a criptografia e a descriptografia de E/S em tempo real dos arquivos de dados e de log. A criptografia usa uma DEK (chave de criptografia do banco de dados), que é armazenada no registro de inicialização do banco de dados para disponibilidade durante a recuperação. A DEK é uma chave simétrica protegida por um certificado armazenado no banco de dados **mestre** do servidor ou uma chave assimétrica protegida por um módulo EKM.  
   
##  <a name="Restrictions"></a> Limitações e restrições  
  
-   Ao mover um banco de dados protegido por TDE, é necessário também mover o certificado ou a chave assimétrica que é usada para abrir a DEK. O certificado ou a chave assimétrica devem ser instalados no banco de dados **mestre** do servidor de destino, de forma que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] possa acessar os arquivos do banco de dados. Para obter mais informações, veja [TDE &#40;Transparent Data Encryption&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
-   Você deve reter cópias do arquivo de certificado e do arquivo de chave privada para poder recuperar o certificado. A senha da chave privada não precisa ser igual à senha da chave mestra do banco de dados.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] armazena os arquivos criados aqui em **C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA** por padrão. Os nomes e locais dos seus arquivos poderão ser diferentes.  
  
##  <a name="Permissions"></a> Permissões  
  
-   Requer a permissão **CONTROL DATABASE** no banco de dados **mestre** para criar a chave mestra de banco de dados.  
  
-   Requer a permissão **CREATE CERTIFICATE** no banco de dados **mestre** para criar o certificado que protege a DEK.  
  
-   Requer a permissão **CONTROL DATABASE** no banco de dados e a permissão **VIEW DEFINITION** na chave assimétrica ou no certificado usado para criptografar a chave de criptografia do banco de dados.  
  
##  <a name="SSMSProcedure"></a> Para criar um banco de dados protegido por criptografia de dados transparente  

Os procedimentos a seguir mostram a que você precisa criar um banco de dados protegido por TDE usando o SQL Server Management Studio e usando o Transact-SQL.
  
###  <a name="SSMSCreate"></a> Usando o SQL Server Management Studio  
  
1.  Crie uma chave mestra e um certificado de banco de dados no banco de dados **mestre** . Para obter mais informações, veja **Usando o Transact-SQL** abaixo.  
  
2.  Crie um backup do certificado do servidor no banco de dados **mestre** . Para obter mais informações, veja **Usando o Transact-SQL** abaixo.  
  
3.  No Pesquisador de Objetos, clique com o botão direito do mouse na pasta **Bancos de Dados** e selecione **Novo Banco de Dados**.  
  
4.  Na caixa de diálogo **Novo Banco de Dados** , na caixa **Nome do banco de dados** , digite o nome do novo banco de dados.  
  
5.  Na caixa de diálogo **Proprietário** , digite o nome do proprietário do novo banco de dados. Como alternativa, clique nas reticências **(…)** para abrir a caixa de diálogo **Selecionar Proprietário do Banco de Dados** . Para obter mais informações sobre a criação de um novo banco de dados, consulte [Create a Database](../../../relational-databases/databases/create-a-database.md).  
  
6.  No Pesquisador de Objetos, clique no sinal de mais para expandir a pasta **Bancos de Dados** .  
  
7.  Clique com o botão direito do mouse no banco de dados que você criou, aponte para **Tarefas**e selecione **Gerenciar Criptografia de Banco de Dados**.  
  
     As opções a seguir estão disponíveis na caixa de diálogo **Gerenciar Criptografia de Banco de Dados** .  
  
     **Algoritmo de Criptografia**  
     Exibe ou define o algoritmo para uso na criptografia de banco de dados. **AES128** é o algoritmo padrão. Este campo não pode ficar em branco. Para obter mais informações sobre algoritmos de criptografia, consulte [Choose an Encryption Algorithm](../../../relational-databases/security/encryption/choose-an-encryption-algorithm.md).  
  
     **Usar certificado de servidor**  
     Define a criptografia a ser protegida por um certificado. Selecione uma opção da lista. Se você não tiver a permissão **VIEW DEFINITION** nos certificados do servidor, essa lista estará vazia. Se um método de certificado de criptografia for selecionado, esse valor não poderá ficar em branco. Para obter mais informações sobre certificados, consulte [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
     **Usar chave assimétrica do servidor**  
     Define a criptografia a ser protegida por uma chave assimétrica. Somente as chaves assimétricas disponíveis são exibidas. Somente uma chave assimétrica protegida por um módulo EKM pode criptografar um banco de dados que usa a TDE.  
  
     **Definir criptografia de banco de dados como ativa**  
     Altera o banco de dados para ativar (marcado) ou desativar (desmarcado) a TDE.  
  
8.  Quando terminar, clique em **OK**.  
  
###  <a name="TsqlCreate"></a> Usando o Transact-SQL  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql  
    -- Create a database master key and a certificate in the master database.  
    USE master ;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1';  
    GO  
    CREATE CERTIFICATE TestSQLServerCert   
    WITH SUBJECT = 'Certificate to protect TDE key'  
    GO  
    -- Create a backup of the server certificate in the master database.  
    -- The following code stores the backup of the certificate and the private key file in the default data location for this instance of SQL Server   
    -- (C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA).  
  
    BACKUP CERTIFICATE TestSQLServerCert   
    TO FILE = 'TestSQLServerCert'  
    WITH PRIVATE KEY   
    (  
        FILE = 'SQLPrivateKeyFile',  
        ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1'  
    );  
    GO  
    -- Create a database to be protected by TDE.  
    CREATE DATABASE CustRecords ;  
    GO  
    -- Switch to the new database.  
    -- Create a database encryption key, that is protected by the server certificate in the master database.   
    -- Alter the new database to encrypt the database using TDE.  
    USE CustRecords;  
    GO  
    CREATE DATABASE ENCRYPTION KEY  
    WITH ALGORITHM = AES_128  
    ENCRYPTION BY SERVER CERTIFICATE TestSQLServerCert;  
    GO  
    ALTER DATABASE CustRecords  
    SET ENCRYPTION ON;  
    GO  
    ```  
  
 Para obter mais informações, consulte:  
  
-   [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-certificate-transact-sql.md)  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
-   [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-encryption-key-transact-sql.md)  
  
-   [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)  
  
##  <a name="TsqlProcedure"></a> Para mover um banco de dados protegido por Transparent Data Encryption 

Os procedimentos a seguir mostram a que você precisa mover um banco de dados protegido por TDE usando o SQL Server Management Studio e usando o Transact-SQL.
  
###  <a name="SSMSMove"></a> Usando o SQL Server Management Studio  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse no banco de dados que você criptografou acima, aponte para **Tarefas** e selecione **Desanexar...**.  
  
     As opções a seguir estão disponíveis na caixa de diálogo **Desanexar Banco de Dados** .  
  
     **Bancos de dados a serem desanexados**  
     Lista os bancos de dados a serem desanexados  
  
     **Database Name**  
     Exibe o nome do banco de dados a ser desanexado.  
  
     **Cancelar Conexões**  
     Cancelar conexões com o banco de dados especificado.  
  
    > [!NOTE]  
    >  Você não pode desanexar um banco de dados com conexões ativas.  
  
     **Atualização de Estatísticas**  
     Por padrão, a operação desanexar retém qualquer estatística de otimização desatualizada ao desanexar o banco de dados; para atualizar as estatísticas de otimização existentes, clique nesta caixa de seleção.  
  
     **Manter Catálogos de Texto Completo**  
     Por padrão, a operação desanexar mantém qualquer catálogo de texto completo que esteja associado ao banco de dados. Para removê-los, desmarque a caixa de seleção **Manter Catálogos de Texto Completo** . Essa opção é exibida apenas quando você está atualizando um banco de dados do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
     **Status**  
     Exibe um dos seguintes estados: **Pronto** ou **Não pronto**.  
  
     **Mensagem**  
     A coluna **Mensagem** pode exibir informações sobre o banco de dados, da seguinte forma:  
  
    -   Quando um banco de dados estiver envolvido com replicação, o **Status** será **Não pronto** e a coluna **Mensagem** exibirá **Banco de Dados replicado**.  
  
    -   Quando um banco de dados tiver uma ou mais conexões ativas, o **Status** será **Não está pronto** e a coluna **Mensagem** exibirá *<number_of_active_connections>***Conexão(ões) ativa(s)** — por exemplo: **1 conexão ativa**. Antes de desanexar o banco de dados, você deverá cancelar qualquer conexão ativa selecionando **Cancelar Conexões**.  
  
     Para obter mais informações sobre a mensagem, clique o texto com hiperlink para abrir o Monitor de atividades.  
  
2.  Clique em **OK**.  
  
3.  Usando o Windows Explorer, mova ou copie os arquivos de banco de dados do servidor de origem para o mesmo local no servidor de destino.  
  
4.  Usando o Windows Explorer, mova ou copie o backup do certificado do servidor e o arquivo de chave privada do servidor de origem para o mesmo local no servidor de destino.  
  
5.  Crie uma chave mestra de banco de dados na instância de destino do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, veja **Usando o Transact-SQL** abaixo.  
  
6.  Recrie o certificado do servidor usando o arquivo de backup de certificado do servidor original. Para obter mais informações, veja **Usando o Transact-SQL** abaixo.  
  
7.  No Pesquisador de Objetos, no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse na pasta **Bancos de Dados** e selecione **Anexar...**.  
  
8.  Na caixa de diálogo **Anexar Bancos de Dados** , em **Bancos de dados a serem anexados**, clique em **Adicionar**.  
  
9. Na caixa de diálogo **Localizar Arquivos de Banco de Dados –***server_name* , selecione o arquivo de banco de dados a ser anexado ao novo servidor e clique em **OK**.  
  
     As opções a seguir estão disponíveis na caixa de diálogo **Anexar Bancos de Dados** .  
  
     **Bancos de dados a serem anexados**  
     Exibe informações sobre os bancos de dados selecionados.  
  
     \<no column header>  
     Exibe um ícone que indica o status da operação de anexação. Os possíveis ícones são descritos em **Status** , abaixo).  
  
     **Local do Arquivo MDF**  
     Exibe o caminho e o nome de arquivo do arquivo MDF selecionado.  
  
     **Database Name**  
     Exibe o nome do banco de dados.  
  
     **Anexar como**  
     Opcionalmente, especifique um nome diferente para o banco de dados anexar como.  
  
     **Proprietário**  
     Fornece uma lista suspensa de possíveis proprietários de banco de dados dos quais você pode selecionar um proprietário diferente opcionalmente.  
  
     **Status**  
     Exibe o status do banco de dados de acordo com a seguinte tabela.  
  
    |Ícone|Texto de status|Descrição|  
    |----------|-----------------|-----------------|  
    |(No icon)|(Nenhum texto)|A operação de anexação não foi iniciada ou pode estar pendente para esse objeto. Esse é o padrão quando a caixa de diálogo é aberta.|  
    |Triângulo verde apontando para a direita|Em andamento|A operação de anexação foi iniciada mas não está completa.|  
    |Sinal de verificação verde|Success|O objeto foi anexado com êxito.|  
    |Círculo vermelho contendo uma cruz branca|Erro|A operação de anexação encontrou um erro e não foi concluída com êxito.|  
    |Círculo que contém dois quadrantes pretos (à esquerda e à direita) e dois quadrantes brancos (em cima e em baixo)|Stopped (parado)|A operação de anexação não foi completada com êxito porque o usuário interrompeu a operação.|  
    |Círculo que contém uma seta curvada que aponta para o sentido anti-horário|Revertida|A operação de anexação teve êxito, mas foi revertida devido a um erro ao se anexar outro objeto.|  
  
     **Mensagem**  
     Exibe uma mensagem em branco ou um hiperlink "Arquivo não encontrado"  
  
     **Adicionar**  
     Encontrar os arquivos de banco de dados principais necessários. Quando o usuário selecionar um arquivo .mdf , os respectivos campos são automaticamente preenchidos com informações aplicáveis da grade **Bancos de dados a serem anexados** .  
  
     **Remover**  
     Remove o arquivo selecionado da grade **Bancos de dados a serem anexados** .  
  
     **"** *<database_name>* **" detalhes do banco de dados**  
     Exibe os nomes dos arquivos a serem anexados. Para verificar ou alterar o nome do caminho de um arquivo, clique no botão **Procurar** (**…**).  
  
    > [!NOTE]  
    >  Se um arquivo não existir, a coluna **Mensagem** exibe "Não encontrado." Se um arquivo de log não for encontrado, ele existe em outro diretório ou foi excluído. Você precisa atualizar o caminho do arquivo na grade **detalhes do banco de dados** para indicar o local correto ou remover o arquivo de log da grade. Se um arquivo de dados .ndf não for encontrado, você precisará atualizar seu caminho na grade a fim de indicar o local correto.  
  
     **Nome do arquivo original**  
     Exibe o nome do arquivo anexado que pertence ao banco de dados.  
  
     **Tipo de arquivo**  
     Indica o tipo de arquivo, **Dados** ou **Log**.  
  
     **Caminho do arquivo atual**  
     Exibe o caminho para o arquivo de banco de dados selecionado. O caminho pode ser editado manualmente.  
  
     **Mensagem**  
     Exibe uma mensagem em branco ou um hiperlink “**Arquivo não encontrado**”.  
  
###  <a name="TsqlMove"></a> Usando o Transact-SQL  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql  
    -- Detach the TDE protected database from the source server.   
    USE master ;  
    GO  
    EXEC master.dbo.sp_detach_db @dbname = N'CustRecords';  
    GO  
    -- Move or copy the database files from the source server to the same location on the destination server.   
    -- Move or copy the backup of the server certificate and the private key file from the source server to the same location on the destination server.   
    -- Create a database master key on the destination instance of SQL Server.   
    USE master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1';  
    GO  
    -- Recreate the server certificate by using the original server certificate backup file.   
    -- The password must be the same as the password that was used when the backup was created.  
  
    CREATE CERTIFICATE TestSQLServerCert   
    FROM FILE = 'TestSQLServerCert'  
    WITH PRIVATE KEY   
    (  
        FILE = 'SQLPrivateKeyFile',  
        DECRYPTION BY PASSWORD = '*rt@40(FL&dasl1'  
    );  
    GO  
    -- Attach the database that is being moved.   
    -- The path of the database files must be the location where you have stored the database files.  
    CREATE DATABASE [CustRecords] ON   
    ( FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\CustRecords.mdf' ),  
    ( FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\CustRecords_log.LDF' )  
    FOR ATTACH ;  
    GO  
    ```  
  
 Para obter mais informações, consulte:  
  
-   [sp_detach_db &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)  
  
-   [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
## <a name="see-also"></a>Consulte também  
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [Transparent Data Encryption com o Banco de Dados SQL do Azure](../../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md)  
  
  
