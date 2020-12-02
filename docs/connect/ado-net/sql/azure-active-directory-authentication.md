---
title: Usar a autenticação do Azure Active Directory com o SqlClient
description: Descreve como usar os modos de autenticação do Azure Active Directory com suporte para se conectar a fontes de dados do SQL do Azure com o SqlClient
ms.date: 11/20/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: karinazhou
ms.author: v-jizho2
ms.reviewer: ''
ms.openlocfilehash: 0f8aaffc1f87b33a5c685b55d724fe96c44258af
ms.sourcegitcommit: ece151df14dc2610d96cd0d40b370a4653796d74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96297943"
---
# <a name="using-azure-active-directory-authentication-with-sqlclient"></a>Usar a autenticação do Azure Active Directory com o SqlClient

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE [Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Este artigo descreve como se conectar a fontes de dados do SQL do Azure usando a autenticação do Azure AD (Azure Active Directory) em um aplicativo .NET com o SqlClient.

A autenticação do Azure AD usa identidades para acessar fontes de dados do SQL do Azure, como o Banco de Dados SQL do Azure, a Instância Gerenciada de SQL do Azure e o Azure Synapse Analytics. O namespace **Microsoft.Data.SqlClient** permite que aplicativos cliente especifiquem as credenciais do Azure AD em diferentes modos de autenticação quando estão se conectando ao Banco de Dados SQL do Azure. 

Quando você define a propriedade de conexão `Authentication` na cadeia de conexão, o cliente pode escolher um modo de autenticação preferencial do Azure AD de acordo com o valor fornecido:

- A versão mais antiga do **Microsoft.Data.SqlClient** dá suporte a `Active Directory Password` para o .NET Framework, .NET Core e .NET Standard. Ela também dá suporte à autenticação `Active Directory Integrated` e `Active Directory Interactive` para o .NET Framework. 

- Começando com o **Microsoft.Data.SqlClient** 2.0.0, o suporte à autenticação `Active Directory Integrated` e `Active Directory Interactive` foi estendido para o .NET Framework, .NET Core e .NET Standard. 

  Um novo modo de autenticação `Active Directory Service Principal` também foi adicionado no SqlClient 2.0.0. Ele usa a ID do cliente e o segredo de uma identidade de entidade de serviço para realizar a autenticação. 

- Mais modos de autenticação foram adicionados no **Microsoft.Data.SqlClient** 2.1.0, incluindo `Active Directory Device Code Flow` e `Active Directory Managed Identity` (também conhecido como `Active Directory MSI`). Esses novos modos permitem que o aplicativo adquira um token de acesso para se conectar ao servidor. 

Para obter mais informações sobre a autenticação do Azure AD além das descritas nas seções a seguir, confira [Conectar-se ao Banco de Dados SQL usando a autenticação do Azure Active Directory](/azure/azure-sql/database/authentication-aad-overview).


## <a name="setting-azure-active-directory-authentication"></a>Configurar a autenticação do Azure Active Directory

Quando o aplicativo está se conectando a fontes de dados do SQL do Azure usando a autenticação do Azure AD, ele precisa fornecer um modo de autenticação válido. A tabela a seguir lista os modos de autenticação com suporte. O aplicativo especifica um modo usando a propriedade de conexão `Authentication` na cadeia de conexão.

| Valor | Descrição  | Estrutura    | Versão do Microsoft.Data.SqlClient |
|:--|:--|:--|:--:|
| Senha do Active Directory | Autentique com a identidade do Azure Active Directory usando um nome de usuário e uma senha | .NET Framework 4.6+, .NET Core 2.1+, .NET Standard 2.0+  | 1.0+|
| Integrado ao Active Directory |Autentique com a identidade do Azure AD usando a autenticação integrada | .NET Framework 4.6+, .NET Core 2.1+, .NET Standard 2.0+ | 2.0.0+<sup>1</sup> |
| Interativa do Active Directory | Autentique com a identidade do Azure AD usando a autenticação interativa | .NET Framework 4.6+, .NET Core 2.1+, .NET Standard 2.0+ | 2.0.0+<sup>1</sup> |
| Entidade de serviço do Active Directory | Autentique com uma identidade do Azure AD usando a ID do cliente e o segredo de uma identidade de entidade de serviço | .NET Framework 4.6+, .NET Core 2.1+, .NET Standard 2.0+ | 2.0.0+ |
| Fluxo de código de dispositivo do Active Directory | Autentique com uma identidade do Azure AD usando o modo de Fluxo de código de dispositivo | .NET Framework 4.6+, .NET Core 2.1+, .NET Standard 2.0+ | 2.1.0+ |
| Identidade gerenciada do Active Directory, <br>MSI do Active Directory | Autentique com uma identidade do Azure AD usando a identidade gerenciada atribuída pelo sistema ou pelo usuário | .NET Framework 4.6+, .NET Core 2.1+, .NET Standard 2.0+ | 2.1.0+ |

<sup>1</sup> Antes do **Microsoft.Data.SqlClient** 2.0.0, as autenticações `Active Directory Integrated` e `Active Directory Interactive` têm suporte apenas no .NET Framework 4.6+. 


## <a name="using-active-directory-password-authentication"></a>Usar a autenticação de senha do Azure Active Directory

O modo de autenticação `Active Directory Password` dá suporte à autenticação para fontes de dados do Azure com o Azure AD para usuários nativos ou federados do Azure AD. Quando você estiver usando esse modo, as credenciais do usuário deverão ser fornecidas na cadeia de conexão. O exemplo a seguir mostra como usar a autenticação `Active Directory Password`.

```c#
// Use your own server, database, user ID, and password.
string ConnectionString = @"Server=demo.database.windows.net; Authentication=Active Directory Password; Database=testdb; User Id=user@domain.com; Password=**_";

using (SqlConnection conn = new SqlConnection(ConnectionString)) {
    conn.Open();
}
```


## <a name="using-active-directory-integrated-authentication"></a>Usar a autenticação integrada do Active Directory

Para usar modo de autenticação `Active Directory Integrated`, você precisa federar a instância do Active Directory local com o Azure AD na nuvem. Você pode fazer a federação usando os AD FS (Serviços de Federação do Active Directory), por exemplo.

Com esse modo, quando você estiver conectado a um computador conectado ao domínio, poderá acessar as fontes de dados do SQL do Azure sem que as credenciais sejam solicitadas. Não é possível especificar o nome de usuário e a senha na cadeia de conexão para aplicativos .NET Framework. Nos aplicativos .NET Core e .NET Standard, o nome de usuário é opcional na cadeia de conexão. Não é possível definir a propriedade `Credential` de SqlConnection nesse modo. 

O snippet de código a seguir é um exemplo de quando a autenticação `Active Directory Integrated` está em uso.

```c#
// Use your own server and database.
string ConnectionString1 = @"Server=demo.database.windows.net; Authentication=Active Directory Integrated; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString1)) {
    conn.Open();
}

// User ID is optional for .NET Core and .NET Standard.
string ConnectionString2 = @"Server=demo.database.windows.net; Authentication=Active Directory Integrated; Database=testdb; User Id=user@domain.com";

using (SqlConnection conn = new SqlConnection(ConnectionString2)) {
    conn.Open();
}
```


## <a name="using-active-directory-interactive-authentication"></a>Usar a autenticação Interativa do Active Directory

A autenticação `Active Directory Interactive` dá suporte à tecnologia de autenticação multifator para se conectar a fontes de dados do SQL do Azure. Se você fornecer esse modo de autenticação na cadeia de conexão, uma tela de autenticação do Azure será exibida e solicitará que o usuário insira credenciais válidas. Não é possível especificar a senha na cadeia de conexão. 

Não é possível definir a propriedade `Credential` de SqlConnection nesse modo. Com o _ *Microsoft.Data.SqlClient** 2.0.0 e posterior, é possível usar o nome de usuário na cadeia de conexão quando se está no modo interativo. 

O exemplo a seguir mostra como usar a autenticação `Active Directory Interactive`.

```c#
// Use your own server, database, and user ID.
// User ID is optional.
string ConnectionString1 = @"Server=demo.database.windows.net; Authentication=Active Directory Interactive; Database=testdb; User Id=user@domain.com";

using (SqlConnection conn = new SqlConnection(ConnectionString1)) {
    conn.Open();
}

// User ID is not provided.
string ConnectionString2 = @"Server=demo.database.windows.net; Authentication=Active Directory Interactive; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString2)) {
    conn.Open();
}
```


## <a name="using-active-directory-service-principal-authentication"></a>Usar a autenticação de Entidade de Serviço do Active Directory

No modo de autenticação `Active Directory Service Principal`, o aplicativo cliente pode se conectar a fontes de dados do SQL do Azure fornecendo a ID do cliente e o segredo de uma identidade de entidade de serviço. A autenticação de entidade de serviço envolve:
1. Configuração de um registro de aplicativo com um segredo.
1. Concessão de permissões para o aplicativo na instância do Banco de Dados SQL do Azure.
1. Conexão com a credencial correta. 

O exemplo a seguir mostra como usar a autenticação `Active Directory Service Principal`.

```c#
// Use your own server, database, app ID, and secret.
string ConnectionString = @"Server=demo.database.windows.net; Authentication=Active Directory Service Principal; Database=testdb; User Id=AppId; Password=secret";

using (SqlConnection conn = new SqlConnection(ConnectionString)) {
    conn.Open();
}
```


## <a name="using-active-directory-device-code-flow-authentication"></a>Usar a autenticação de Fluxo de código do dispositivo do Active Directory

Com a [MSAL.NET](/azure/active-directory/develop/msal-overview) (Biblioteca de Autenticação da Microsoft para .NET), a autenticação `Active Directory Device Code Flow` permite que o aplicativo cliente se conecte a fontes de dados do SQL do Azure em dispositivos e sistemas operacionais que não têm um navegador da Web interativo. A autenticação interativa será executada em outro dispositivo. Para saber mais sobre a autenticação de fluxo de código de dispositivo, confira [Fluxo de código do dispositivo OAuth 2.0](/azure/active-directory/develop/v2-oauth2-device-code). 

Quando esse modo estiver em uso, não será possível definir a propriedade `Credential` de `SqlConnection`. Além disso, o nome de usuário e a senha não devem ser especificados na cadeia de conexão. 

O trecho de código a seguir é um exemplo de uso da autenticação `Active Directory Device Code Flow`.

```c#
// Use your own server and database.
string ConnectionString = @"Server=demo.database.windows.net; Authentication=Active Directory Device Code Flow; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString)) {
    conn.Open();
}
```


## <a name="using-active-directory-managed-identity-authentication"></a>Usar a autenticação de Identidade gerenciada do Active Directory

As *identidades gerenciadas* de recursos do Azure é o novo nome para o serviço anteriormente conhecido como MSI (Identidade de Serviço Gerenciada). Quando um aplicativo cliente usa um recurso do Azure para acessar um serviço do Azure que dá suporte à autenticação do Azure AD, você pode usar as identidades gerenciadas para fazer a autenticação fornecendo uma identidade ao recurso no Azure AD. Depois, você poderá usar essa identidade para obter tokens de acesso. Isso pode eliminar a necessidade de gerenciar credenciais e segredos. 

Há dois tipos de identidades gerenciadas: 

- A _identidade gerenciada atribuída pelo sistema_ é criada em uma instância de serviço no Azure AD. Ela está vinculada ao ciclo de vida dessa instância de serviço. 
- _Uma identidade gerenciada atribuída pelo usuário_ é criada como um recurso autônomo do Azure. Ela pode ser atribuída a uma ou mais instâncias de um serviço do Azure. 

Para saber mais sobre identidades gerenciadas, confira [Sobre as identidades gerenciadas para recursos do Azure](/azure/active-directory/managed-identities-azure-resources/overview).

Desde o **Microsoft.Data.SqlClient** 2.1.0, o driver dá suporte à autenticação para o Banco de Dados SQL do Azure, o Azure Synapse Analytics e a Instância Gerenciada de SQL do Azure adquirindo tokens de acesso por meio de identidade gerenciada. Para usar essa autenticação, especifique `Active Directory Managed Identity` ou `Active Directory MSI` na cadeia de conexão; nenhuma senha será necessária. 

Também não é possível definir a propriedade `Credential` de `SqlConnection` nesse modo. Para uma identidade gerenciada atribuída pelo usuário, o nome de usuário deve ser fornecido. 

O exemplo a seguir mostra como usar a autenticação `Active Directory Managed Identity` com uma identidade gerenciada atribuída pelo sistema.

```c#
// For system-assigned managed identity
// Use your own server and database.
string ConnectionString1 = @"Server=demo.database.windows.net; Authentication=Active Directory Managed Identity; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString1)) {
    conn.Open();
}

string ConnectionString2 = @"Server=demo.database.windows.net; Authentication=Active Directory MSI; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString2)) {
    conn.Open();
}
```

O exemplo a seguir demonstra a autenticação `Active Directory Managed Identity` com uma identidade gerenciada atribuída pelo usuário.

```c#
// For user-assigned managed identity
// Use your own server, database, and user ID.
string ConnectionString1 = @"Server=demo.database.windows.net; Authentication=Active Directory Managed Identity; User Id=ObjectIdOfManagedIdentity; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString1)) {
    conn.Open();
}

string ConnectionString2 = @"Server=demo.database.windows.net; Authentication=Active Directory MSI; User Id=ObjectIdOfManagedIdentity; Database=testdb";

using (SqlConnection conn = new SqlConnection(ConnectionString2)) {
    conn.Open();
}
```


## <a name="customizing-active-directory-authentication"></a>Personalizar a autenticação do Active Directory

Além de usar a autenticação do Active Directory incorporada ao driver, o **Microsoft.Data.SqlClient** 2.1.0 e posterior fornece aos aplicativos a opção de personalizar a autenticação do Active Directory. A personalização é baseada na classe `ActiveDirectoryAuthenticationProvider`, que é derivada da classe abstrata [`SqlAuthenticationProvider`](/dotnet/api/system.data.sqlclient.sqlauthenticationprovider). 

Durante a autenticação do Active Directory, o aplicativo cliente pode definir sua própria classe `ActiveDirectoryAuthencationProvider` ao:

- Usar um método de retorno de chamada personalizado.
- Passar uma ID do cliente de aplicativo para a biblioteca MSAL por meio do driver SqlClient a fim de buscar tokens de acesso.

O exemplo a seguir mostra como usar um retorno de chamada personalizado quando a autenticação `Active Directory Device Code Flow` está em uso. 

[!code-csharp [AADAuthenticationCustomDeviceFlowCallback#1](~/../sqlclient/doc/samples/AADAuthenticationCustomDeviceFlowCallback.cs#1)]

Com uma classe `ActiveDirectoryAuthenticationProvider` personalizada, uma ID do cliente de aplicativo definida pelo usuário pode ser passada para o SqlClient quando um modo de autenticação do Active Directory com suporte está em uso. Os modos de autenticação do Active Directory com suporte incluem `Active Directory Password`, `Active Directory Integrated`, `Active Directory Interactive`, `Active Directory Service Principal` e `Active Directory Device Code Flow`.

A ID do cliente de aplicativo também é configurável por meio de `SqlAuthenticationProviderConfigurationSection` ou `SqlClientAuthenticationProviderConfigurationSection`. A propriedade de configuração `applicationClientId` aplica-se ao .NET Framework 4.6+ e ao .NET Core 2.1+.

O snippet de código a seguir é um exemplo de uso de uma classe `ActiveDirectoryAuthenticationProvider` personalizada com uma ID do cliente de aplicativo definida pelo usuário quando a autenticação `Active Directory Interactive` está em uso.

[!code-csharp [ApplicationClientIdAzureAuthenticationProvider#1](~/../sqlclient/doc/samples/ApplicationClientIdAzureAuthenticationProvider.cs#1)]

O exemplo a seguir mostra como definir uma ID do cliente de aplicativo por meio de uma seção de configuração.

```xml
<configuration>
  <configSections>
    <section name="SqlClientAuthenticationProviders"
             type="Microsoft.Data.SqlClient.SqlClientAuthenticationProviderConfigurationSection, Microsoft.Data.SqlClient" />
  </configSections>
  <SqlClientAuthenticationProviders applicationClientId ="<GUID>" />
</configuration>

<!--or-->

<configuration>
  <configSections>
    <section name="SqlAuthenticationProviders"
             type="Microsoft.Data.SqlClient.SqlAuthenticationProviderConfigurationSection, Microsoft.Data.SqlClient" />
  </configSections>
  <SqlAuthenticationProviders applicationClientId ="<GUID>" />
</configuration>
```

## <a name="support-for-a-custom-sql-authentication-provider"></a>Suporte para um provedor de autenticação SQL personalizado

Com mais flexibilidade, o aplicativo cliente também pode usar seu próprio provedor de autenticação do Active Directory em vez de usar a classe `ActiveDirectoryAuthenticationProvider`. O provedor de autenticação personalizado precisa ser uma subclasse de `SqlAuthenticationProvider` com métodos substituídos. 

O exemplo a seguir mostra como usar um novo provedor para a autenticação `Active Directory Device Code Flow`.

[!code-csharp [CustomDeviceCodeFlowAzureAuthenticationProvider#1](~/../sqlclient/doc/samples/CustomDeviceCodeFlowAzureAuthenticationProvider.cs#1)]

Além de melhorar a experiência de autenticação `Active Directory Interactive`, o **Microsoft.Data.SqlClient** 2.1.0 e posterior fornece as seguintes APIs para aplicativos cliente a fim de personalizar as autenticações de fluxo de código de dispositivo e interativa.

```c#
public class ActiveDirectoryAuthenticationProvider
{
    // For .NET Framework targeted applications only
    // Sets a reference to the current System.Windows.Forms.IWin32Window that triggers the browser to be shown. 
    // Used to center the browser pop-up onto this window.
    public void SetIWin32WindowFunc(Func<IWin32Window> iWin32WindowFunc);

    // For .NET Standard targeted applications only
    // Sets a reference to the ViewController (if using Xamarin.iOS), Activity (if using Xamarin.Android) IWin32Window, or IntPtr (if using .NET Framework). 
    // Used for invoking the browser for Active Directory Interactive authentication.
    public void SetParentActivityOrWindowFunc(Func<object> parentActivityOrWindowFunc);

    // For .NET Framework, .NET Core, and .NET Standard targeted applications
    // Sets a callback method that's invoked with a custom web UI instance that will let the user sign in with Azure AD, present consent if needed, and get back the authorization code. 
    // Applicable when working with Active Directory Interactive authentication.
    public void SetAcquireAuthorizationCodeAsyncCallback(Func<Uri, Uri, CancellationToken, Task<Uri>> acquireAuthorizationCodeAsyncCallback);

    // For .NET Framework, .NET Core, and .NET Standard targeted applications
    // Clears cached user tokens from the token provider.
    public static void ClearUserTokenCache();
}
```


## <a name="see-also"></a>Confira também
- [Objetos de entidade de serviço e aplicativo no Azure Active Directory](/azure/active-directory/develop/app-objects-and-service-principals)
- [Fluxos de autenticação](/azure/active-directory/develop/msal-authentication-flows)
