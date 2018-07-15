---
title: Fazer backup, restaurar e mover o catálogo do SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bf806aef-8556-48ab-aed5-e95de9a2204e
caps.latest.revision: 10
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 79ae1eb490823b18509a5b26432bb05b68131c46
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37250916"
---
# <a name="backup-restore-and-move-the-ssis-catalog"></a>Fazer backup, restaurar e mover o catálogo do SSIS
  [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] inclui o banco de dados do SSISDB. Você consulta exibições no banco de dados SSISDB para inspecionar objetos, configurações e dados operacionais que são armazenados no catálogo do **SSISDB** . Este tópico fornece instruções para fazer backup do banco de dados e restaurá-lo.  
  
 O catálogo do **SSISDB** armazena os pacotes que você implantou no servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para obter mais informações sobre o catálogo, consulte [Catálogo do SSIS](catalog/ssis-catalog.md).  
  
##  <a name="backup"></a> Para fazer o backup do banco de dados SSIS  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e conecte-se a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
2.  Faça backup da chave mestra para o banco de dados do SSISDB, usando a instrução Transact-SQL BACKUP MASTER KEY. A chave é armazenada em um arquivo que você especifica. Use a senha para criptografar a chave mestra no arquivo.  
  
     Para obter mais informações sobre a instrução, consulte [BACKUP MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-master-key-transact-sql).  
  
     No exemplo a seguir, a chave mestra é exportada para o arquivo `c:\temp directory\RCTestInstKey`. A senha `LS2Setup!` é usada para criptografar a chave mestra.  
  
    ```  
    backup master key to file = 'c:\temp\RCTestInstKey'  
           encryption by password = 'LS2Setup!'  
  
    ```  
  
3.  Faça backup do banco de dados do SSISDB usando a caixa de diálogo **Backup de Banco de Dados** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Como fazer backup de um banco de dados (SQL Server Management Studio)](http://go.microsoft.com/fwlink/?LinkId=231812).  
  
4.  Gere o script de CREATE LOGIN para ##MS_SSISServerCleanupJobLogin ##, fazendo o seguinte. Para obter mais informações, veja [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql).  
  
    1.  No Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], expanda o nó **Segurança** e expanda o nó **Logons**.  
  
    2.  Clique com o botão direito do mouse em **##MS_SSISServerCleanupJobLogin##** e clique em **Script de Logon como** > **CREATE To** > **Nova Janela do Editor de Consultas**.  
  
5.  Se você estiver restaurando o banco de dados SSISDB para uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] na qual o catálogo do SSISDB nunca foi criado, gere o script CREATE PROCEDURE para sp_ssis_startup, fazendo o seguinte. Para obter mais informações, consulte [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql).  
  
    1.  No Pesquisador de Objetos, expanda o nó **Bancos de Dados** e, em seguida, expanda o nó **mestre** > **Programação** > **Procedimentos Armazenados**.  
  
    2.  Clique com o botão direito do mouse em **dbo.sp_ssis_startup**e clique em **Script de Procedimento Armazenado como** > **CREATE To** > **Nova Janela do Editor de Consultas**.  
  
6.  Confirme que o SQL Server Agent foi iniciado  
  
7.  Se você estiver restaurando o banco de dados SSISDB para uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] na qual o catálogo do SSISDB nunca foi criado, gere um script para o Trabalho de Manutenção do Servidor SSIS, fazendo o seguinte. O script é criado automaticamente no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent quando o catálogo do SSISDB é criado. O trabalho ajuda a limpar os logs da operação de limpeza fora da janela de retenção e remove versões anteriores de projetos.  
  
    1.  No Pesquisador de Objetos, expanda o nó **SQL Server Agent** e, em seguida, expanda o nó **Trabalhos** .  
  
    2.  Clique com o botão direito do mouse em Trabalho de Manutenção do Servidor SSIS e clique em **Script de Trabalho como** > **CREATE To** > **Nova Janela do Editor de Consultas**.  
  
### <a name="to-restore-the-ssis-database"></a>Para restaurar o banco de dados SSIS  
  
1.  Se você estiver restaurando o banco de dados SSISDB para uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] onde o catálogo do SSISDB nunca foi criado, habilite o clr (Common Language Runtime) executando o procedimento armazenado sp_configure. Para obter mais informações, veja [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) e [Opção clr habilitado](http://go.microsoft.com/fwlink/?LinkId=231855).  
  
    ```  
    use master   
           sp_configure 'clr enabled', 1  
           reconfigure  
  
    ```  
  
2.  Se você estiver restaurando o banco de dados SSISDB para uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] onde o catálogo do SSISDB nunca foi criado, crie a chave assimétrica e o logon da chave assimétrica e conceda permissão UNSAFE para o logon.  
  
    ```  
    Create Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey  
           FROM Executable File = 'C:\Program Files\Microsoft SQL Server\110\DTS\Binn\Microsoft.SqlServer.IntegrationServices.Server.dll'  
  
    ```  
  
     Os procedimentos armazenados CLR do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] exigem que permissões de UNSAFE sejam concedidas ao logon porque o logon exige acesso adicional a recursos restritos, como a API do Microsoft Win32. Para obter mais informações sobre a permissão de código UNSAFE, consulte [Criando um assembly](../relational-databases/clr-integration/assemblies/creating-an-assembly.md).  
  
    ```  
    Create Login MS_SQLEnableSystemAssemblyLoadingUser  
           FROM Asymmetric key MS_SQLEnableSystemAssemblyLoadingKey   
  
           Grant unsafe Assembly to MS_SQLEnableSystemAssemblyLoadingUser  
  
    ```  
  
3.  Restaure o banco de dados SSISDB do backup usando a caixa de diálogo **Restaurar Banco de Dados** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte os tópicos a seguir.  
  
    -   [Restaurar banco de dados &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)  
  
    -   [Restaurar banco de dados &#40;página Arquivos&#41;](../relational-databases/backup-restore/restore-database-files-page.md)  
  
    -   [Restaurar banco de dados &#40;página Opções&#41;](../relational-databases/backup-restore/restore-database-options-page.md)  
  
4.  Execute os scripts que você criou no procedimento [Para fazer backup do banco de dados SSIS](#backup) para ##MS_SSISServerCleanupJobLogin##, sp_ssis_startup e Trabalho de Manutenção do Servidor SSIS. Confirme que o SQL Server Agent foi iniciado.  
  
5.  Execute a instrução a seguir para definir o procedimento sp_ssis_startup para execução automática. Para obter mais informações, veja [sp_procoption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-procoption-transact-sql).  
  
    ```  
    EXEC sp_procoption N'sp_ssis_startup','startup','on'  
    ```  
  
6.  Mapeie o usuário do SSISDB ##MS_SSISServerCleanupJobUser## (banco de dados do SSISDB) para ##MS_SSISServerCleanupJobLogin## usando a caixa de diálogo **Propriedades de Logon** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
7.  Restaure a chave mestra usando um dos seguintes métodos. Para obter mais informações sobre criptografia, consulte [Hierarquia de criptografia](../relational-databases/security/encryption/encryption-hierarchy.md).  
  
    -   **Método 1**  
  
         Use este método se você já executou um backup da chave mestra do banco de dados e você tem a senha usada para criptografar a chave mestra.  
  
        ```  
               Restore master key from file = 'c:\temp\RCTestInstKey'  
               Decryption by password = 'LS2Setup!' -- 'Password used to encrypt the master key during SSISDB backup'  
               Encryption by password = 'LS3Setup!' -- 'New Password'  
               Force  
  
        ```  
  
        > [!NOTE]  
        >  Confirme que a conta de serviço do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tem permissões para ler o arquivo da chave de backup.  
  
        > [!NOTE]  
        >  Você verá a seguinte mensagem de aviso exibida no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] se a chave mestra de banco de dados ainda não tiver sido criptografada pela chave mestra de serviço. Ignore a mensagem de aviso.  
        >   
        >  **A chave mestra atual não pode ser descriptografada. O erro foi ignorado porque a opção FORCE foi especificada.**  
        >   
        >  O argumento FORCE especifica que o processo de restauração deve continuar mesmo se a chave mestra de banco de dados atual não estiver aberta. Para o catálogo do SSISDB, como a chave mestra de banco de dados não foi aberta na instância onde você está restaurando o banco de dados, você verá esta mensagem.  
  
    -   **Método 2**  
  
         Use este método se você tiver a senha original que foi usada para criar o SSISDB.  
  
        ```  
        open master key decryption by password = 'LS1Setup!' --'Password used when creating SSISDB'  
               Alter Master Key Add encryption by Service Master Key  
        ```  
  
8.  Determine se o esquema de catálogo SSISDB e os binários [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (ISServerExec e SQLCLR assembly) são compatíveis executando [catalog.check_schema_version](/sql/integration-services/system-stored-procedures/catalog-check-schema-version).  
  
9. Para confirmar que o banco de dados do SSISDB foi restaurado com êxito, execute operações no catálogo d SSISDB, por exemplo, executar pacotes que foram implantados no servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para obter mais informações, consulte [Executar um pacote no servidor SSIS usando o SQL Server Management Studio](run-a-package-on-the-ssis-server-using-sql-server-management-studio.md).  
  
### <a name="to-move-the-ssis-database"></a>Para mover o banco de dados SSIS  
  
-   Siga as instruções para mover bancos de dados de usuários. Para obter mais informações, veja [Mover bancos de dados de usuário](../relational-databases/databases/move-user-databases.md).  
  
     Assegure-se de fazer backup da chave mestra do banco de dados SSISDB e proteger o arquivo de backup. Para obter mais informações, consulte [Para fazer o backup do banco de dados SSIS](#backup).  
  
     Verifique se os objetos pertinentes do Integration Services (SSIS) estão criados na nova instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] na qual o catálogo do SSISDB ainda não foi criado.  
  
  
