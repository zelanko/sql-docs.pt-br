---
title: 'Lição 6: Migrar um banco de dados de uma fonte de máquina local a uma máquina de destino no Windows Azure | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: d9134ade-7b03-4c5c-8ed3-3bc369a61691
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9a75375ae8636cd3c8861030131ce08c63832460
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52404264"
---
# <a name="lesson-6-migrate-a-database-from-a-source-machine-on-premises-to-a-destination-machine-in-windows-azure"></a>Lição 6: Migrar um banco de dados de um computador de origem local para um computador de destino no Microsoft Azure
  Esta lição supõe que você já tem outro SQL Server, que pode residir em outro computador local ou em uma máquina virtual no Windows Azure. Para obter informações sobre como criar uma máquina virtual SQL Server no Windows Azure, consulte [Provisionando uma máquina de Virtual do SQL Server no Windows Azure](http://www.windowsazure.com/manage/windows/common-tasks/install-sql-server/). Após o provisionamento de uma máquina virtual do SQL Server no Windows Azure, verifique se é possível conectar-se a uma instância do SQL Server nessa máquina virtual por meio do SQL Server Management Studio em outro computador.  
  
 Esta lição supõe também que você já concluiu as seguintes etapas:  
  
-   Você tem uma conta de Armazenamento do Windows Azure.  
  
-   Você criou um contêiner na sua conta de Armazenamento do Windows Azure.  
  
-   Você criou uma política em um contêiner com direitos de leitura, gravação e lista. Você também gerou uma chave de SAS.  
  
-   Você criou uma credencial do SQL Server no computador de origem.  
  
-   Você já criou uma máquina virtual do SQL Server de destino no Windows Azure. É recomendável que você a crie selecionando uma imagem da plataforma que inclua o SQL Server 2014.  
  
 Para migrar uma banco de dados do SQL Server local para outra máquina virtual no Windows Azure, siga estas etapas:  
  
1.  No computador de origem (que é um computador local neste tutorial), abra uma janela de consulta no SQL Server Management Studio. Desanexe seu banco de dados para movê-lo para outro computador executando estas instruções:  
  
    ```  
    -- Detach the database in the source machine   
    USE master  
    EXEC sp_detach_db 'TestDB1', 'true';  
    ```  
  
2.  Se você precisar transferir um banco de dados para um computador de destino, primeiro você deverá prepará-lo. Para preparar seu computador de destino, primeiro é necessário criar uma credencial do SQL Server no computador de destino. Se ele for um banco de dados criptografado, você precisará importar também o certificado do computador de origem para o computador de destino.  
  
    1.  Para criar uma credencial do SQL Server no computador de destino, siga estas etapas:  
  
        1.  Conecte-se ao computador de destino por meio do SQL Server Management Studio no computador de origem.  Ou, inicie o SQL Server Management Studio no computador de destino diretamente.  
  
        2.  Na barra de ferramentas padrão, clique em **nova consulta**.  
  
        3.  Copie e cole o exemplo a seguir na janela de consulta, e modifique conforme necessário. A instrução a seguir cria uma credencial do SQL Server para armazenar o certificado de acesso compartilhado do contêiner de armazenamento.  
  
            ```tsql  
  
            USE master   
            GO   
            CREATE CREDENTIAL [http://teststorageaccnt.blob.core.windows.net/testcontainer]   
            WITH IDENTITY='SHARED ACCESS SIGNATURE',   
            SECRET = 'your SAS key'   
            GO  
  
            ```  
  
        4.  Para ver todas as credenciais disponíveis, você pode executar a instrução a seguir na janela de consulta:  
  
            ```tsql  
            SELECT * from sys.credentials   
            ```  
  
        5.  Quando conectado a um servidor de destino, abra a janela de consulta e execute:  
  
            ```tsql  
  
            -- Create a master key and a server certificate   
            USE master   
            GO   
            CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MySQLKey01'; -- You may use a different password.   
            GO   
            CREATE CERTIFICATE MySQLCert   
            FROM FILE = 'C:\certs\MySQLCert.CER'   
            WITH PRIVATE KEY   
            (   
            FILE = 'C:\certs\MySQLPrivateKeyFile.PVK',   
            DECRYPTION BY PASSWORD = 'MySQLKey01'   
            );   
            GO  
  
            ```  
  
             No final dessa etapa, o computador de destino terá importado o certificado de criptografia que foi submetido a backup a partir do computador de origem. Em seguida, você pode anexar os arquivos de dados ao computador de destino.  
  
    2.  Depois, crie um banco de dados com os arquivos de dados e de log que apontam para arquivos existentes no Armazenamento do Windows Azure usando a opção FOR ATTACH. Na janela de consulta, execute a seguinte instrução:  
  
        ```tsql  
  
        --Create a database on the destination server   
        CREATE DATABASE TestDB1onDest   
        ON   
        (NAME = TestDB1_data,   
            FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Data.mdf' )   
        LOG ON   
         (NAME = TestDB1_log,   
            FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Log.ldf')   
        FOR ATTACH   
        GO  
  
        ```  
  
    3.  No Pesquisador de Objetos, clique em Bancos de Dados e clique com o botão direito em Atualizar. Você verá o banco de dados TestDB1onDest recém-criado listado.  
  
    4.  Em seguida, execute a seguinte instrução na janela de consulta:  
  
        ```tsql  
  
        USE TestDB1onDest   
        SELECT * FROM Table1;   
        GO  
  
        ```  
  
         Isso deve listar todos os dados que você inseriu na lição 4.  
  
 Observe que o banco de dados criptografado foi transferido para outra instância do computador sem o movimento de dados.  
  
 Para criar um banco de dados com os arquivos de dados e de log que apontam para arquivos existentes no Armazenamento do Windows Azure usando a interface do usuário do SQL Server Management Studio, execute estas etapas:  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do Mecanismo de Banco de Dados do SQL Server e expanda-a.  
  
2.  Clique com o botão direito do mouse em **Bancos de Dados**e clique em **Novo Banco de Dados**. Em seguida, clique com o botão direito do mouse em TestDB1. Clique em Tarefas e, em seguida, clique em Desanexar. Na janela da caixa de diálogo Desanexar, marque Descartar Conexões. Clique em **OK**.  
  
3.  Conecte-se ao computador de destino, que tem o SQL Server CTP2 2014 ou posterior. Para preparar seu computador de destino, é necessário criar uma credencial do SQL Server no computador de destino que aponte para o mesmo contêiner em que você colocou TestDB1. Se você pretende anexar novamente no mesmo computador, não será necessário criar outra credencial.  
  
4.  Na **Pesquisador de objetos**, clique com botão direito **bancos de dados** e clique em **Attach**.  
  
5.  No **anexar bancos de dados** caixa de diálogo, especifique o banco de dados a ser anexado, clique em **Add**. No **localizar arquivos de banco de dados** janela caixa de diálogo:  
  
     Para o banco de dados local do arquivo de dados, digite: `https://teststorageaccnt.blob.core.windows.net/testcontainer/`.  
  
     Nome de arquivo, digite: `TestDB1Data.mdf`.  
  
6.  Clique em **OK**.  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-6-7.gif "SQL 14 CTP2")  
  
 **Próxima lição:**  
  
 [Lição 7: Mover os arquivos de dados para o armazenamento do Windows Azure](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)  
  
  
