---
title: Gerenciador de conexões OLE DB | Microsoft Docs
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
ms.openlocfilehash: 70e439dd6ed176fbb9c2d2fe666b314bd48f2f9c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904267"
---
# <a name="ole-db-connection-manager"></a>gerenciador de conexões OLE DB

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Um gerenciador de conexões OLE DB permite que um pacote se conecte a uma fonte de dados usando um provedor OLE DB. Por exemplo, um gerenciador de conexões OLE DB que se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar o provedor OLE DB da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
    
> [!NOTE]
>  O provedor de OLEDB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 não dá suporte às novas palavras-chave de cadeia de conexão (MultiSubnetFailover=True) para clustering de failover de várias sub-redes. Para obter mais informações, consulte as [SQL Server Release Notes](https://go.microsoft.com/fwlink/?LinkId=247824) (Notas de versão do SQL Server) e o post do blog [Always On Multi-Subnet Failover and SSIS](https://www.mattmasson.com/2012/03/alwayson-multi-subnet-failover-and-ssis/)(Failover de várias sub-redes AlwaysOn e SSIS) em www.mattmasson.com.    
> 
> [!NOTE]
>  Se a fonte de dados for [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007, ela exigirá um provedor de dados diferente das versões anteriores do Excel ou do Access. Para obter mais informações, consulte [Conectar-se a uma pasta de trabalho do Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md) e [Conectar-se a um banco de dados do Access](../../integration-services/connection-manager/connect-to-an-access-database.md).    
    
 Várias tarefas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e componentes de fluxo de dados usam um gerenciador de conexões OLE DB. Por exemplo, a fonte e o destino do OLE DB usam esse gerenciador de conexões para extrair e carregar dados e a tarefa Executar SQL pode usar esse gerenciador de conexões para se conectar a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar consultas.    
    
 O gerenciador de conexões OLE DB também é usado para acessar fontes de dados OLE DB em tarefas personalizadas gravadas em código não gerenciado que usa uma linguagem como C++.    
    
 Ao adicionar um gerenciador de conexões OLE DB a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que disponibilizará uma conexão do OLE DB em tempo de execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção **Connections** no pacote.    
    
 A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **OLEDB**.    
    
 O gerenciador de conexões OLE DB pode ser configurado das seguintes maneiras:    
    
-   Forneça uma cadeia de conexão específica configurada para atender aos requisitos do provedor selecionado.    
    
-   Dependendo do provedor, inclua o nome da fonte de dados à qual efetuar a conexão.    
    
-   Forneça credenciais de segurança apropriadas para o provedor selecionado.    
    
-   Indique se a conexão criada a partir do gerenciador de conexões será retida em tempo de execução.    
    
## <a name="logging"></a>Log    
 Você pode registrar as chamadas que o gerenciador de conexões OLE DB faz aos provedores de dados externos. É possível usar esse recurso de registro para solucionar problemas de conexões que o gerenciador de conexões OLE DB cria para as fontes de dados externas. Para registrar as chamadas que o gerenciador de conexões OLE DB cria para os provedores de dados externos, habilite o registro do pacote e selecione o evento **Diagnóstico** no nível de pacote. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).    
    
## <a name="configuration-of-the-oledb-connection-manager"></a>Configuração do gerenciador de conexões OLEDB    
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Configurar Gerenciador de Conexões OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md). Para obter mais informações sobre como configurar um gerenciador de conexões programaticamente, consulte a documentação da classe **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** no Guia do Desenvolvedor.    
    
## <a name="related-content"></a>Conteúdo relacionado    
    
-   Artigo do Wiki, [SSIS with Oracle Connectors](https://go.microsoft.com/fwlink/?LinkId=220670) (SSIS com Conectores Oracle) em social.technet.microsoft.com.    
    
-   Artigo técnico, [Connection Strings for OLE DB Providers](https://go.microsoft.com/fwlink/?LinkId=220744)(Cadeias de conexão para provedores de OLE DB), em carlprothman.net.    
    
## <a name="configure-ole-db-connection-manager"></a>Configurar Gerenciador de Conexões OLE DB
  Use a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** para adicionar uma conexão a uma fonte de dados, seja ela uma nova conexão ou a cópia de uma conexão existente.  
  
> [!NOTE]  
>  Se a fonte de dados for [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, ela exigirá um gerenciador de conexões diferente de versões anteriores do Excel. Para obter mais informações, consulte [Conectar-se a uma pasta de trabalho do Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
>   
>  Se a fonte de dados for o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007, ela exigirá um provedor OLE DB diferente das versões anteriores do Access. Para obter mais informações, consulte [Conectar-se a um banco de dados do Access](../../integration-services/connection-manager/connect-to-an-access-database.md).  
  
 Para obter mais informações sobre o gerenciador de conexões OLE DB, consulte [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Conexões de dados**  
 Selecione uma conexão de dados OLE DB existente na lista.  
  
 **Propriedades de conexão de dados**  
 Exiba as propriedades e os valores da conexão de dados OLE DB selecionada.  
  
 **Nova**  
 Crie uma conexão de dados OLE DB usando a caixa de diálogo **Gerenciador de Conexões** .  
  
 **Delete (excluir)**  
 Selecione uma conexão de dados e a exclua usando o botão **Excluir** .  
  
### <a name="managed-identities-for-azure-resources-authentication"></a>Identidades gerenciadas para autenticação de recursos do Azure
Ao executar pacotes SSIS no [Azure-SSIS Integration Runtime no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime), você pode usar a [identidade gerenciada](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity) associada ao data factory para a autenticação do Banco de Dados SQL do Azure (ou da Instância Gerenciada). O factory designado pode acessar dados do banco de dados e copiá-los para o banco de dados usando essa identidade.

Para usar a autenticação de identidade gerenciada para o Banco de Dados SQL do Azure, siga estas etapas para configurar seu banco de dados:

1. **Crie um grupo no Azure AD.** Torne a identidade gerenciada um membro do grupo.
    
   1. [Encontre a identidade gerenciada do data factory no portal do Azure](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity). Acesse as **Propriedades** do data factory. Copie a **ID de Objeto da Identidade Gerenciada**.
    
   1. Instale o módulo do [PowerShell do Azure AD](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2). Entre usando o comando `Connect-AzureAD`. Execute os comandos a seguir para criar um grupo e adicionar a identidade gerenciada como um membro.
      ```powershell
      $Group = New-AzureADGroup -DisplayName "<your group name>" -MailEnabled $false -SecurityEnabled $true -MailNickName "NotSet"
      Add-AzureAdGroupMember -ObjectId $Group.ObjectId -RefObjectId "<your data factory managed identity object ID>"
      ```
    
1. **[Provisione um administrador do Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server)** para o servidor do SQL Azure no portal do Azure, caso ainda não tenha feito isso. O administrador do Azure AD pode ser um usuário ou um grupo do Azure AD. Se você conceder uma função de administrador ao grupo com a identidade gerenciada, ignore as etapas 3 e 4. O administrador terá acesso completo ao banco de dados.

1. **[Crie usuários de banco de dados independente](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)** para o grupo do Azure AD. Conecte-se ao banco de dados do qual ou para o qual deseja copiar dados usando ferramentas como o SSMS, com uma identidade do Azure AD que tenha, pelo menos, a permissão ALTER ANY USER. Execute o seguinte T-SQL: 
    
    ```sql
    CREATE USER [your AAD group name] FROM EXTERNAL PROVIDER;
    ```

1. **Conceda as permissões necessárias ao grupo do Azure AD** como faria normalmente para usuários do SQL e outros. Por exemplo, execute o seguinte código:

    ```sql
    ALTER ROLE [role name] ADD MEMBER [your AAD group name];
    ```

Para usar a autenticação de identidade gerenciada para a Instância Gerenciada do Banco de Dados SQL do Azure, siga estas etapas para configurar seu banco de dados:
    
1. **[Provisione um administrador do Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-managed-instance)** para a instância gerenciada no portal do Azure, caso ainda não tenha feito isso. O administrador do Azure AD pode ser um usuário ou um grupo do Azure AD. Se você conceder uma função de administrador ao grupo com a identidade gerenciada, ignore as etapas 2 a 5. O administrador terá acesso completo ao banco de dados.

1. **[Encontre a identidade gerenciada do data factory no portal do Azure](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity)** . Acesse as **Propriedades** do data factory. Copie a **ID do Aplicativo da Identidade Gerenciada** (NÃO a **ID de Objeto da Identidade Gerenciada**).

1. **Converter a identidade gerenciada do data factory em tipo binário**. Conecte-se ao banco de dados **mestre** na instância gerenciada usando ferramentas como o SSMS com sua conta de administrador do SQL/do Active Directory. Execute o seguinte T-SQL no banco de dados **mestre** para obter a ID do aplicativo de identidade gerenciada como binário:
    
    ```sql
    DECLARE @applicationId uniqueidentifier = '{your managed identity application ID}'
    select CAST(@applicationId AS varbinary)
    ```

1. **Adicione a identidade gerenciada do data factory como um usuário** à Instância Gerenciada do Banco de Dados SQL do Azure. Execute o seguinte T-SQL no banco de dados **mestre**:
    
    ```sql
    CREATE LOGIN [{a name for the managed identity}] FROM EXTERNAL PROVIDER with SID = {your managed identity application ID as binary}, TYPE = E
    ```

1. **Conceda as permissões necessárias da identidade gerenciada do data factory**. Execute o seguinte T-SQL no banco de dados do qual ou para o qual deseja copiar os dados:

    ```sql
    CREATE USER [{the managed identity name}] FOR LOGIN [{the managed identity name}] WITH DEFAULT_SCHEMA = dbo
    ALTER ROLE db_owner ADD MEMBER [{the managed identity name}]
    ```

Em seguida, **configure o provedor OLE DB** para o gerenciador de conexões OLE DB. Há duas opções para fazer isso.
    
1. Configurar em tempo de design. No Designer do SSIS, clique duas vezes no gerenciador de conexões OLE DB para abrir a janela **Gerenciador de Conexões**. Na lista suspensa **Provedor**, selecione [**Microsoft OLE DB Driver for SQL Server**](https://go.microsoft.com/fwlink/?linkid=871294).
    > [!NOTE]
    >  Outros provedores na lista suspensa PODEM NÃO dar suporte à autenticação da identidade gerenciada.
    
1. Configurar em tempo de execução. Quando você executar o pacote por meio do [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) ou da [atividade Executar Pacote SSIS do Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity), localize a propriedade do gerenciador de conexões **ConnectionString** do gerenciador de conexões OLE DB e atualize a propriedade de conexão **Provider** para **MSOLEDBSQL** (ou seja, Microsoft OLE DB Driver for SQL Server).
    ```vb
    Data Source=serverName;Initial Catalog=databaseName;Provider=MSOLEDBSQL;...
    ```

Por fim, **configure a autenticação da identidade gerenciada** para o gerenciador de conexões OLE DB. Há duas opções para fazer isso.
    
1. Configurar em tempo de design. No Designer do SSIS, clique com o botão direito do mouse no gerenciador de conexões OLE DB e clique em **Propriedades** para abrir a **janela Propriedades**. Atualize a propriedade **ConnectUsingManagedIdentity** para **True**.
    > [!NOTE]
    >  Atualmente, a propriedade **ConnectUsingManagedIdentity** do gerenciador de conexões NÃO entra em vigor (indicando que a autenticação de identidade gerenciada não funciona) quando você executa o pacote SSIS no Designer do SSIS ou no [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server.

1. Configurar em tempo de execução. Quando você executar o pacote por meio do SSMS ou da atividade Executar Pacote do SQL, localize o gerenciador de conexões OLE DB e atualize sua propriedade **ConnectUsingManagedIdentity** como **True**.
    > [!NOTE]
    >  No Azure-SSIS Integration Runtime, todos os outros métodos de autenticação (por exemplo, segurança integrada, senha) pré-configurados no gerenciador de conexões OLE DB serão **substituídos** quando a autenticação de identidade gerenciada for usada para estabelecer a conexão de banco de dados.

> [!NOTE]
>  Para configurar a autenticação de identidade gerenciada em pacotes existentes, recompile o projeto do SSIS com o [Designer do SSIS mais recente](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) pelo menos uma vez e reimplante esse projeto do SSIS no Azure-SSIS Integration Runtime, de modo que a nova propriedade do gerenciador de conexões **ConnectUsingManagedIdentity** seja adicionada automaticamente a todos os gerenciadores de conexões OLE DB no projeto do SSIS.

## <a name="see-also"></a>Consulte Também    
 [Origem de OLE DB](../../integration-services/data-flow/ole-db-source.md)     
 [Destino OLE DB](../../integration-services/data-flow/ole-db-destination.md)     
 [Tarefa Executar SQL](../../integration-services/control-flow/execute-sql-task.md)     
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)    
    
  
