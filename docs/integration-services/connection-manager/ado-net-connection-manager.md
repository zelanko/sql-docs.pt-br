---
title: Gerenciador de conexões ADO.NET | Microsoft Docs
description: Um gerenciador de conexões ADO.NET permite que um pacote acesse fontes de dados usando um provedor .NET.
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetconnection.f1
helpviewer_keywords:
- connection managers [Integration Services], ADO.NET
- ADO.NET connection manager [Integration Services]
- connections [Integration Services], ADO.NET
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d61b7423bb39267fe4171d661e8fe7a74fbc6faa
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294485"
---
# <a name="adonet-connection-manager"></a>Gerenciador de conexões ADO.NET

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Um gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] permite que um pacote acesse fontes de dados usando um provedor .NET. Normalmente, você usa esse gerenciador de conexões para acessar fontes de dados, como [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você também pode acessar fontes de dados expostas por meio de OLE DB e XML em tarefas personalizadas escritas em código gerenciado usando uma linguagem, como C#.  
  
Quando você adiciona um gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a um pacote, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que é resolvido como uma conexão [!INCLUDE[vstecado](../../includes/vstecado-md.md)] em tempo de execução. Ele define as propriedades do gerenciador de conexões e adiciona esse gerenciador à coleção de **Conexões** do pacote.  
  
A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `ADO.NET`. O valor de `ConnectionManagerType` está qualificado para incluir o nome do provedor .NET usado pelo gerenciador de conexões.  
  
## <a name="adonet-connection-manager-troubleshooting"></a>Solução de problemas do gerenciador de conexões ADO.NET  
Você pode registrar as chamadas que o gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] faz a provedores de dados externos. É possível solucionar problemas de conexões que o gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] cria para fontes de dados externas. Para registrar as chamadas que o gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] faz aos provedores de dados externos, habilite o registro do pacote e selecione o evento **Diagnóstico** no nível de pacote. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
Ao serem lidos por um gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)], certos tipos de dados de data do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geram os resultados mostrados na tabela a seguir.  
  
|Tipo de dados do SQL Server|Resultado|  
|--------------------------|------------|  
|**time**, **datetimeoffset**|O pacote apresentará erros, a menos que use comandos com parâmetros SQL. Para utilizar comandos SQL parametrizados, use a tarefa Executar SQL em seu pacote. Para obter mais informações, consulte [Tarefa Executar SQL](../../integration-services/control-flow/execute-sql-task.md) e [Parâmetros e códigos de retorno na Tarefa Executar SQL](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).|  
|**datetime2**|O gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] trunca o valor de milissegundo.|  
  
> [!NOTE]  
>  Para obter mais informações sobre tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e como eles são associados a tipos de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) e [Tipos de dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="adonet-connection-manager-configuration"></a>Configuração do gerenciador de conexões ADO.NET  
  
Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou de maneira programática.  
  
-   Forneça uma cadeia de conexão específica configurada para atender aos requisitos do provedor .NET selecionado.  
  
-   Dependendo do provedor, inclua o nome da fonte de dados à qual efetuar a conexão.  
  
-   Forneça credenciais de segurança apropriadas para o provedor selecionado.  
  
-   Indique se a conexão criada a partir do gerenciador de conexões será retida em tempo de execução.  
  
Muitas das opções de configuração do gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] dependem do provedor .NET que o gerenciador de conexões usa.  
  
Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)], confira [Configurar gerenciador de conexões ADO.NET](../../integration-services/connection-manager/configure-ado-net-connection-manager.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
### <a name="configure-adonet-connection-manager"></a>Configurar Gerenciador de Conexões ADO.NET
Use a caixa de diálogo **Configurar gerenciador de conexões ADO.NET** para adicionar uma conexão a uma fonte de dados que pode ser acessada usando um provedor de dados .NET Framework. Por exemplo, um provedor desse tipo é o SqlClient. O gerenciador de conexões pode usar uma conexão existente ou você pode criar uma nova.  
  
 Para saber mais sobre o gerenciador de conexões ADO.NET, consulte [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md).  
  
#### <a name="options"></a>Opções  
**Conexões de dados**  
Selecione uma conexão de dados ADO.NET existente na lista.  
  
**Propriedades de conexão de dados**  
Exiba as propriedades e os valores da conexão de dados ADO.NET selecionada.  
  
**Nova**  
Crie uma conexão de dados ADO.NET utilizando a caixa de diálogo do **Gerenciador de Conexões** .  
  
**Delete (excluir)**  
Selecione uma conexão e selecione **Excluir** para excluí-la.  
  
#### <a name="managed-identities-for-azure-resources-authentication"></a>Identidades gerenciadas para autenticação de recursos do Azure
Ao executar pacotes SSIS no [Azure-SSIS Integration Runtime no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime), você pode usar a [identidade gerenciada](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity) associada ao data factory para a autenticação do Banco de Dados SQL do Azure (ou da instância gerenciada). O factory designado pode acessar dados do banco de dados e copiá-los para o banco de dados usando essa identidade.

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

Para usar a autenticação de identidade gerenciada para a instância gerenciada do Banco de Dados SQL do Azure, siga estas etapas a fim de configurar seu banco de dados:
    
1. [Provisione um administrador do Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-managed-instance) para a instância gerenciada no portal do Azure, caso ainda não tenha feito isso. O administrador do Azure AD pode ser um usuário ou um grupo do Azure AD. Se você conceder uma função de administrador ao grupo com a identidade gerenciada, ignore as etapas 2 a 5. O administrador terá acesso completo ao banco de dados.

1. [Encontre a identidade gerenciada do data factory no portal do Azure](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity). Acesse as **Propriedades** do data factory. Copie a **ID do Aplicativo da Identidade Gerenciada** (não a **ID de Objeto da Identidade Gerenciada**).

1. Converta a identidade gerenciada do data factory em tipo binário. Conecte-se ao banco de dados **mestre** na instância gerenciada usando ferramentas como o SSMS com sua conta de administrador do SQL ou do Active Directory. Execute o seguinte T-SQL no banco de dados **mestre** para obter a ID do aplicativo de identidade gerenciada como tipo binário:
    
    ```sql
    DECLARE @applicationId uniqueidentifier = '{your managed identity application ID}'
    select CAST(@applicationId AS varbinary)
    ```

1. Adicione a identidade gerenciada do data factory como um usuário à instância gerenciada do Banco de Dados SQL do Azure. Execute o seguinte T-SQL no banco de dados **mestre**:
    
    ```sql
    CREATE LOGIN [{a name for the managed identity}] FROM EXTERNAL PROVIDER with SID = {your managed identity application ID as binary}, TYPE = E
    ```

1. Conceda as permissões necessárias da identidade gerenciada do data factory. Saiba mais sobre as funções adequadas em [Funções do nível de banco de dados](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles). Execute o seguinte T-SQL no banco de dados do qual ou para o qual deseja copiar os dados:

    ```sql
    CREATE USER [{the managed identity name}] FOR LOGIN [{the managed identity name}] WITH DEFAULT_SCHEMA = dbo
    ALTER ROLE [role name] ADD MEMBER [{the managed identity name}]
    ```

Por fim, configure a autenticação da identidade gerenciada para o gerenciador de conexões ADO.NET. Veja a seguir as opções para fazer isso:
    
- **Configurar em tempo de design.** No Designer do SSIS, clique com o botão direito do mouse no gerenciador de conexões ADO.NET e clique em **Propriedades**. Atualize a propriedade `ConnectUsingManagedIdentity` para `True`.
    > [!NOTE]
    >  Atualmente, a propriedade do gerenciador de conexões `ConnectUsingManagedIdentity` não entra em vigor (indicando que a autenticação de identidade gerenciada não funciona) quando você executa o pacote SSIS no SSIS Designer ou no SQL Server [!INCLUDE[msCoName](../../includes/msconame-md.md)].
    
- **Configurar no tempo de execução.** Ao executar o pacote via [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) ou a [atividade Executar Pacote SSIS do Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity), localize o gerenciador de conexões ADO.NET. Atualize sua propriedade `ConnectUsingManagedIdentity` para `True`.
    > [!NOTE]
    >  No Azure-SSIS Integration Runtime, todos os outros métodos de autenticação (por exemplo, autenticação integrada e senha) pré-configurados no gerenciador de conexões ADO.NET são substituídos quando a autenticação de identidade gerenciada é usada para estabelecer uma conexão de banco de dados.

> [!NOTE]
>  Para configurar a autenticação de identidade gerenciada em pacotes existentes, a maneira preferencial é recompilar seu projeto SSIS com o [Designer SSIS mais recente](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) pelo menos uma vez. Reimplante esse projeto SSIS para o Azure-SSIS Integration Runtime, para que a nova propriedade do gerenciador de conexões `ConnectUsingManagedIdentity` seja automaticamente adicionada a todos os gerenciadores de conexões ADO.NET no projeto SSIS. Como alternativa, pode-se usar diretamente uma substituição de propriedade com o caminho de propriedade **\Package.Connections [{nome do seu gerenciador de conexões}].Properties[ConnectUsingManagedIdentity]** no tempo de execução.

## <a name="see-also"></a>Confira também  
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
