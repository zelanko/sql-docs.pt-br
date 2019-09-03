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
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a1a7c3d0e1648bb2c05e20c78ed293e33a34fe47
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155170"
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
    
Ao adicionar um gerenciador de conexões OLE DB a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que disponibiliza uma conexão do OLE DB em tempo de execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção **Conexões** no pacote.    
    
A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `OLEDB`.    
    
Você pode configurar um gerenciador de conexões OLE DB de uma das seguintes formas:    
    
-   Forneça uma cadeia de conexão específica configurada para atender aos requisitos do provedor selecionado.    
    
-   Dependendo do provedor, inclua o nome da fonte de dados à qual efetuar a conexão.    
    
-   Forneça credenciais de segurança apropriadas para o provedor selecionado.    
    
-   Indique se a conexão criada a partir do gerenciador de conexões será retida em tempo de execução.    
    
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
  
 **Nova**  
 Crie uma conexão de dados OLE DB usando a caixa de diálogo **Gerenciador de Conexões** .  
  
 **Delete (excluir)**  
 Escolha uma conexão de dados e selecione **Excluir** para excluí-la.  
  
#### <a name="managed-identities-for-azure-resources-authentication"></a>Identidades gerenciadas para autenticação de recursos do Azure
Ao executar pacotes SSIS no [Azure-SSIS Integration Runtime no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime), use a [identidade gerenciada](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity) associada ao data factory para autenticação do Banco de Dados SQL do Azure (ou da instância gerenciada). O factory designado pode acessar dados do banco de dados e copiá-los para o banco de dados usando essa identidade.

> [!NOTE]
>  Ao usar a autenticação do Azure AD (Azure Active Directory) (incluindo a autenticação de identidade gerenciada) para se conectar ao Banco de Dados SQL do Azure (ou instância gerenciada), você pode encontrar um problema relacionado à falha na execução do pacote ou alteração inesperada do comportamento. Para saber mais, confira [Recursos e limitações do Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication#azure-ad-features-and-limitations).

Para usar a autenticação de identidade gerenciada para o Banco de Dados SQL do Azure, siga estas etapas para configurar seu banco de dados:

1. Crie um grupo no Azure AD. Torne a identidade gerenciada um membro do grupo.
    
   1. [Encontre a identidade gerenciada do data factory no portal do Azure](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity). Acesse as **Propriedades** do data factory. Copie a **ID de Objeto da Identidade Gerenciada**.
    
   1. Instale o módulo do [PowerShell do Azure AD](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2). Entre usando o comando `Connect-AzureAD`. Execute os comandos a seguir para criar um grupo e adicionar a identidade gerenciada como um membro.
      ```powershell
      $Group = New-AzureADGroup -DisplayName "<your group name>" -MailEnabled $false -SecurityEnabled $true -MailNickName "NotSet"
      Add-AzureAdGroupMember -ObjectId $Group.ObjectId -RefObjectId "<your data factory managed identity object ID>"
      ```
    
1. [Provisione um administrador do Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server) para o servidor do SQL Azure no portal do Azure, caso ainda não tenha feito isso. O administrador do Azure AD pode ser um usuário ou um grupo do Azure AD. Se você conceder uma função de administrador ao grupo com a identidade gerenciada, ignore as etapas 3 e 4. O administrador terá acesso completo ao banco de dados.

1. [Crie usuários de banco de dados independente](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities) para o grupo do Azure AD. Conecte-se ao banco de dados do qual ou para o qual deseja copiar dados usando ferramentas como o SSMS, com uma identidade do Azure AD que tenha, pelo menos, a permissão ALTER ANY USER. Execute o seguinte T-SQL: 
    
    ```sql
    CREATE USER [your AAD group name] FROM EXTERNAL PROVIDER;
    ```

1. Conceda as permissões necessárias ao grupo do Azure AD como faria normalmente para usuários do SQL e outros. Saiba mais sobre as funções adequadas em [Funções do nível de banco de dados](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles). Por exemplo, execute o seguinte código:

    ```sql
    ALTER ROLE [role name] ADD MEMBER [your AAD group name];
    ```

Para usar a autenticação de identidade gerenciada para a Instância Gerenciada do Banco de Dados SQL do Azure, siga estas etapas para configurar seu banco de dados:
    
1. [Provisione um administrador do Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-managed-instance) para a instância gerenciada no portal do Azure, caso ainda não tenha feito isso. O administrador do Azure AD pode ser um usuário ou um grupo do Azure AD. Se você conceder uma função de administrador ao grupo com a identidade gerenciada, ignore as etapas 2 a 5. O administrador terá acesso completo ao banco de dados.

1. [Encontre a identidade gerenciada do data factory no portal do Azure](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity). Acesse as **Propriedades** do data factory. Copie a **ID do Aplicativo da Identidade Gerenciada** (não a **ID de Objeto da Identidade Gerenciada**).

1. Converta a identidade gerenciada do data factory em tipo binário. Conecte-se ao banco de dados **mestre** na instância gerenciada usando ferramentas como o SSMS com sua conta de administrador do SQL ou do Active Directory. Execute o seguinte T-SQL no banco de dados **mestre** para obter a ID do aplicativo de identidade gerenciada como tipo binário:
    
    ```sql
    DECLARE @applicationId uniqueidentifier = '{your managed identity application ID}'
    select CAST(@applicationId AS varbinary)
    ```

1. Adicione a identidade gerenciada do data factory como um usuário à Instância Gerenciada do Banco de Dados SQL do Azure. Execute o seguinte T-SQL no banco de dados **mestre**:
    
    ```sql
    CREATE LOGIN [{a name for the managed identity}] FROM EXTERNAL PROVIDER with SID = {your managed identity application ID as binary}, TYPE = E
    ```

1. Conceda as permissões necessárias da identidade gerenciada do data factory. Saiba mais sobre as funções adequadas em [Funções do nível de banco de dados](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles). Execute o seguinte T-SQL no banco de dados do qual ou para o qual deseja copiar os dados:

    ```sql
    CREATE USER [{the managed identity name}] FOR LOGIN [{the managed identity name}] WITH DEFAULT_SCHEMA = dbo
    ALTER ROLE [role name] ADD MEMBER [{the managed identity name}]
    ```

Em seguida, configure o provedor OLE DB para o gerenciador de conexões OLE DB. Veja a seguir duas opções para fazer isso:
    
- **Configurar em tempo de design.** No Designer do SSIS, clique duas vezes no gerenciador de conexões OLE DB para abrir a janela **Gerenciador de Conexões**. Na lista suspensa **Provedor**, selecione [**Microsoft OLE DB Driver for SQL Server**](https://go.microsoft.com/fwlink/?linkid=871294).
    > [!NOTE]
    >  Outros provedores na lista suspensa podem não dar suporte à autenticação da identidade gerenciada.
    
- **Configurar em tempo de execução.** Ao executar o pacote por meio do [SSMS (SQL Server Management Studio) ](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) ou da [atividade Executar Pacote SSIS do Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity), localize a propriedade do gerenciador de conexões **ConnectionString** para o gerenciador de conexões OLE DB. Atualize a propriedade de conexão `Provider` para `MSOLEDBSQL` (ou seja, driver do OLE DB para SQL Server).
    ```vb
    Data Source=serverName;Initial Catalog=databaseName;Provider=MSOLEDBSQL;...
    ```

Por fim, configure a autenticação da identidade gerenciada para o gerenciador de conexões OLE DB. Veja a seguir duas opções para fazer isso:
    
- **Configurar em tempo de design.** No Designer do SSIS, clique com o botão direito do mouse no gerenciador de conexões OLE DB e selecione **Propriedades**. Atualize a propriedade `ConnectUsingManagedIdentity` para `True`.
    > [!NOTE]
    >  Atualmente, a propriedade do gerenciador de conexões `ConnectUsingManagedIdentity` não entra em vigor (indicando que a autenticação de identidade gerenciada não funciona) quando você executa o pacote SSIS no SSIS Designer ou no SQL Server [!INCLUDE[msCoName](../../includes/msconame-md.md)].

- **Configurar em tempo de execução.** Ao executar o pacote por meio de SSMS ou uma atividade **Executar Pacote do SQL**, localize o gerenciador de conexões OLE DB e atualize a propriedade `ConnectUsingManagedIdentity` para `True`.
    > [!NOTE]
    >  No Azure-SSIS Integration Runtime, todos os outros métodos de autenticação (por exemplo, segurança integrada e senha) pré-configurados no gerenciador de conexões OLE DB são substituídos quando a autenticação de identidade gerenciada é usada para estabelecer a conexão de banco de dados.

> [!NOTE]
>  Para configurar a autenticação de identidade gerenciada em pacotes existentes, a maneira preferencial é recompilar seu projeto SSIS com o [Designer SSIS mais recente](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) pelo menos uma vez. Reimplante esse projeto SSIS no Azure-SSIS Integration Runtime para que a nova propriedade do gerenciador de conexões `ConnectUsingManagedIdentity` seja automaticamente adicionada a todos os gerenciadores de conexões OLE DB no projeto SSIS. Como alternativa, pode-se usar diretamente a substituição de propriedade com o caminho de propriedade **\Package.Connections [{nome do seu gerenciador de conexões}].Properties[ConnectUsingManagedIdentity]** no tempo de execução.

## <a name="see-also"></a>Confira também    
 [Origem de OLE DB](../../integration-services/data-flow/ole-db-source.md)     
 [Destino OLE DB](../../integration-services/data-flow/ole-db-destination.md)     
 [Tarefa Executar SQL](../../integration-services/control-flow/execute-sql-task.md)     
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)    
    
  
