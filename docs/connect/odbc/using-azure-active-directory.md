---
title: Usando Azure Active Directory com o driver ODBC | Microsoft Docs para SQL Server
ms.custom: ''
ms.date: 11/08/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0f9d73dace4e17d87e1c93da703786fc920b2fb
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176163"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>Como usar o Azure Active Directory com o Driver ODBC
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>Finalidade

O Microsoft ODBC Driver for SQL Server com a versão 13,1 ou superior permite que os aplicativos ODBC se conectem a uma instância do SQL Azure usando uma identidade federada no Azure Active Directory com um nome de usuário/senha, um token de acesso de Azure Active Directory, um Azure active Identidade de serviço gerenciado de diretório ou autenticação integrada do Windows (_somente driver do Windows_). Para o driver ODBC versão 13,1, a autenticação de token de acesso Azure Active Directory é _somente Windows_. O driver ODBC versão 17 e superior dá suporte a essa autenticação em todas as plataformas (Windows, Linux e Mac). Uma nova Azure Active Directory autenticação interativa com a ID de logon é introduzida no driver ODBC versão 17,1 para Windows. Um novo método de autenticação de identidade de serviço gerenciado Azure Active Directory foi adicionado no driver ODBC versão 17.3.1.1 para identidades atribuídas pelo sistema e pelo usuário. Todos eles são realizados por meio do uso de novas palavras-chave de cadeia de conexão e DSN, e atributos de conexão.

> [!NOTE]
> O driver ODBC no Linux e no macOS não oferece suporte a Serviços de Federação do Active Directory (AD FS). Se você estiver usando Azure Active Directory autenticação de nome de usuário/senha de um cliente Linux ou macOS e sua configuração de Active Directory incluir serviços federados, a autenticação poderá falhar.

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>Palavras-chave de DSN e de cadeia de conexão novas e/ou modificadas

A `Authentication` palavra-chave pode ser usada ao se conectar com um DSN ou uma cadeia de conexão para controlar o modo de autenticação. O valor definido na cadeia de conexão substitui isso no DSN, se fornecido. O _valor de pré-atributo_ da `Authentication` configuração é o valor calculado a partir da cadeia de conexão e dos valores de DSN.

|Nome|Valores|Padrão|Descrição|
|-|-|-|-|
|`Authentication`|(não definido), (cadeia de caracteres vazia `SqlPassword`) `ActiveDirectoryPassword`, `ActiveDirectoryIntegrated` `ActiveDirectoryInteractive`,,,,`ActiveDirectoryMsi` |(não definido)|Controla o modo de autenticação.<table><tr><th>Valor<th>Descrição<tr><td>(não definido)<td>Modo de autenticação determinado por outras palavras-chave (opções de conexão herdadas existentes).<tr><td>(cadeia de caracteres vazia)<td>Ajuda de Cadeia de Conexão Substitua e desmarque `Authentication` um valor definido no DSN.<tr><td>`SqlPassword`<td>Autentique diretamente em uma instância de SQL Server usando um nome de usuário e senha.<tr><td>`ActiveDirectoryPassword`<td>Autentique com uma identidade de Azure Active Directory usando um nome de usuário e senha.<tr><td>`ActiveDirectoryIntegrated`<td>_Somente driver do Windows_. Autentique com uma identidade de Azure Active Directory usando a autenticação integrada.<tr><td>`ActiveDirectoryInteractive`<td>_Somente driver do Windows_. Autentique com uma identidade de Azure Active Directory usando a autenticação interativa.<tr><td>`ActiveDirectoryMsi`<td>Autentique com a identidade do Azure Active Directory usando a autenticação de identidade de serviço gerenciada. Para identidade atribuída pelo usuário, o UID é definido como a ID de objeto da identidade do usuário.</table>|
|`Encrypt`|(não definido), `Yes`, `No`|(consulte a descrição)|Controla a criptografia de uma conexão. Se o valor de pré-atributo da `Authentication` configuração não for _nenhum_ no DSN ou na cadeia de conexão, o padrão `Yes`será. Caso contrário, o padrão é `No`. Se o atributo `SQL_COPT_SS_AUTHENTICATION` substituir o valor de pré-atributo `Authentication`de, defina explicitamente o valor de criptografia no DSN ou na cadeia de conexão ou no atributo de conexão. O valor de pré-atributo de criptografia `Yes` é se o valor for definido `Yes` como no DSN ou na cadeia de conexão.|

## <a name="new-andor-modified-connection-attributes"></a>Atributos de conexão novos e/ou modificados

Os seguintes atributos de conexão precedente à conexão foram introduzidos ou modificados para dar suporte à autenticação Azure Active Directory. Quando um atributo de conexão tem uma cadeia de conexão ou palavra-chave DSN correspondente e é definido, o atributo de conexão tem precedência.

|attribute|Tipo|Valores|Padrão|Descrição|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_AD_INTERACTIVE`, `SQL_AU_AD_MSI`, `SQL_AU_RESET`|(não definido)|Consulte a descrição `Authentication` da palavra-chave acima. `SQL_AU_NONE`é fornecido para substituir explicitamente um valor definido `Authentication` no DSN e/ou na cadeia de conexão, enquanto `SQL_AU_RESET` o não define o atributo se ele foi definido, permitindo que o DSN ou o valor da cadeia de conexão tenha precedência.|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|Ponteiro para `ACCESSTOKEN` ou nulo|NULL|Se não for NULL, especifica o token de acesso AzureAD a ser usado. É um erro especificar um token `UID`de acesso `Trusted_Connection`, `PWD` `Authentication` bem como palavras-chave de cadeia de conexão, ou seus atributos equivalentes. <br> **Observação:** O driver ODBC versão 13,1 dá suporte apenas para isso no _Windows_.|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(consulte a descrição)|Controla a criptografia de uma conexão. `SQL_EN_OFF`e `SQL_EN_ON` desabilite e habilite a criptografia, respectivamente. Se o valor de `Authentication` preattribute da configuração não for _None_ ou `SQL_COPT_SS_ACCESS_TOKEN` for definido, e `Encrypt` não tiver sido especificado no DSN ou na cadeia de conexão, o padrão será `SQL_EN_ON`. Caso contrário, o padrão é `SQL_EN_OFF`. Se o atributo `SQL_COPT_SS_AUTHENTICATION` de conexão for definido como não _nenhum_, defina `SQL_COPT_SS_ENCRYPT` explicitamente como o valor desejado se `Encrypt` não tiver sido especificado no DSN ou na cadeia de conexão. O valor efetivo desse atributo controla [se a criptografia será usada para a conexão.](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|Não há suporte com Azure Active Directory, já que as alterações de senha para entidades de segurança do AAD não podem ser realizadas por meio de uma conexão ODBC. <br><br>A expiração de senha para Autenticação do SQL Server foi introduzida no SQL Server 2005. O `SQL_COPT_SS_OLDPWD` atributo foi adicionado para permitir que o cliente forneça a senha antiga e a nova para a conexão. Quando essa propriedade estiver definida, o provedor não usará o pool de conexões na primeira conexão nem nas conexões seguintes, já que a cadeia de conexão conterá a "senha antiga", que agora foi alterada.|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|_Preterido_; Use `SQL_COPT_SS_AUTHENTICATION` definir como `SQL_AU_AD_INTEGRATED` em vez disso. <br><br>Força o uso da autenticação do Windows (Kerberos no Linux e macOS) para validação de acesso no logon do servidor. Quando a autenticação do Windows é usada, o driver ignora os valores de identificador de usuário e senha `SQLConnect`fornecidos `SQLDriverConnect`como parte `SQLBrowseConnect` do processamento, ou.|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Adições de interface do usuário para Azure Active Directory (somente driver do Windows)

As interfaces de configuração do DSN e de conexão do driver foram aprimoradas com as opções adicionais necessárias para usar a autenticação com o Azure AD.

### <a name="creating-and-editing-dsns-in-the-ui"></a>Criando e editando DSNs na interface do usuário

É possível usar as novas opções de autenticação do Azure AD ao criar ou editar um DSN existente usando a interface do usuário da instalação do driver:

Autenticação integrada do `Authentication=ActiveDirectoryIntegrated` para Azure Active Directory para SQL Azure

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword`para Azure Active Directory autenticação de nome de usuário/senha para SQL Azure

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

Autenticação interativa do `Authentication=ActiveDirectoryInteractive` para Azure Active Directory para SQL Azure

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword`para autenticação de nome de usuário/senha para SQL Server (Azure ou não)

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes`para autenticação integrada de SSPI do Windows herdado

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

As cinco opções correspondem a `Trusted_Connection=Yes` (autenticação integrada somente SSPI do Windows herdada existente) `Authentication=` e `SqlPassword` `ActiveDirectoryIntegrated`, `ActiveDirectoryPassword`,, `ActiveDirectoryInteractive`e, respectivamente.

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>SQLDriverConnect prompt (somente driver do Windows)

A caixa de diálogo de prompt exibida por SQLDriverConnect quando solicita as informações necessárias para concluir a conexão contém três novas opções para a autenticação do Azure AD:

![ServerLogin.png](windows/ServerLogin.png)

Essas opções correspondem aos mesmos cinco disponíveis na interface do usuário da instalação do DSN acima.

### <a name="example-connection-strings"></a>Cadeias de conexão de exemplo
1. Autenticação SQL Server-sintaxe herdada. O certificado do servidor não é validado e a criptografia é usada somente se o servidor o impõe. O nome de usuário/senha é passado na cadeia de conexão.
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. Autenticação do SQL – nova sintaxe. O cliente solicita criptografia (o valor padrão de `Encrypt` é `true`) e o certificado do servidor é validado, independentemente da configuração de criptografia `TrustServerCertificate` (a menos `true`que seja definido como). O nome de usuário/senha é passado na cadeia de conexão.
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. Autenticação integrada do Windows (Kerberos no Linux e macOS) usando a sintaxe SSPI (para SQL Server ou SQL IaaS)-atual. O certificado do servidor não é validado, a menos que a criptografia seja usada. 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Somente driver do Windows_.) Autenticação integrada do Windows usando SSPI (se o banco de dados de destino estiver em SQL Server ou SQL IaaS)-nova sintaxe. O cliente solicita criptografia (o valor padrão de `Encrypt` é `true`) e o certificado do servidor é validado, independentemente da configuração de criptografia `TrustServerCertificate` (a menos `true`que seja definido como). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. Autenticação de nome de usuário/senha do AAD (se o banco de dados de destino estiver no BD SQL do Azure). O certificado do servidor é validado, independentemente da configuração de `TrustServerCertificate` criptografia (a `true`menos que seja definido como). O nome de usuário/senha é passado na cadeia de conexão. 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Somente driver do Windows_.) Autenticação integrada do Windows usando a ADAL, que envolve a eliminação de credenciais de conta do Windows para um token de acesso emitido pelo AAD, supondo que o banco de dados de destino esteja no banco de dados SQL do Azure. O certificado do servidor é validado, independentemente da configuração de `TrustServerCertificate` criptografia (a `true`menos que seja definido como). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_Somente driver do Windows_.) A autenticação interativa do AAD usa a tecnologia de autenticação multifator do Azure para configurar a conexão. Nesse modo, ao fornecer a ID de logon, uma caixa de diálogo de autenticação do Azure é disparada e permite que o usuário insira a senha para concluir a conexão. O nome de usuário é passado na cadeia de conexão.
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

8. A autenticação de Identidade de Serviço Gerenciada do AAD usa a identidade atribuída pelo usuário ou para autenticação para configurar a conexão. Para identidade atribuída pelo usuário, o UID é definido como a ID de objeto da identidade do usuário.<br>
Para identidade atribuída pelo sistema,<br>
`server=Server;database=Database;Authentication=ActiveDirectoryMsi;`<br>
Para identidade atribuída pelo usuário com a ID de objeto igual a myobjectid,<br>
`server=Server;database=Database;UID=myObjectId;Authentication=ActiveDirectoryMsi;`

> [!NOTE] 
>- Ao usar as novas opções de Active Directory com o driver ODBC do Windows, verifique se o [biblioteca de autenticação do Active Directory para SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072) foi instalado. Ao usar os drivers Linux e MacOS, verifique se `libcurl` o foi instalado. Para o driver versão 17,2 e posterior, essa não é uma dependência explícita, pois não é necessária para os outros métodos de autenticação ou operações ODBC.
>- Para se conectar usando um nome de usuário e senha da conta de SQL Server, você `SqlPassword` pode usar a nova opção, que é recomendada especialmente para SQL Azure, já que essa opção permite padrões de conexão mais seguros.
>- Para se conectar usando uma conta de Azure Active Directory nome de usuário `Authentication=ActiveDirectoryPassword` e senha, especifique na cadeia `UID` de `PWD` conexão e as palavras-chave com o nome de usuário e a senha, respectivamente.
>- Para se conectar usando a autenticação integrada do Windows ou Active Directory integrada (somente driver do `Authentication=ActiveDirectoryIntegrated` Windows), especifique na cadeia de conexão. O driver escolherá o modo de autenticação correto automaticamente. `UID`e `PWD` não deve ser especificado.
>- Para se conectar usando a autenticação do Active Directory Interactive (somente driver `UID` do Windows), é necessário especificar.

## <a name="authenticating-with-an-access-token"></a>Autenticando com um token de acesso

O `SQL_COPT_SS_ACCESS_TOKEN` atributo pre-Connection permite o uso de um token de acesso obtido do Azure ad para autenticação em vez de nome de usuário e senha e também ignora a negociação e a obtenção de um token de acesso pelo driver. Para usar um token de acesso, defina `SQL_COPT_SS_ACCESS_TOKEN` o atributo de conexão como um ponteiro `ACCESSTOKEN` para uma estrutura:

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

O `ACCESSTOKEN` é uma estrutura de comprimento variável que consiste em um _comprimento_ de 4 bytes seguido por bytes de _comprimento_ de dados opacos que formam o token de acesso. Devido ao modo como SQL Server trata os tokens de acesso, um obtido por meio de uma resposta JSON do [OAuth 2,0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) deve ser expandido para que cada byte seja seguido por um byte de preenchimento 0, semelhante a uma cadeia de caracteres UCS-2 contendo apenas caracteres ASCII; no entanto, o token é um valor opaco e o comprimento especificado, em bytes, não deve incluir nenhum terminador nulo. Devido a suas restrições de comprimento e formato consideráveis, esse método de autenticação só está disponível programaticamente por meio do atributo de `SQL_COPT_SS_ACCESS_TOKEN` conexão; não há nenhuma palavra-chave de cadeia de conexão ou DSN correspondente. A cadeia de conexão não deve `UID`conter `PWD`, `Authentication`, ou `Trusted_Connection` palavras-chave.

> [!NOTE]
> O driver ODBC versão 13,1 dá suporte apenas a essa autenticação no _Windows_.

## <a name="azure-active-directory-authentication-sample-code"></a>Código de exemplo de autenticação do Azure Active Directory

O exemplo a seguir mostra o código necessário para se conectar a SQL Server usando Azure Active Directory com palavras-chave de conexão. Observe que não há necessidade de alterar o próprio código do aplicativo; a cadeia de conexão, ou DSN, se for usada, é a única modificação necessária para usar o AAD para autenticação:
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
O exemplo a seguir mostra o código necessário para se conectar ao SQL Server usando Azure Active Directory com autenticação de token de acesso. Nesse caso, é necessário modificar o código do aplicativo para processar o token de acesso e definir o atributo de conexão associado.
~~~
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server}"
    SQLCHAR accessToken[] = "eyJ0eXAiOi..."; // In the format extracted from an OAuth JSON response
    ...
    DWORD dataSize = 2 * strlen(accessToken);
    ACCESSTOKEN *pAccToken = malloc(sizeof(ACCESSTOKEN) + dataSize);
    pAccToken->dataSize = dataSize;
    // Expand access token with padding bytes
    for(int i = 0, j = 0; i < dataSize; i += 2, j++) {
        pAccToken->data[i] = accessToken[j];
        pAccToken->data[i+1] = 0;
    }
    ...
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_ACCESS_TOKEN, (SQLPOINTER)pAccToken, SQL_IS_POINTER);
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);      
    ...
    free(pAccToken);
~~~
Veja a seguir um exemplo de cadeia de conexão para uso com Azure Active Directory autenticação interativa. Observe que ele não contém o campo PWD, pois a senha seria inserida usando a tela de autenticação do Azure.
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~
Veja a seguir um exemplo de cadeia de conexão para uso com Azure Active Directory Identidade de Serviço Gerenciada autenticação. Observe que o UID é definido como a ID de objeto da identidade do usuário para a identidade atribuída pelo usuário.
~~~
// For system-assigned identity,
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};Authentication=ActiveDirectoryMsi"
...
// For user-assigned identity with object ID equals to myObjectId
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myObjectId;Authentication=ActiveDirectoryMsi"
~~~

## <a name="see-also"></a>Consulte Também
[Suporte à autenticação baseada em token para o BD SQL do Azure usando a autenticação do Azure AD](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

