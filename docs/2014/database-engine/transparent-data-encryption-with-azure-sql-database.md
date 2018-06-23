---
title: Transparent Data Encryption com o Banco de Dados SQL do Azure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-security
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- TDE, SQL Database
- Transparent Data Encryption, SQL Database
- encryption (SQL Database) TDE
ms.assetid: 0bf7e8ff-1416-4923-9c4c-49341e208c62
caps.latest.revision: 31
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 1850458778cadbfe871880d42a7830c94078c2a4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120854"
---
# <a name="transparent-data-encryption-with-azure-sql-database"></a>Transparent Data Encryption com o Banco de Dados SQL do Azure
  [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] criptografia de dados transparente (visualização) ajuda a proteger contra a ameaça de atividades mal-intencionadas executando criptografia em tempo real e a descriptografia do banco de dados, backups associados e arquivos de log de transações em repouso sem exigir alterações no aplicativo.  
  
 Ela criptografa o armazenamento de um banco de dados inteiro usando uma chave simétrica chamada de chave de criptografia de banco de dados. No [!INCLUDE[ssSDS](../includes/sssds-md.md)] , a chave de criptografia do banco de dados é protegida por um certificado do servidor interno. O certificado do servidor interno é exclusivo para cada servidor [!INCLUDE[ssSDS](../includes/sssds-md.md)] . Se um banco de dados está em uma relação de GeoDR, ele é protegido por uma chave diferente em cada servidor. Se dois bancos de dados estão conectados ao mesmo servidor, eles compartilham o mesmo certificado interno. [!INCLUDE[msCoName](../includes/msconame-md.md)] gira automaticamente esses certificados pelo menos a cada 90 dias. Para obter uma descrição geral do TDE, consulte [TDE &#40;Transparent Data Encryption&#41;](../relational-databases/security/encryption/transparent-data-encryption.md).  
  
 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] não dá suporte à integração do Cofre da Chave do Azure com TDE. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em execução em uma máquina virtual do Azure pode usar uma chave assimétrica do Cofre da Chave. Para obter mais informações, consulte [exemplo a: Transparent Data Encryption usando uma chave assimétrica do Cofre de chaves](../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md#ExampleA).  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[sqldbesa](../includes/sqldbesa-md.md)] ([visualização em algumas regiões](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).|  
  
> [!IMPORTANT]  
>  Este é um recurso de visualização. Eu reconheço e Concordo que a implementação de [!INCLUDE[ssSDS](../includes/sssds-md.md)] criptografia transparente de dados em meus bancos de dados está sujeito aos termos de visualização em meu contrato de licença (por exemplo, o Enterprise Agreement, contrato do Microsoft Azure ou assinatura Online da Microsoft Contrato), bem como qualquer aplicável [termos de uso da visualização do Microsoft Azure](http://azure.microsoft.com/support/legal/preview-supplemental-terms/).  
  
 A visualização do status da TDE aplica-se até mesmo ao subconjunto de regiões geográficas em que versão da família V12 de [!INCLUDE[ssSDS](../includes/sssds-md.md)] é anunciada como apresentando agora status de disponibilidade geral. A TDE para [!INCLUDE[ssSDS](../includes/sssds-md.md)] não se destina para uso em bancos de dados de produção até o [!INCLUDE[msCoName](../includes/msconame-md.md)] anunciar a promoção da TDE, de visualização para GA. Para obter mais informações sobre [!INCLUDE[ssSDS](../includes/sssds-md.md)] V12, consulte [Novidades no Banco de Dados SQL do Azure](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/).  
  
##  <a name="Permissions"></a> Permissões  
 Para inscrever-se para a visualizar e configurar TDE por meio do portal do Azure, usando a API REST ou usando o PowerShell, você deve estar conectado como o proprietário do Azure, Colaborador ou Gerenciador de segurança do SQL.  
  
 Para configurar a TDE usando [!INCLUDE[tsql](../includes/tsql-md.md)] , é requerido o seguinte:  
  
-   Você já deve estar inscrito para a visualização da TDE.  
  
-   Para criar a chave de criptografia de banco de dados deve ser um [!INCLUDE[ssSDS](../includes/sssds-md.md)] administrador ou você deve ser um membro do **dbmanager** função no mestre de banco de dados e ter o **controle** no banco de dados.  
  
-   Para executar a instrução ALTER DATABASE com a opção SET só requer a associação na função **dbmanager** .  
  
##  <a name="Preview"></a> Inscreva-se para a visualização da TDE e habilite TDE em um banco de dados  
  
1.  Visite o Portal do Azure em [ https://portal.azure.com ](https://portal.azure.com) e entrar com sua conta de administrador do Azure ou colaborador.  
  
2.  Na faixa à esquerda, clique para **PROCURAR**e, em seguida, clique em **Bancos de dados SQL**.  
  
3.  Com **Bancos de dados SQL** selecionado no painel esquerdo, clique em seu banco de dados de usuário.  
  
4.  Na folha do banco de dados, clique em **Todas as configurações**.  
  
5.  Na folha **Configurações** , clique na parte **Transparent Data Encryption (visualização)** para abrir a folha **VISUALIZAÇÃO da Transparent Data Encryption** . Se você ainda não estiver inscrito para a visualização de TDE, as configurações de criptografia de dados serão desabilitadas até que você conclua a inscrição.  
  
6.  Clique em **TERMOS DE VISUALIZAÇÃO**.  
  
7.  Leia os termos da visualização e, se você concordar com os termos, selecione o **termos de encryptionPreview de dados transparente** caixa de seleção e, em seguida, clique em **Okey** próximo à parte inferior da página. Retornando para o **dados encryptionPREVIEW** folha, onde o **criptografia de dados** botão agora deve ser habilitado.  
  
8.  Na folha **VISUALIZAÇÃO da criptografia de dados** , mova o botão **Criptografia de dados** para **Ligado**, e, em seguida, clique em **Salvar** (na parte superior da página) para aplicar a configuração. O **Status de criptografia** aproximará o progresso da Transparent Data Encryption.  
  
     ![SQLDB_TDE_TermsNewUI](../../2014/database-engine/media/sqldb-tde-termsnewui.png "SQLDB_TDE_TermsNewUI")  
  
     Você também pode monitorar o progresso da criptografia conectando [!INCLUDE[ssSDS](../includes/sssds-md.md)] usando uma ferramenta de consulta como [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] como um usuário de banco de dados com a permissão **EXIBIR ESTADO DO BANCO DE DADOS** . Consulta o `encryption_state` coluna o [sys.DM database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) exibição.  
  
##  <a name="Encrypt"></a> Habilitando a TDE em [!INCLUDE[ssSDS](../includes/sssds-md.md)] usando Transact-SQL  
 Nas etapas a seguir, suponha que você já se inscreveu para a visualização.  
  
###  <a name="TsqlProcedure"></a>  
  
1.  Conecte-se ao banco de dados usando um logon que seja um administrador ou um membro da função **dbmanager** no banco de dados mestre.  
  
2.  Execute as seguintes instruções para criar uma chave de criptografia do banco de dados e criptografar o banco de dados.  
  
    ```  
    -- Create the database encryption key that will be used for TDE.  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER CERTIFICATE ##MS_TdeCertificate##;  
  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;  
    GO  
    ```  
  
3.  Para monitorar o progresso de criptografia em [!INCLUDE[ssSDS](../includes/sssds-md.md)], aos usuários de banco de dados de **VIEW DATABASE STATE** permissão pode consultar o `encryption_state` coluna do [sys.DM database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) modo de exibição.  
  
## <a name="enabling-tde-on-sql-database-by-using-powershell"></a>Habilitando a TDE no banco de dados SQL usando PowerShell  
 Usando o Azure PowerShell, você pode executar o seguinte comando para ligar/desligar a TDE. Você precisa se conectar a sua conta na janela de PS antes de executar o comando. Nas etapas a seguir, suponha que você já se inscreveu para a visualização. Para obter informações adicionais sobre o PowerShell, consulte [Como instalar e configurar o Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).  
  
1.  Para habilitar a TDE, retorne o status de TDE e exiba a atividade de criptografia.  
  
    ```  
    PS C:\> Switch-AzureMode -Name AzureResourceManager  
  
    PS C:\> Set-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Enabled"  
  
    PS C:\> Get-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    PS C:\> Get-AzureSqlDatabaseTransparentDataEncryptionActivity -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1"  
  
    ```  
  
2.  Para desabilitar a TDE:  
  
    ```  
    PS C:\> Set-AzureSqlDatabaseTransparentDataEncryption -ServerName "myserver" -ResourceGroupName "Default-SQL-WestUS" -DatabaseName "database1" -State "Disabled"  
  
    PS C:\> Switch-AzureMode -Name AzureServiceManagement  
    ```  
  
##  <a name="Decrypt"></a> Descriptografar um banco de dados protegido por TDE no [!INCLUDE[ssSDS](../includes/sssds-md.md)]  
  
#### <a name="to-disable-tde-by-using-the-azure-portal"></a>Para desabilitar a TDE usando o Portal do Azure  
  
1.  Visite o Portal do Azure em [ https://portal.azure.com ](https://portal.azure.com) e entrar com sua conta de administrador do Azure ou colaborador.  
  
2.  Na faixa à esquerda, clique para **PROCURAR**e, em seguida, clique em **Bancos de dados SQL**.  
  
3.  Com **Bancos de dados SQL** selecionado no painel esquerdo, clique em seu banco de dados de usuário.  
  
4.  Na folha do banco de dados, clique em **Todas as configurações**.  
  
5.  Na folha **Configurações** , clique na parte **Transparent Data Encryption (visualização)** para abrir a folha **VISUALIZAÇÃO da Transparent Data Encryption** .  
  
6.  Na folha **VISUALIZAÇÃO da Transparent Data Encryption** , mova o botão **Criptografia de dados** para **Desligado**e, em seguida, clique em **Salvar** (na parte superior da página) para aplicar a configuração. O **Status de criptografia** aproximará o progresso de descriptografia de dados transparente.  
  
     Você também pode monitorar o progresso da descriptografia conectando-se ao [!INCLUDE[ssSDS](../includes/sssds-md.md)] usando uma ferramenta de consulta como [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] como um usuário de banco de dados com a permissão **EXIBIR ESTADO DE BANCO DE DADOS** . Consulta o `encryption_state` coluna o [sys.DM database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)exibição.  
  
#### <a name="to-disable-tde-by-using-transact-sql"></a>Para desabilitar a TDE usando Transact-SQL  
  
1.  Conecte-se ao banco de dados usando um logon que seja um administrador ou um membro da função **dbmanager** no banco de dados mestre.  
  
2.  Execute as seguintes instruções para descriptografar o banco de dados.  
  
    ```  
    -- Enable encryption  
    ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;  
    GO  
    ```  
  
3.  Para monitorar o progresso de criptografia em [!INCLUDE[ssSDS](../includes/sssds-md.md)], aos usuários de banco de dados de **VIEW DATABASE STATE** permissão pode consultar o `encryption_state` coluna do [sys.DM database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) modo de exibição.  
  
##  <a name="Working"></a> Trabalhando com TDE bancos de dados protegidos em [!INCLUDE[ssSDS](../includes/sssds-md.md)]  
 Não é necessário descriptografar bancos de dados para operações no Azure. As configurações de TDE no banco de dados de origem ou banco de dados primário são herdadas de forma transparente no destino. Isso inclui operações envolvendo:  
  
-   Restauração Geográfica  
  
-   Recuperação Pontual de Autoatendimento  
  
-   Restaurar um Banco de Dados Excluído  
  
-   Replicação Geográfica Ativa  
  
-   Criar uma Cópia do Banco de Dados  
  
##  <a name="Moving"></a> Mover um banco de dados protegido por TDE usando. Arquivos Bacpac  
 Quando exportar um protegido por TDE usando a função Exportar banco de dados do banco de dados de [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] Portal ou o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Assistente de importação e exportação, o conteúdo do banco de dados não está criptografado. O conteúdo é armazenado em arquivos. bacpac que não estão criptografados.  Certifique-se de proteger os arquivos. bacpac adequadamente e habilitar a TDE após a conclusão da importação do novo banco de dados.  
  
## <a name="related-sql-server-topic"></a>Tópico do SQL Server relacionado  
 [Habilitar a TDE usando EKM](../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
## <a name="see-also"></a>Consulte também  
 [TDE &#40;Transparent Data Encryption&#41;](../relational-databases/security/encryption/transparent-data-encryption.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
  
