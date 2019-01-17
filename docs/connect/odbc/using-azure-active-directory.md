---
title: Usando o Azure Active Directory com o Driver ODBC | Documentos do Microsoft para SQL Server
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
manager: craigg
ms.openlocfilehash: 98f7e0ac3667bc8546a7bf7ce2d8036341bb2650
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206595"
---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>Como usar o Azure Active Directory com o Driver ODBC
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>Finalidade

O Microsoft ODBC Driver for SQL Server com a versão 13.1 ou superior permite que os aplicativos ODBC para se conectar a uma instância do SQL Azure usando uma identidade federada no Azure Active Directory com um nome de usuário/senha, um token de acesso do Azure Active Directory ou Windows Autenticação integrada (_somente o driver do Windows_). Para o Driver ODBC versão 13.1, o acesso do Active Directory do Azure é a autenticação de token _apenas Windows_. O Driver ODBC versão 17 e acima suportam essa autenticação em todas as plataformas (Windows, Linux e Mac). Uma nova autenticação interativa do Active Directory do Azure com a ID de logon é introduzida no Driver ODBC para a versão 17.1 para Windows. Todos esses são realizados com o uso de novo DSN e palavras-chave de cadeia de caracteres de conexão e atributos de conexão.

> [!NOTE]
> O Driver ODBC no Linux e macOS não oferece suporte a serviços de Federação do Active Directory. Se você estiver usando autenticação de nome de usuário e senha do Active Directory de um cliente Linux ou macOS de cliente e configuração do Active Directory inclui serviços de federação, autenticação poderá falhar.

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>DSN de novo e/ou modificado e palavras-chave de cadeia de caracteres de Conexão

O `Authentication` palavra-chave pode ser usado ao conectar-se com uma cadeia de conexão DSN para controlar o modo de autenticação. O valor definido na cadeia de conexão substitui que no DSN, se fornecido. O _valor do atributo previamente_ da `Authentication` configuração é o valor calculado da cadeia de caracteres de conexão e valores DSN.

|Nome|Valores|Padrão|Descrição|
|-|-|-|-|
|`Authentication`|(não definido), (cadeia de caracteres vazia), `SqlPassword`, `ActiveDirectoryPassword`, `ActiveDirectoryIntegrated`, `ActiveDirectoryInteractive`|(não definido)|Controla o modo de autenticação.<table><tr><th>Valor<th>Descrição<tr><td>(não definido)<td>Modo de autenticação determinado por outras palavras-chave (opções de conexão herdado existente).<tr><td>(cadeia de caracteres vazia)<td>Cadeia de Conexão: "{0}" Substituir e desconfigurar um `Authentication` conjunto no DSN de valor.<tr><td>`SqlPassword`<td>Autenticar diretamente a uma instância do SQL Server usando um nome de usuário e senha.<tr><td>`ActiveDirectoryPassword`<td>Autenticar com uma identidade do Active Directory do Azure usando um nome de usuário e senha.<tr><td>`ActiveDirectoryIntegrated`<td>_Somente o driver do Windows_. Autenticar com uma identidade do Active Directory do Azure usando a autenticação integrada.<tr><td>`ActiveDirectoryInteractive`<td>_Somente o driver do Windows_. Autenticar com uma identidade do Active Directory do Azure usando a autenticação interativa.</table>|
|`Encrypt`|(não definido), `Yes`, `No`|(consulte a descrição)|Controla a criptografia de uma conexão. Se o valor do pré-atributo de a `Authentication` configuração não é _none_ na cadeia de conexão ou de DSN, o padrão é `Yes`. Caso contrário, o padrão é `No`. Se o atributo `SQL_COPT_SS_AUTHENTICATION` substitui o valor do pré-atributo de `Authentication`explicitamente definir o valor de criptografia no DSN ou cadeia de caracteres de conexão ou atributo de conexão. É o valor do atributo de pré-lançamento de criptografia `Yes` se o valor for definido como `Yes` na cadeia de caracteres de conexão ou DSN.|

## <a name="new-andor-modified-connection-attributes"></a>Atributos de Conexão nova e/ou modificados

O seguinte previamente conectar conexão atributos foram introduzidos ou modificados para dar suporte à autenticação do Active Directory do Azure. Quando um atributo de conexão tem uma cadeia de conexão correspondente ou a palavra-chave DSN e é definido, o atributo de conexão tem precedência.

|attribute|Tipo|Valores|Padrão|Descrição|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_AD_INTERACTIVE`, `SQL_AU_RESET`|(não definido)|Consulte a descrição de `Authentication` acima de palavra-chave. `SQL_AU_NONE` é fornecido para substituir explicitamente um conjunto `Authentication` valor na cadeia de caracteres DSN e/ou a conexão enquanto `SQL_AU_RESET` desativará o atributo se ele foi definido, permitindo que o valor da cadeia de conexão ou de DSN ter precedência.|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|Ponteiro para `ACCESSTOKEN` ou nulo|NULL|Se não for nulo, especifica o Token de acesso do Azure AD para usar. É um erro especificar um token de acesso e também `UID`, `PWD`, `Trusted_Connection`, ou `Authentication` palavras-chave de cadeia de caracteres de conexão ou seus atributos equivalentes. <br> **Observação:** Driver ODBC versão 13.1 só dá suporte a isso em _Windows_.|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(consulte a descrição)|Controla a criptografia de uma conexão. `SQL_EN_OFF` e `SQL_EN_ON` desabilitar e habilitar a criptografia, respectivamente. Se o valor do pré-atributo de a `Authentication` configuração não é _none_ ou `SQL_COPT_SS_ACCESS_TOKEN` estiver definido, e `Encrypt` não foi especificado na cadeia de caracteres de conexão ou DSN, o padrão é `SQL_EN_ON`. Caso contrário, o padrão é `SQL_EN_OFF`. Se o atributo de conexão `SQL_COPT_SS_AUTHENTICATION` é definido como não _none_, defina explicitamente `SQL_COPT_SS_ENCRYPT` para o valor desejado se `Encrypt` não foi especificado na cadeia de conexão ou de DSN. O valor efetivo de controles esse atributo [se a criptografia será usada para a conexão.](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|Não tem suporte com o Azure Active Directory, uma vez que as alterações de senha para entidades de segurança do AAD não podem ser feitas por meio de uma conexão ODBC. <br><br>A expiração de senha para Autenticação do SQL Server foi introduzida no SQL Server 2005. O `SQL_COPT_SS_OLDPWD` atributo foi adicionado para permitir que o cliente fornecer a antiga e a nova senha para a conexão. Quando essa propriedade estiver definida, o provedor não usará o pool de conexões na primeira conexão nem nas conexões seguintes, já que a cadeia de conexão conterá a "senha antiga", que agora foi alterada.|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|_Preterido_; use `SQL_COPT_SS_AUTHENTICATION` definido como `SQL_AU_AD_INTEGRATED` em vez disso. <br><br>Use força da autenticação do Windows (Kerberos no Linux e macOS) para validação de acesso no logon do servidor. Quando a autenticação do Windows é usada, o driver ignora os valores de identificador e a senha de usuário fornecidos como parte do `SQLConnect`, `SQLDriverConnect`, ou `SQLBrowseConnect` de processamento.|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Adições de interface do usuário do Azure Active Directory (driver do Windows somente)

A instalação de DSN e interfaces do usuário da conexão do driver foram aprimorados com as opções adicionais necessárias para usar a autenticação com o Azure AD.

### <a name="creating-and-editing-dsns-in-the-ui"></a>Criando e editando DSNs na interface do usuário

É possível usar o novo Azure AD autenticação opções ao criar ou editar um DSN existente usando a instalação do driver da interface do usuário:

Autenticação integrada do `Authentication=ActiveDirectoryIntegrated` para Azure Active Directory para SQL Azure

![CreateNewDSN_ADIntegrated.png](windows/CreateNewDSN_ADIntegrated.png)

`Authentication=ActiveDirectoryPassword` para autenticação de nome de usuário e senha do Active Directory do Azure para SQL Azure

![CreateNewDSN_ADPassword.png](windows/CreateNewDSN_ADPassword.png)

Autenticação interativa do `Authentication=ActiveDirectoryInteractive` para Azure Active Directory para SQL Azure

![CreateNewDSN_ADInteractive.png](windows/CreateNewDSN_ADInteractive.png)

`Authentication=SqlPassword` para autenticação de nome de usuário e senha para o SQL Server (do Azure ou não)

![CreateNewDSN_SQLServer.png](windows/CreateNewDSN_SQLServer.png)

`Trusted_Connection=Yes` para Windows SSPI herdado autenticação integrada

![CreateNewDSN_winSSPI.png](windows/CreateNewDSN_winSSPI.png)

As cinco opções correspondem às `Trusted_Connection=Yes` (existente herdado Windows SSPI somente autenticação integrada) e `Authentication=` `ActiveDirectoryIntegrated`, `SqlPassword`, `ActiveDirectoryPassword`, e `ActiveDirectoryInteractive`, respectivamente.

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>Prompt de SQLDriverConnect (driver do Windows somente)

A caixa de diálogo prompt exibida pelo SQLDriverConnect quando ele solicita as informações necessárias para concluir a conexão contém três novas opções de autenticação do Azure AD:

![ServerLogin.png](windows/ServerLogin.png)

Essas opções correspondem aos mesmos cinco disponíveis na configuração do DSN acima de interface do usuário.

### <a name="example-connection-strings"></a>Cadeias de conexão de exemplo
1. Autenticação do SQL Server - sintaxe herdada. Certificado do servidor não for validado, e a criptografia é usada somente se o servidor de aplicá-la. O nome de usuário e a senha é passada na cadeia de conexão.
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. Autenticação do SQL - nova sintaxe. O cliente solicita criptografia (o valor padrão de `Encrypt` está `true`) e o certificado do servidor obtém validado, independentemente da configuração de criptografia (a menos que `TrustServerCertificate` é definido como `true`). O nome de usuário e a senha é passada na cadeia de conexão.
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. Autenticação do Windows (Kerberos no Linux e macOS) integrada usando o SSPI (para SQL Server ou SQL IaaS) - sintaxe atual. Certificado do servidor não for validado, a menos que a criptografia é usada. 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Somente o driver do Windows_.) Autenticação do Windows integrada usando o SSPI (se o banco de dados de destino estiver no SQL Server ou SQL IaaS) - nova sintaxe. O cliente solicita criptografia (o valor padrão de `Encrypt` está `true`) e o certificado do servidor obtém validado, independentemente da configuração de criptografia (a menos que `TrustServerCertificate` é definido como `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. Autenticação de nome de usuário e senha do AAD (se o banco de dados de destino está no BD SQL do Azure). Obtém Validar certificado do servidor, independentemente da configuração de criptografia (a menos que `TrustServerCertificate` é definido como `true`). O nome de usuário e a senha é passada na cadeia de conexão. 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Somente o driver do Windows_.) Autenticação integrada do Windows usando a ADAL, que envolve a resgatar credenciais de conta do Windows para um token de acesso emitidos pelo AAD, supondo que o banco de dados de destino está no banco de dados SQL. Obtém Validar certificado do servidor, independentemente da configuração de criptografia (a menos que `TrustServerCertificate` é definido como `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
7. (_Somente o driver do Windows_.) Autenticação interativa do AAD usa a tecnologia de autenticação multifator do Azure para configurar a conexão. Nesse modo, fornecendo a ID de logon, uma caixa de diálogo de autenticação do Windows Azure é disparada e permite que o usuário insira a senha para concluir a conexão. O nome de usuário é passado na cadeia de conexão.
`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

![WindowsAzureAuth.png](windows/WindowsAzureAuth.png)

> [!NOTE] 
>- Ao usar as novas opções do Active Directory com o driver ODBC do Windows, certifique-se de que o [Active Directory Authentication Library para SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072) foi instalado. Ao usar os drivers de Linux e macOS, certifique-se de que `libcurl` foi instalado. Para a versão de driver 17.2 e posterior, isso não é uma dependência explícita, pois ele não é necessário para outros métodos de autenticação ou operações de ODBC.
>- Para se conectar usando uma senha e o nome da conta do SQL Server, você pode agora usar o novo `SqlPassword` opção, o que é recomendada especialmente para o SQL Azure, pois essa opção permite que os padrões de conexão mais seguros.
>- Para se conectar usando um nome da conta do Azure Active Directory e a senha, especifique `Authentication=ActiveDirectoryPassword` na cadeia de conexão e o `UID` e `PWD` palavras-chave com o nome de usuário e senha, respectivamente.
>- Para se conectar usando a autenticação integrada do Active Directory (driver do Windows somente) ou integrada do Windows, especifique `Authentication=ActiveDirectoryIntegrated` na cadeia de conexão. O driver escolherá o modo de autenticação correto automaticamente. `UID` e `PWD` não deve ser especificado.
>- Para conectar-se usando a autenticação do Active Directory Interactive (driver do Windows somente), `UID` deve ser especificado.

## <a name="authenticating-with-an-access-token"></a>Autenticando com um Token de acesso

O `SQL_COPT_SS_ACCESS_TOKEN` atributo da conexão permite o uso de um token de acesso obtido no Azure AD para autenticação em vez do nome de usuário e senha e também ignora a negociação e obtenção de um token de acesso pelo driver. Para usar um token de acesso, defina as `SQL_COPT_SS_ACCESS_TOKEN` atributo de conexão para um ponteiro para um `ACCESSTOKEN` estrutura:

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

O `ACCESSTOKEN` é uma estrutura de comprimento variável que consiste em 4 bytes _comprimento_ seguido por _comprimento_ bytes de dados opaco que formam o token de acesso. Devido a como o SQL Server lida com tokens de acesso, obtido por meio de um [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) resposta JSON deve ser expandida para que cada byte é seguido por um 0 byte, semelhante a uma cadeia de caracteres de UCS-2 que contém apenas caracteres ASCII de preenchimento; no entanto, o token é um valor opaco e o comprimento especificado, em bytes, não devem incluir qualquer terminador nulo. Por causa de suas restrições de comprimento e formato considerável, esse método de autenticação só está disponível por meio de programação por meio de `SQL_COPT_SS_ACCESS_TOKEN` atributo de conexão; nenhum DSN correspondente ou a palavra-chave de cadeia de caracteres de conexão. A cadeia de caracteres de conexão não deve conter `UID`, `PWD`, `Authentication`, ou `Trusted_Connection` palavras-chave.

> [!NOTE]
> O Driver ODBC versão 13.1 só dá suporte a essa autenticação em _Windows_.

## <a name="azure-active-directory-authentication-sample-code"></a>Código de exemplo de autenticação do Azure Active Directory

O exemplo a seguir mostra o código necessário para se conectar ao SQL Server usando o Azure Active Directory com palavras-chave de conexão. Observe que não há necessidade de alterar o código do aplicativo em si; a cadeia de caracteres de conexão ou DSN se um for usado, é a única modificação necessária para usar o AAD para autenticação:
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
O exemplo a seguir mostra o código necessário para se conectar ao SQL Server usando o Azure Active Directory com autenticação de token de acesso. Nesse caso, é necessário modificar o código do aplicativo para processar o token de acesso e definir o atributo de conexão associado.
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
A seguir está um exemplo de cadeia de conexão para uso com autenticação interativa do Azure Active Directory. Observe que ele não contém o campo PWD como a senha deve ser inserida usando a tela de autenticação do Windows Azure.
~~~
SQLCHAR connString[] = "Driver={ODBC Driver 17 for SQL Server};Server={server};UID=myuser;Authentication=ActiveDirectoryInteractive"
~~~

## <a name="see-also"></a>Consulte Também
[Suporte à autenticação baseada em token para BD SQL do Azure usando a autenticação do AD do Azure](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)

