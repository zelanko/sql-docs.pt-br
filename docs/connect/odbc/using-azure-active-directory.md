---
title: Como usar o Azure Active Directory com o Driver ODBC | Microsoft Docs for SQL Server
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
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "70176163"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>Como usar o Azure Active Directory com o Driver ODBC
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>Finalidade

O Microsoft ODBC Driver for SQL Server, versão 13.1 ou posterior, permite que os aplicativos ODBC se conectem a uma instância do SQL Azure usando uma identidade federada no Azure Active Directory com um nome de usuário/senha, um token de acesso do Azure Active Directory, uma identidade de serviço gerenciado do Azure Active Directory ou a autenticação integrada do Windows (_somente driver do Windows_). No caso do Driver ODBC versão 13.1, a autenticação do token de acesso do Azure Active Directory é _somente Windows_. O Driver ODBC versão 17 e posterior dá suporte a essa autenticação em todas as plataformas (Windows, Linux e Mac). Uma nova autenticação interativa do Azure Active Directory com a ID de logon é introduzida no Driver ODBC versão 17.1 para Windows. Um novo método de autenticação de identidade de serviço gerenciado do Azure Active Directory foi adicionado no Driver ODBC versão 17.3.1.1 para identidades atribuídas pelo sistema e pelo usuário. Todos eles são realizados por meio da utilização de novas palavras-chave de cadeia de conexão e DSN e atributos de conexão.

> [!NOTE]
> O Driver ODBC no Linux e no macOS não dá suporte a Serviços de Federação do Active Directory (AD FS). Se você estiver usando a autenticação de nome de usuário/senha do Azure Active Directory em um cliente Linux ou macOS e sua configuração do Active Directory incluir Serviços Federados, a autenticação poderá falhar.

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>Palavras-chave novas e/ou modificadas da cadeia de conexão e DSN

A palavra-chave `Authentication` pode ser usada ao se conectar com um DSN ou uma cadeia de conexão para controlar o modo de autenticação. O valor definido na cadeia de conexão substitui o valor do DSN, caso ele seja fornecido. O _valor de pré-atributo_ da configuração da `Authentication` é o valor computado a partir dos valores de DSN e da cadeia de conexão.

|Nome|Valores|Padrão|Descrição|
|-|-|-|-|
|`Authentication`|(não definido), (cadeia de caracteres vazia), `SqlPassword`, `ActiveDirectoryPassword`, `ActiveDirectoryIntegrated`, `ActiveDirectoryInteractive`, `ActiveDirectoryMsi` |(não definido)|Controla o modo de autenticação.<table><tr><th>Valor<th>Descrição<tr><td>(não definido)<td>Modo de autenticação determinado por outras palavras-chave (opções de conexão herdadas existentes).<tr><td>(cadeia de caracteres vazia)<td>(Cadeia de conexão apenas.) Substitua e remova a definição de um valor `Authentication` definido no DSN.<tr><td>`SqlPassword`<td>Autentique diretamente em uma instância do SQL Server usando um nome de usuário e senha.<tr><td>`ActiveDirectoryPassword`<td>Autentique com a identidade do Azure Active Directory por meio de um nome de usuário e senha.<tr><td>`ActiveDirectoryIntegrated`<td>_Driver do Windows apenas_. Autentique com a identidade do Azure Active Directory por meio da autenticação integrada.<tr><td>`ActiveDirectoryInteractive`<td>_Driver do Windows apenas_. Autentique com a identidade do Azure Active Directory por meio da autenticação interativa.<tr><td>`ActiveDirectoryMsi`<td>Autentique com a identidade do Azure Active Directory por meio da autenticação de identidade do serviço gerenciado. Para identidade atribuída pelo usuário, o UID é definido como a ID de objeto da identidade do usuário.</table>|
|`Encrypt`|(não definido), `Yes`, `No`|(confira a descrição)|Controla a criptografia de uma conexão. Se o valor de pré-atributo da configuração de `Authentication` não for _nenhum_ no DSN e na cadeia de conexão, o padrão será `Yes`. Caso contrário, o padrão é `No`. Se o atributo `SQL_COPT_SS_AUTHENTICATION` substituir o valor do pré-atributo de `Authentication`, defina explicitamente o valor de Criptografia no DSN ou na cadeia de conexão ou no atributo de conexão. O valor do pré-atributo da Criptografia será `Yes` se o valor estiver definido como `Yes` no DSN ou na cadeia de conexão.|

## <a name="new-andor-modified-connection-attributes"></a>Atributos de conexão novos e/ou modificados

Os seguintes atributos de pré-conexão foram introduzidos ou modificados para dar suporte à autenticação do Azure Active Directory. Quando um atributo de conexão tem uma cadeia de conexão ou palavra-chave do DSN correspondente e está definido, o atributo de conexão tem precedência.

|Atributo|Type|Valores|Padrão|Descrição|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_AD_INTERACTIVE`, `SQL_AU_AD_MSI`, `SQL_AU_RESET`|(não definido)|Confira a descrição da palavra-chave `Authentication` acima. `SQL_AU_NONE` é fornecido para substituir explicitamente um valor `Authentication` definido no DSN e/ou na cadeia de conexão, enquanto `SQL_AU_RESET` cancela a definição do atributo caso ele tenha sido definido, permitindo que o DSN ou o valor da cadeia de conexão tenha precedência.|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|Ponteiro como `ACCESSTOKEN` ou NULL|NULO|Se não for NULL, especificará o token de acesso do AzureAD a ser usado. É um erro especificar um token de acesso além de palavras-chave da cadeia de conexão `UID`, `PWD`, `Trusted_Connection` ou `Authentication` ou seus atributos equivalentes. <br> **OBSERVAÇÃO:** O Driver ODBC versão 13.1 só oferece suporte a isso no _Windows_.|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(confira a descrição)|Controla a criptografia de uma conexão. `SQL_EN_OFF` e `SQL_EN_ON` ativam e desativam a criptografia, respectivamente. Se o valor de pré-atributo da configuração `Authentication` não for _nenhum_, ou `SQL_COPT_SS_ACCESS_TOKEN` estiver definido e `Encrypt` não tiver sido especificado no DSN e na cadeia de conexão, o padrão será `SQL_EN_ON`. Caso contrário, o padrão é `SQL_EN_OFF`. Se o atributo de conexão `SQL_COPT_SS_AUTHENTICATION` estiver definido como não sendo _nenhum_, defina explicitamente `SQL_COPT_SS_ENCRYPT` como o valor desejado se `Encrypt` não tiver sido especificado no DSN ou na cadeia de conexão. O valor efetivo desse atributo controla [se a criptografia será usada para a conexão.](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|Não há suporte no Azure Active Directory já que as alterações de senha para entidades de segurança do AAD não podem ser realizadas por meio de uma conexão ODBC. <br><br>A expiração de senha para Autenticação do SQL Server foi introduzida no SQL Server 2005. O atributo `SQL_COPT_SS_OLDPWD` foi adicionado para permitir que o cliente forneça tanto a senha antiga quanto a nova para a conexão. Quando essa propriedade estiver definida, o provedor não usará o pool de conexões na primeira conexão nem nas conexões seguintes, já que a cadeia de conexão conterá a "senha antiga", que agora foi alterada.|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|_Preterido_; em vez disso, use `SQL_COPT_SS_AUTHENTICATION` definido como `SQL_AU_AD_INTEGRATED`. <br><br>Força o uso da Autenticação do Windows (Kerberos no Linux e macOS) para validação de acesso no logon do servidor. Quando a Autenticação do Windows é usada, o driver ignora os valores do identificador de usuário e da senha fornecidos como parte do processamento de `SQLConnect`, `SQLDriverConnect` ou `SQLBrowseConnect`.|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>As Adições da interface do usuário para o Azure Active Directory (somente driver do Windows)

As interfaces do usuário de configuração e conexão do DSN do driver foram aprimoradas com as opções adicionais necessárias para que a autenticação com o Azure AD possa ser usada.

### <a name="creating-and-editing-dsns-in-the-ui"></a>Criação e edição de DSNs no interface do usuário

É possível usar as novas opções de autenticação do Azure AD quando criar ou editar um DSN existente por meio da interface do usuário da configuração do driver:

Autenticação integrada do `Authentication=ActiveDirectoryIntegrated` para Azure Active Directory para SQL Azure

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

Autenticação de nome de usuário/senha do `Authentication=ActiveDirectoryPassword` para Azure Active Directory para SQL Azure

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

Autenticação interativa do `Authentication=ActiveDirectoryInteractive` para Azure Active Directory para SQL Azure

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword` para autenticação de nome de usuário/senha para SQL Server (Azure ou não)

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes` para autenticação integrada de SSPI herdada do Windows

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

As cinco opções correspondem à `Trusted_Connection=Yes` (autenticação integrada existente somente para SSPI herdada do Windows) e `Authentication=` `ActiveDirectoryIntegrated`, `SqlPassword`, `ActiveDirectoryPassword`e `ActiveDirectoryInteractive`, respectivamente.

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>Prompt do SQLDriverConnect (somente driver do Windows)

A caixa de diálogo de prompt exibida pelo SQLDriverConnect quando ele solicita as informações necessárias para concluir a conexão tem três novas opções para a autenticação do Azure AD:

![ServerLogin.png](windows/ServerLogin.png)

Essas opções correspondem às mesmas cinco opções disponíveis na interface do usuário da configuração do DSN acima.

### <a name="example-connection-strings"></a>Cadeias de conexão de exemplo
1. Autenticação do SQL Server – sintaxe herdada. O certificado do servidor não é validado e a criptografia só será usada se for imposta pelo servidor. O nome de usuário/senha é passado na cadeia de conexão.
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. Autenticação do SQL – nova sintaxe. O cliente solicita criptografia (o valor padrão de `Encrypt` é `true`) e o certificado do servidor é validado, independentemente da configuração da criptografia (a menos que `TrustServerCertificate` esteja definido como `true`). O nome de usuário/senha é passado na cadeia de conexão.
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. Autenticação integrada do Windows (Kerberos no Linux e macOS) por meio da sintaxe SSPI (para SQL Server ou SQL IaaS) – sintaxe atual. O certificado do servidor não é validado, a menos que seja usada a criptografia. 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Driver do Windows apenas_.) Autenticação integrada do Windows por meio de SSPI (se o banco de dados de destino estiver no SQL Server ou SQL IaaS) – nova sintaxe. O cliente solicita criptografia (o valor padrão de `Encrypt` é `true`) e o certificado do servidor é validado, independentemente da configuração da criptografia (a menos que `TrustServerCertificate` esteja definido como `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. Autenticação de nome de usuário/senha do AAD (se o banco de dados de destino estiver no banco de dados do SQL do Azure). O certificado do servidor é validado, independentemente da configuração da criptografia (a menos que `TrustServerCertificate` esteja definido como `true`). O nome de usuário/senha é passado na cadeia de conexão. 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Driver do Windows apenas_.) Autenticação integrada do Windows pela ADAL, que envolve a eliminação de credenciais de conta do Windows para um token de acesso emitido pelo AAD, supondo que o banco de dados de destino esteja no Banco de dados SQL do Azure. O certificado do servidor é validado, independentemente da configuração da criptografia (a menos que `TrustServerCertificate` esteja definido como `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_Driver do Windows apenas_.) A autenticação interativa do AAD usa a tecnologia de autenticação multifator do Azure para configurar a conexão. Nesse modo, ao fornecer a ID de logon, uma caixa de diálogo de autenticação do Azure é acionada para permitir que o usuário insira a senha e conclua a conexão. O nome de usuário é passado na cadeia de conexão.
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

8. A autenticação da Identidade de Serviço Gerenciada do AAD usa a identidade para autenticação atribuída pelo usuário ou pelo sistema para configurar a conexão. Para identidade atribuída pelo usuário, o UID é definido como a ID de objeto da identidade do usuário.<br>
Para identidade atribuída pelo sistema,<br>
`server=Server;database=Database;Authentication=ActiveDirectoryMsi;`<br>
Para a identidade atribuída pelo usuário com a ID de objeto igual a myObjectId,<br>
`server=Server;database=Database;UID=myObjectId;Authentication=ActiveDirectoryMsi;`

> [!NOTE] 
>- Ao usar as novas opções do Active Directory com o Driver ODBC do Windows, verifique se a [Biblioteca de Autenticação do Active Directory para SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072) foi instalada. Quando usar drivers do Linux e macOS, verifique se `libcurl` foi instalado. Para o driver versão 17.2 e posterior, essa não é uma dependência explícita já que não é necessária para os demais métodos de autenticação ou operações ODBC.
>- Para se conectar usando um nome de usuário e senha da conta de SQL Server, você pode usar a nova opção `SqlPassword` que é recomendada especialmente para o SQL Azure já que permite padrões de conexão mais seguros.
>- Para se conectar usando um nome de usuário e senha da conta do Azure Active Directory, especifique `Authentication=ActiveDirectoryPassword` na cadeia de conexão e as palavras-chave `UID` e `PWD` com o nome de usuário e a senha, respectivamente.
>- Para se conectar usando a autenticação integrada do Windows ou do Active Directory (somente driver do Windows), especifique `Authentication=ActiveDirectoryIntegrated` na cadeia de conexão. O driver escolherá o modo de autenticação correto automaticamente. `UID` e `PWD` não devem ser especificados.
>- Para se conectar usando a autenticação interativa do Active Directory (somente driver do Windows), `UID` deve ser especificado.

## <a name="authenticating-with-an-access-token"></a>Autenticação com um token de acesso

O atributo de pré-conexão `SQL_COPT_SS_ACCESS_TOKEN` permite usar um token de acesso obtido do Azure AD para autenticação, em vez do nome de usuário e senha, e também ignora a negociação e a obtenção de um token de acesso pelo driver. Para usar um token de acesso, defina o atributo de conexão `SQL_COPT_SS_ACCESS_TOKEN` como um ponteiro para uma estrutura `ACCESSTOKEN`:

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

O `ACCESSTOKEN` é uma estrutura de comprimento variável formada por um _comprimento_ de 4 bytes seguido pelos bytes de _comprimento_ dos dados opacos que formam o token de acesso. Devido ao modo como SQL Server trata os tokens de acesso, o token obtido por meio de uma resposta JSON do [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) deve ser expandido para que cada byte seja seguido por um byte de preenchimento 0, semelhante a uma cadeia de caracteres UCS-2 contendo apenas caracteres ASCII; no entanto, o token é um valor opaco e o comprimento especificado, em bytes, não deve incluir terminadores nulos. Devido a suas restrições de comprimento e formato consideráveis, esse método de autenticação só está disponível programaticamente por meio do atributo de conexão `SQL_COPT_SS_ACCESS_TOKEN`. Não há palavras-chave correspondentes da cadeia de conexão e do DSN. A cadeia de conexão não deve conter as palavras-chave `UID`, `PWD`, `Authentication` ou `Trusted_Connection`.

> [!NOTE]
> O Driver ODBC versão 13.1 só oferece suporte a essa autenticação no _Windows_.

## <a name="azure-active-directory-authentication-sample-code"></a>Código de exemplo de autenticação do Azure Active Directory

O exemplo a seguir mostra o código necessário para se conectar ao SQL Server por meio do Azure Active Directory com palavras-chave de conexão. Observe que não há necessidade de alterar o próprio código do aplicativo; a cadeia de conexão, ou DSN, se for usada, é a única modificação necessária para usar o AAD na autenticação:
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
O exemplo a seguir mostra o código necessário para se conectar ao SQL Server por meio do Azure Active Directory com a autenticação de token de acesso. Nesse caso, é necessário modificar o código do aplicativo para processar o token de acesso e definir o atributo de conexão associado.
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
Veja a seguir um exemplo de cadeia de conexão para ser usada com a Autenticação interativa do Azure Active Directory. Observe que ela não tem o campo PWD, pois a senha seria inserida usando a tela da Autenticação do Azure.
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~
Veja a seguir um exemplo de cadeia de conexão para ser usada com a Autenticação de identidade do serviço do Azure Active Directory. Observe que o UID é definido como a ID de objeto da identidade do usuário para a identidade atribuída pelo usuário.
~~~
// For system-assigned identity,
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};Authentication=ActiveDirectoryMsi"
...
// For user-assigned identity with object ID equals to myObjectId
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myObjectId;Authentication=ActiveDirectoryMsi"
~~~

## <a name="see-also"></a>Consulte Também
[Suporte para autenticação baseada em token para o Banco de Dados SQL do Azure usando a autenticação do Azure AD](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

