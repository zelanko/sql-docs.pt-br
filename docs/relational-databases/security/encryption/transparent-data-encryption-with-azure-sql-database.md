---
title: Transparent Data Encryption com o Banco de Dados SQL do Azure | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
- MSDN content
- MSDN - SQL DB
ms.date: 09/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TDE, SQL Database
- encryption (SQL Database), TDE
- Transparent Data Encryption, SQL Database
ms.assetid: 0bf7e8ff-1416-4923-9c4c-49341e208c62
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1c607015f1ead5b19d4c32c5bac62eb624b0578b
ms.lasthandoff: 04/11/2017

---
# <a name="transparent-data-encryption-with-azure-sql-database"></a>Transparent Data Encryption com o Banco de Dados SQL do Azure
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx_md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] A Transparent Data Encryption ajuda a proteger contra a ameaça de atividades mal-intencionadas executando criptografia e descriptografia em tempo real do banco de dados, backups associados e arquivos de log de transações em repouso sem exigir alterações no aplicativo.  
  
 Ela criptografa o armazenamento de um banco de dados inteiro usando uma chave simétrica chamada de chave de criptografia de banco de dados. No [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] , a chave de criptografia do banco de dados é protegida por um certificado do servidor interno. O certificado do servidor interno é exclusivo para cada servidor [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] . Se um banco de dados está em uma relação de GeoDR, ele é protegido por uma chave diferente em cada servidor. Se dois bancos de dados estão conectados ao mesmo servidor, eles compartilham o mesmo certificado interno. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] gira automaticamente esses certificados pelo menos a cada 90 dias. Para obter uma descrição geral do TDE, consulte [TDE &#40;Transparent Data Encryption&#41;](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md).  
  
 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] não dá suporte à integração do Cofre da Chave do Azure com TDE. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em execução em uma máquina virtual do Azure pode usar uma chave assimétrica do Cofre da Chave. Para obter mais informações, veja [Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
##  <a name="Permissions"></a> Permissões  
 Para configurar a TDE por meio do portal do Azure, usando a API REST ou usando o PowerShell, você deve estar conectado como o proprietário do Azure, o Colaborador ou o Gerenciador de segurança do SQL.  
  
 Para configurar a TDE usando [!INCLUDE[tsql](../../../includes/tsql-md.md)] , é requerido o seguinte:  
  
-   Para executar a instrução ALTER DATABASE com a opção SET é necessário haver associação na função **dbmanager** .  
  
##  <a name="Preview"></a> Habilitar a TDE em um banco de dados usando o Portal  
  
1.  Visite o Portal do Azure em [https://portal.azure.com](https://portal.azure.com) e entre com sua conta do Administrador ou Colaborador do Azure.  
  
2.  Na faixa à esquerda, clique para **PROCURAR**e, em seguida, clique em **Bancos de dados SQL**.  
  
3.  Com **Bancos de dados SQL** selecionado no painel esquerdo, clique em seu banco de dados de usuário.  
  
4.  Na folha do banco de dados, clique em **Todas as configurações**.  
  
5.  Na folha **Configurações** , clique na parte **Transparent Data Encryption** para abrir a folha **Transparent Data Encryption** .  
  
6.  Na folha **Criptografia de dados** , mova o botão da **Criptografia de dados** para **Ligado**e, em seguida, clique em **Salvar** (na parte superior da página) para aplicar a configuração. O **Status de criptografia** aproximará o progresso da Transparent Data Encryption.  
  
     ![Iniciar a criptografia TDE do Banco de Dados SQL](../../../relational-databases/security/encryption/media/sqldb-tde-encrypt.png "Iniciar a criptografia TDE do Banco de Dados SQL")  
  
     Você também pode monitorar o progresso da criptografia conectando [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] usando uma ferramenta de consulta como [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] como um usuário de banco de dados com a permissão **EXIBIR ESTADO DO BANCO DE DADOS** . Consulte a coluna **encryption_state** da exibição [sys.dm_database_encryption_keys](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) .  
  
##  <a name="Encrypt"></a> Habilitando a TDE em [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] usando Transact-SQL  
 As etapas a seguir habilitam a TDE.  
  
###  <a name="TsqlProcedure"></a>  
  
1.  Conecte-se ao banco de dados usando um logon que seja um administrador ou um membro da função **dbmanager** no banco de dados mestre.  
  
2.  Execute as seguintes instruções para criptografar o banco de dados.  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;  
    GO  
    ```  
  
3.  Para monitorar o andamento de criptografia em [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], os usuários de banco de dados com a permissão **VIEW DATABASE STATE** podem consultar a coluna **encryption_state** da exibição [sys.dm_database_encryption_keys](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) .  
  
##  <a name="EncryptPS"></a> Habilitando e desabilitando a TDE em [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] usando o PowerShell  
 Usando o Azure PowerShell, você pode executar o seguinte comando para ligar/desligar a TDE. Você deve se conectar à sua conta na janela de PS antes de executar o comando. Personalizar o exemplo para usar os valores para o `ServerName`, `ResourceGroupName`, e os `DatabaseName` parâmetros. Para obter informações adicionais sobre o PowerShell, consulte [Como instalar e configurar o Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).  
  
> [!NOTE]  
>  Para continuar, você deve instalar e configurar a versão 1.0 do Azure PowerShell. A versão 0.9.8 pode ser usada, mas ela foi preterida e precisar alternar para os cmdlets do AzureResourceManager usando o comando `PS C:\> Switch-AzureMode -Name AzureResourceManager` .  
  
###  <a name="PSlProcedure"></a>  
  
1.  Para habilitar a TDE, retorne o status de TDE e exiba a atividade de criptografia:  
  
    ```  
    PS C:\> Set-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Enabled"  
  
    PS C:\> Get-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    PS C:\> Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
    ```  
  
     Se estiver usando a versão 0.9.8, use os comandos Set-AzureSqlDatabaseTransparentDataEncryption, Get-AzureSqlDatabaseTransparentDataEncryption e Get-AzureSqlDatabaseTransparentDataEncryptionActivity.  
  
2.  Para desabilitar a TDE:  
  
    ```  
    PS C:\> Set-AzureRMSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Disabled"  
  
    ```  
  
     Se estiver usando a versão 0.9.8, use o comando Set-AzureSqlDatabaseTransparentDataEncryption.  
  
##  <a name="Decrypt"></a> Descriptografar um banco de dados protegido por TDE no [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]  
  
#### <a name="to-disable-tde-by-using-the-azure-portal"></a>Para desabilitar a TDE usando o Portal do Azure  
  
1.  Visite o Portal do Azure em [https://portal.azure.com](https://portal.azure.com) e entre com sua conta do Administrador ou Colaborador do Azure.  
  
2.  Na faixa à esquerda, clique para **PROCURAR**e, em seguida, clique em **Bancos de dados SQL**.  
  
3.  Com **Bancos de dados SQL** selecionado no painel esquerdo, clique em seu banco de dados de usuário.  
  
4.  Na folha do banco de dados, clique em **Todas as configurações**.  
  
5.  Na folha **Configurações** , clique na parte **Transparent Data Encryption** para abrir a folha **Transparent Data Encryption** .  
  
6.  Na folha **Transparent Data Encryption** , mova o botão **Criptografia de dados** para **Desligado**e clique em **Salvar** (na parte superior da página) para aplicar a configuração. O **Status de criptografia** aproximará o progresso de descriptografia de dados transparente.  
  
     Você também pode monitorar o progresso da descriptografia conectando-se ao [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] usando uma ferramenta de consulta como [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] como um usuário de banco de dados com a permissão **EXIBIR ESTADO DE BANCO DE DADOS** . Consulte a coluna **encryption_state** da exibição [sys.dm_database_encryption_keys](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) .  
  
#### <a name="to-disable-tde-by-using-transact-sql"></a>Para desabilitar a TDE usando Transact-SQL  
  
1.  Conecte-se ao banco de dados usando um logon que seja um administrador ou um membro da função **dbmanager** no banco de dados mestre.  
  
2.  Execute as seguintes instruções para descriptografar o banco de dados.  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;  
    GO  
    ```  
  
3.  Para monitorar o andamento de criptografia em [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], os usuários de banco de dados com a permissão **VIEW DATABASE STATE** podem consultar a coluna **encryption_state** da exibição [sys.dm_database_encryption_keys](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) .  
  
##  <a name="Working"></a> Movendo um banco de dados protegido por TDE no [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]  
 Não é necessário descriptografar bancos de dados para operações no Azure. As configurações de TDE no banco de dados de origem ou banco de dados primário são herdadas de forma transparente no destino. Isso inclui operações envolvendo:  
  
-   Restauração Geográfica  
  
-   Recuperação Pontual de Autoatendimento  
  
-   Restaurar um Banco de Dados Excluído  
  
-   Replicação Geográfica Ativa  
  
-   Criar uma Cópia do Banco de Dados  
  
 Ao exportar um banco de dados protegido por TDE usando a função Exportar Banco de Dados no Portal do [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] ou no Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , o conteúdo exportado do banco de dados não será criptografado. Esse conteúdo exportado é armazenado em arquivos .bacpac não criptografados. Certifique-se de proteger os arquivos. bacpac adequadamente e habilitar a TDE após a conclusão da importação do novo banco de dados. 
 
 Por exemplo, se o arquivo .bacpac for exportado de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]local, o conteúdo importado do novo banco de dados não será criptografado automaticamente. Da mesma forma, se o arquivo .bacpac for exportado de um [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] para um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]local, o novo banco de dados também não será criptografado automaticamente.  
 
 A única exceção é durante a exportação do [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] – a TDE será habilitada no novo banco de dados, mas o arquivo .bacpac em si ainda não estará criptografado.
  
## <a name="related-sql-server-topic"></a>Tópico do SQL Server relacionado  
 [Habilitar TDE no SQL Server usando EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
## <a name="see-also"></a>Consulte também  
 [TDE &#40;Transparent Data Encryption&#41;](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql.md)  
  
  

