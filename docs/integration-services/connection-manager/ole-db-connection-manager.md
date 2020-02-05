---
title: Gerenciador de conexões OLE DB | Microsoft Docs
description: Um gerenciador de conexões OLE DB permite que um pacote se conecte a uma fonte de dados usando um provedor OLE DB.
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbconnection.f1
helpviewer_keywords:
- OLE DB connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], OLE DB
- connections [Integration Services], OLE DB
ms.assetid: 91e3622e-4b1a-439a-80c7-a00b90d66979
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aa5d978126807e1fb83c08a1d1b8d9d7b74d8368
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74687170"
---
# <a name="ole-db-connection-manager"></a>Gerenciador de conexões OLE DB

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Um gerenciador de conexões OLE DB permite que um pacote se conecte a uma fonte de dados usando um provedor OLE DB. Por exemplo, um gerenciador de conexões OLE DB que se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar o provedor OLE DB da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
    
> [!NOTE]
>  O provedor de OLEDB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 não dá suporte às novas palavras-chave de cadeia de conexão (MultiSubnetFailover=True) para clustering de failover de várias sub-redes. Para saber mais, confira as [Notas sobre a versão do SQL Server 2016](https://go.microsoft.com/fwlink/?LinkId=247824).    
> 
> [!NOTE]
>  Se a fonte de dados for [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007, ela exigirá um provedor de dados diferente das versões anteriores do Excel ou do Access. Para obter mais informações, consulte [Conectar-se a uma pasta de trabalho do Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md) e [Conectar-se a um banco de dados do Access](../../integration-services/connection-manager/connect-to-an-access-database.md).    
    
Várias tarefas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e componentes de fluxo de dados usam um gerenciador de conexões OLE DB. Por exemplo, a origem e o destino de OLE DB usam esse gerenciador de conexões para extrair e carregar dados. A tarefa Executar SQL pode usar um gerenciador de conexões de modo a conectar-se a um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar consultas.    
    
Você também pode usar o gerenciador de conexões OLE DB para acessar fontes de dados OLE DB em tarefas personalizadas gravadas em código não gerenciado que usa uma linguagem como C++.    
    
Ao adicionar um gerenciador de conexões OLE DB a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que disponibiliza uma conexão do OLE DB em runtime, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção **Conexões** no pacote.    
    
A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `OLEDB`.    
    
Você pode configurar um gerenciador de conexões OLE DB de uma das seguintes formas:    
    
-   Forneça uma cadeia de conexão específica configurada para atender aos requisitos do provedor selecionado.    
    
-   Dependendo do provedor, inclua o nome da fonte de dados à qual efetuar a conexão.    
    
-   Forneça credenciais de segurança apropriadas para o provedor selecionado.    
    
-   Indique se a conexão criada a partir do gerenciador de conexões será retida em runtime.    
    
## <a name="log-calls-and-troubleshoot-connections"></a>Chamadas de log e solução de problemas de conexões    
 Você pode registrar as chamadas que o gerenciador de conexões OLE DB faz aos provedores de dados externos. É possível solucionar problemas de conexões que o gerenciador de conexões OLE DB cria para fontes de dados externas. Para registrar as chamadas que o gerenciador de conexões OLE DB cria para os provedores de dados externos, habilite o registro do pacote e selecione o evento **Diagnóstico** no nível de pacote. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).    
    
## <a name="configure-the-ole-db-connection-manager"></a>Configurar gerenciador de conexões OLE DB    
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou de maneira programática. Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Configurar Gerenciador de Conexões OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md). Para obter mais informações sobre como configurar um gerenciador de conexões programaticamente, consulte a documentação da classe **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** no Guia do Desenvolvedor.    
    
### <a name="configure-ole-db-connection-manager"></a>Configurar o gerenciador de conexões OLE DB

Use a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** para adicionar uma conexão com uma fonte de dados. Essa conexão pode ser nova ou uma cópia de uma conexão existente.  
  
> [!NOTE]  
>  Se a fonte de dados for [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, ela exigirá um gerenciador de conexões diferente de versões anteriores do Excel. Para obter mais informações, consulte [Conectar-se a uma pasta de trabalho do Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
>   
>  Se a fonte de dados for o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007, ela exigirá um provedor OLE DB diferente das versões anteriores do Access. Para obter mais informações, consulte [Conectar-se a um banco de dados do Access](../../integration-services/connection-manager/connect-to-an-access-database.md).  
  
 Para obter mais informações sobre o gerenciador de conexões OLE DB, consulte [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
#### <a name="options"></a>Opções  
 **Conexões de dados**  
 Selecione uma conexão de dados OLE DB existente na lista.  
  
 **Propriedades de conexão de dados**  
 Exiba as propriedades e os valores da conexão de dados OLE DB selecionada.  
  
 **Novo**  
 Crie uma conexão de dados OLE DB usando a caixa de diálogo **Gerenciador de Conexões** .  
  
 **Delete (excluir)**  
 Escolha uma conexão de dados e selecione **Excluir** para excluí-la.  
  
#### <a name="managed-identities-for-azure-resources-authentication"></a>Identidades gerenciadas para autenticação de recursos do Azure
Ao executar pacotes SSIS no [Azure-SSIS Integration Runtime no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime), use a [identidade gerenciada](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity) associada ao data factory para autenticação do Banco de Dados SQL do Azure (ou da instância gerenciada). O factory designado pode acessar dados do banco de dados e copiá-los para o banco de dados usando essa identidade.

> [!NOTE]
>  Ao usar a autenticação do Azure AD (Azure Active Directory) (incluindo a autenticação de identidade gerenciada) para se conectar ao Banco de Dados SQL do Azure (ou instância gerenciada), você pode encontrar um problema relacionado à falha na execução do pacote ou alteração inesperada do comportamento. Para saber mais, confira [Recursos e limitações do Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication#azure-ad-features-and-limitations).

Para usar a autenticação de identidade gerenciada para o Banco de Dados SQL do Azure, siga estas etapas para configurar seu banco de dados:

1. [Provisione um administrador do Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server) para o servidor do SQL Azure no portal do Azure, caso ainda não tenha feito isso. O administrador do Azure AD pode ser um usuário ou um grupo do Azure AD. Se você conceder uma função de administrador ao grupo com a identidade gerenciada, ignore as etapas 2 e 3. O administrador terá acesso completo ao banco de dados.

1. [Criar usuários de banco de dados independente](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities) para a identidade gerenciada pelo data factory. Conecte-se ao banco de dados do qual ou para o qual deseja copiar dados usando ferramentas como o SSMS, com uma identidade do Azure AD que tenha, pelo menos, a permissão ALTER ANY USER. Execute o seguinte T-SQL: 
    
    ```sql
    CREATE USER [your data factory name] FROM EXTERNAL PROVIDER;
    ```

1. Conceda à identidade gerenciada do data factory as permissões necessárias, como faria normalmente para usuários do SQL e outros. Saiba mais sobre as funções adequadas em [Funções do nível de banco de dados](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles). Execute o código a seguir. Para mais opções, confira [este documento](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql).

    ```sql
    EXEC sp_addrolemember [role name], [your data factory name];
    ```

Para usar a autenticação de identidade gerenciada para a instância gerenciada do Banco de Dados SQL do Azure, siga estas etapas a fim de configurar seu banco de dados:
    
1. [Provisione um administrador do Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-managed-instance) para a instância gerenciada no portal do Azure, caso ainda não tenha feito isso. O administrador do Azure AD pode ser um usuário ou um grupo do Azure AD. Se você conceder uma função de administrador ao grupo com a identidade gerenciada, ignore as etapas 2 a 4. O administrador terá acesso completo ao banco de dados.

1. [Crie logons](https://docs.microsoft.com/sql/t-sql/statements/create-login-transact-sql?view=azuresqldb-mi-current) para a identidade gerenciada do data factory. No SSMS (SQL Server Management Studio), conecte-se à sua Instância Gerenciada usando uma conta do SQL Server que seja um **sysadmin**. No banco de dados **mestre**, execute o seguinte T-SQL:

    ```sql
    CREATE LOGIN [your data factory name] FROM EXTERNAL PROVIDER;
    ```

1. [Criar usuários de banco de dados independente](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities) para a identidade gerenciada pelo data factory. Conecte-se ao banco de dados do ou para o qual você deseja copiar dados. Execute o seguinte T-SQL: 
  
    ```sql
    CREATE USER [your data factory name] FROM EXTERNAL PROVIDER;
    ```

1. Conceda à identidade gerenciada do data factory as permissões necessárias, como faria normalmente para usuários do SQL e outros. Execute o código a seguir. Para mais opções, confira [este documento](https://docs.microsoft.com/sql/t-sql/statements/alter-role-transact-sql?view=azuresqldb-mi-current).

    ```sql
    ALTER ROLE [role name e.g., db_owner] ADD MEMBER [your data factory name];
    ```

Em seguida, configure o provedor OLE DB para o gerenciador de conexões OLE DB. Veja a seguir as opções para fazer isso:
    
- **Configurar em tempo de design.** No Designer do SSIS, clique duas vezes no gerenciador de conexões OLE DB para abrir a janela **Gerenciador de Conexões**. Na lista suspensa **Provedor**, selecione [**Microsoft OLE DB Driver for SQL Server**](https://go.microsoft.com/fwlink/?linkid=871294).
    > [!NOTE]
    >  Outros provedores na lista suspensa podem não dar suporte à autenticação da identidade gerenciada.
    
- **Configurar no runtime.** Ao executar o pacote por meio do [SSMS (SQL Server Management Studio) ](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) ou da [atividade Executar Pacote SSIS do Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity), localize a propriedade do gerenciador de conexões **ConnectionString** para o gerenciador de conexões OLE DB. Atualize a propriedade de conexão `Provider` para `MSOLEDBSQL` (ou seja, driver do OLE DB para SQL Server).
    ```vb
    Data Source=serverName;Initial Catalog=databaseName;Provider=MSOLEDBSQL;...
    ```

Por fim, configure a autenticação da identidade gerenciada para o gerenciador de conexões OLE DB. Veja a seguir as opções para fazer isso:
    
- **Configurar em tempo de design.** No Designer do SSIS, clique com o botão direito do mouse no gerenciador de conexões OLE DB e selecione **Propriedades**. Atualize a propriedade `ConnectUsingManagedIdentity` para `True`.
    > [!NOTE]
    >  Atualmente, a propriedade do gerenciador de conexões `ConnectUsingManagedIdentity` não entra em vigor (indicando que a autenticação de identidade gerenciada não funciona) quando você executa o pacote SSIS no SSIS Designer ou no SQL Server [!INCLUDE[msCoName](../../includes/msconame-md.md)].

- **Configurar no runtime.** Ao executar o pacote por meio de SSMS ou uma atividade **Executar Pacote do SQL**, localize o gerenciador de conexões OLE DB e atualize a propriedade `ConnectUsingManagedIdentity` para `True`.
    > [!NOTE]
    >  No Azure-SSIS Integration Runtime, todos os outros métodos de autenticação (por exemplo, segurança integrada e senha) pré-configurados no gerenciador de conexões OLE DB são substituídos quando a autenticação de identidade gerenciada é usada para estabelecer a conexão de banco de dados.

> [!NOTE]
>  Para configurar a autenticação de identidade gerenciada em pacotes existentes, a maneira preferencial é recompilar seu projeto SSIS com o [Designer SSIS mais recente](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) pelo menos uma vez. Reimplante esse projeto SSIS no Azure-SSIS Integration Runtime para que a nova propriedade do gerenciador de conexões `ConnectUsingManagedIdentity` seja automaticamente adicionada a todos os gerenciadores de conexões OLE DB no projeto SSIS. Como alternativa, pode-se usar diretamente uma substituição de propriedade com o caminho de propriedade **\Package.Connections [{nome do seu gerenciador de conexões}].Properties[ConnectUsingManagedIdentity]** no runtime.

## <a name="see-also"></a>Confira também    
 [Origem de OLE DB](../../integration-services/data-flow/ole-db-source.md)     
 [Destino OLE DB](../../integration-services/data-flow/ole-db-destination.md)     
 [Tarefa Executar SQL](../../integration-services/control-flow/execute-sql-task.md)     
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)    
    
  
