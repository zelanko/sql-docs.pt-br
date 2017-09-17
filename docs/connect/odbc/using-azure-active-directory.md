---
title: Usando o Active Directory do Azure com o Driver ODBC | Microsoft Docs
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 801f0ec683811776b7a249e4984030d3496e5a1e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>Usando o Active Directory do Azure com o Driver ODBC
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>Finalidade

O ODBC Driver 13.1 para SQL Server permite que os aplicativos ODBC para se conectar a uma instância do SQL Azure usando uma identidade federada no Azure Active Directory com uma nome de usuário/senha, um token de acesso do Active Directory do Azure (driver do Windows somente) ou integrada do Windows Autenticação (driver do Windows somente). Isso é feito com o uso de DSN novo e palavras-chave de cadeia de caracteres de conexão e os atributos de conexão.

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>Novo e/ou modificada DSN e palavras-chave de cadeia de caracteres de Conexão

O `Authentication` palavra-chave pode ser usado ao conectar-se com uma cadeia de conexão DSN para controlar o modo de autenticação. O valor definido na cadeia de conexão substituições no DSN, se fornecido. O _pré-valor do atributo_ do `Authentication` configuração é o valor calculado da cadeia de caracteres de conexão e valores DSN.

|Nome|Valores|Default|Description|
|-|-|-|-|
|`Authentication`|(não definido), (cadeia de caracteres vazia), `SqlPassword`, `ActiveDirectoryPassword`,`ActiveDirectoryIntegrated`|(não definido)|Controla o modo de autenticação.<table><tr><th>Valor<th>Description<tr><td>(não definido)<td>Modo de autenticação determinado por outras palavras-chave (opções de conexão herdados existente).<tr><td>(cadeia de caracteres vazia)<td>(Somente para a cadeia de Conexão.) Substituir e desconfigurar um `Authentication` valor definido no DSN.<tr><td>`SqlPassword`<td>Autenticar diretamente em uma instância do SQL Server usando um nome de usuário e senha.<tr><td>`ActiveDirectoryPassword`<td>Autenticar com uma identidade do Active Directory do Azure usando um nome de usuário e senha.<tr><td>`ActiveDirectoryIntegrated`<td>_Somente o driver do Windows_. Autenticar com uma identidade do Active Directory do Azure usando a autenticação integrada.</table>|
|`Encrypt`|(não definido), `Yes`,`No`|(consulte a descrição)|Controla a criptografia de uma conexão. Se o valor do atributo antes do `Authentication` configuração não é _nenhum_, o padrão é `Yes`. Caso contrário, o padrão é `No`. O valor do atributo antes de criptografia é `Yes` se o valor for definido como `Yes` na cadeia de caracteres de conexão ou DSN.|

## <a name="new-andor-modified-connection-attributes"></a>Atributos de Conexão nova e/ou modificado

O seguinte previamente conectar conexão atributos foram introduzidos ou modificados para dar suporte à autenticação do Active Directory do Azure. Quando um atributo de conexão tem uma cadeia de caracteres de conexão correspondente ou a palavra-chave DSN e estiver definido, o atributo de conexão tem precedência.

|Atributo|Tipo|Valores|Default|Description|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_RESET`|(não definido)|Consulte a descrição do `Authentication` palavra-chave acima. `SQL_AU_NONE`é fornecido para substituir explicitamente um conjunto `Authentication` valor na cadeia de DSN e/ou a conexão enquanto `SQL_AU_RESET` desativa o atributo se ele foi definido, permitindo que o valor de cadeia de caracteres DSN ou conexão precedência.|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|Ponteiro para `ACCESSTOKEN` ou nulo|NULL|_Somente o driver do Windows_. Se não nulo, especifica o Token de acesso doWindows Azure para usar. É um erro para especificar um token de acesso e também `UID`, `PWD`, `Trusted_Connection`, ou `Authentication` palavras-chave de cadeia de caracteres de conexão ou seus atributos equivalentes.|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(consulte a descrição)|Controla a criptografia de uma conexão. `SQL_EN_OFF`e `SQL_EN_ON` desabilitar e habilitar a criptografia, respectivamente. Se o valor do atributo antes do `Authentication` configuração não é _nenhum_ ou `SQL_COPT_SS_ACCESS_TOKEN` for definida, e `Encrypt` não foi especificado na cadeia de caracteres de conexão ou DSN, o padrão é `SQL_EN_ON`. Caso contrário, o padrão é `SQL_EN_OFF`. O valor efetivo de controles esse atributo [se a criptografia será usada para a conexão.](https://docs.microsoft.com/en-us/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|Não compatível com o Active Directory do Azure, desde que as alterações de senha para entidades de segurança do AAD não podem ser realizadas por meio de uma conexão ODBC. <br><br>Expiração de senha para autenticação do SQL Server foi introduzida no SQL Server 2005. O `SQL_COPT_SS_OLDPWD` atributo foi adicionado para permitir que o cliente fornecer a antiga e a nova senha para a conexão. Quando essa propriedade estiver definida, o provedor não usará o pool de conexões na primeira conexão nem nas conexões seguintes, já que a cadeia de conexão conterá a "senha antiga", que agora foi alterada.|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|_Preterido_; use `SQL_COPT_SS_AUTHENTICATION` definida como `SQL_AU_AD_INTEGRATED` em vez disso. <br><br>Força usa da autenticação do Windows (Kerberos em Linux e macOS) para validação de acesso no logon de servidor. Quando a autenticação do Windows é usada, o driver ignora os valores de identificador e a senha de usuário fornecidos como parte do `SQLConnect`, `SQLDriverConnect`, ou `SQLBrowseConnect` de processamento.|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>Adições de interface do usuário do Azure Active Directory (driver do Windows somente)

A configuração DSN e interfaces do usuário da conexão do driver foram aprimorados com as opções adicionais necessárias para usar a autenticação com o Azure AD.

### <a name="creating-and-editing-dsns-in-the-ui"></a>Criando e editando DSNs na interface de usuário

É possível usar o novo AD do Azure autenticação opções ao criar ou editar um DSN existente usando a instalação do driver da interface do usuário:

`Authentication=ActiveDirectoryIntegrated`para a autenticação integrada do Active Directory do Azure para o SQL Azure

![CreateNewDSN3.png](windows/CreateNewDSN3.png)

`Authentication=ActiveDirectoryPassword`para autenticação de nome de usuário e senha do Active Directory do Azure para o SQL Azure

![CreateNewDSN4.png](windows/CreateNewDSN4.png)

`Authentication=SqlPassword`para autenticação de nome de usuário e senha para o SQL Server (do Azure ou não)

![CreateNewDSN.png](windows/CreateNewDSN.png)

`Trusted_Connection=Yes`para Windows SSPI herdado autenticação integrada

![CreateNewDSN2.png](windows/CreateNewDSN2.png)

As quatro opções correspondem às `Trusted_Connection=Yes` (existentes herdadas do Windows somente SSPI a autenticação integrada) e `Authentication=` `ActiveDirectoryIntegrated`, `SqlPassword`, e `ActiveDirectoryPassword`, respectivamente.

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>Prompt de SQLDriverConnect (driver do Windows somente)

A caixa de diálogo prompt exibida pelo SQLDriverConnect quando ele solicita as informações necessárias para concluir a conexão contém duas novas opções de autenticação do AD do Azure:

![SQLServerLogin.png](windows/SQLServerLogin.png)

Essas opções correspondem aos quatro mesmo disponível na interface de usuário acima de configuração do DSN.

### <a name="example-connection-strings"></a>Cadeias de conexão de exemplo
1. Autenticação do SQL Server – sintaxe herdada. Certificado do servidor não for validado, e a criptografia é usada somente se o servidor aplica. A nome de usuário/senha é passada na cadeia de conexão.
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. Autenticação do SQL – nova sintaxe. O cliente solicita criptografia (o valor padrão de `Encrypt` é `true`) e o certificado do servidor é validada, independentemente da configuração de criptografia (a menos que `TrustServerCertificate` é definido como `true`). A nome de usuário/senha é passada na cadeia de conexão.
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. Autenticação integrada do Windows (Kerberos em Linux e macOS) usando SSPI (para SQL Server ou SQL IaaS) – sintaxe atual. Certificado do servidor não for validado, a menos que a criptografia é usada. 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Somente o driver do Windows_.) Autenticação integrada do Windows usando o SSPI (se o banco de dados de destino estiver no SQL Server ou SQL IaaS) – nova sintaxe. O cliente solicita criptografia (o valor padrão de `Encrypt` é `true`) e o certificado do servidor é validada, independentemente da configuração de criptografia (a menos que `TrustServerCertificate` é definido como `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. Autenticação de nome de usuário e senha do AAD (se o banco de dados de destino está no banco de dados de SQL Azure). Certificado do servidor for validado, independentemente da configuração de criptografia (a menos que `TrustServerCertificate` é definido como `true`). A nome de usuário/senha é passada na cadeia de conexão. 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Somente o driver do Windows_.) Autenticação integrada do Windows usando a ADAL, que envolve como credenciais de conta do Windows para um token de acesso emitido AAD, supondo que o banco de dados de destino está no banco de dados do SQL Azure. Certificado do servidor for validado, independentemente da configuração de criptografia (a menos que `TrustServerCertificate` é definido como `true`). 
`server=Server;database=Database; Authentication=ActiveDirectoryIntegrated;`

> [!NOTE] 
>- Ao usar as novas opções do Active Directory com o driver ODBC do Windows, certifique-se de que o [Active Directory Authentication Library para SQL Server](http://go.microsoft.com/fwlink/?LinkID=513072) foi instalado. Os drivers de Linux e macOS não exigem dependências adicionais para autenticar com o Active Directory do Azure.
>- Para se conectar usando uma senha e o nome da conta do SQL Server, você agora pode usar o novo `SqlPassword` opção, que é recomendada principalmente para SQL Azure desde que esta opção permite que os padrões de conexão mais seguros.
>- Para se conectar usando uma senha e o nome da conta do Active Directory do Azure, especifique `Authentication=ActiveDirectoryPassword` na cadeia de conexão e o `UID` e `PWD` palavras-chave com o nome de usuário e senha, respectivamente.
>- Para se conectar usando a autenticação integrado ao Active Directory (driver do Windows somente) ou integrada do Windows, especifique `Authentication=ActiveDirectoryIntegrated` na cadeia de conexão. O driver escolherá o modo de autenticação correto automaticamente. `UID`e `PWD` não deve ser especificado.

## <a name="authenticating-with-an-access-token-windows-driver-only"></a>Autenticar com um Token de acesso (driver do Windows somente)

O `SQL_COPT_SS_ACCESS_TOKEN` atributo da conexão permite o uso de um token de acesso obtido do Azure AD para autenticação em vez do nome de usuário e senha e também ignora a negociação e a obtenção de um token de acesso pelo driver. Para usar um token de acesso, defina o `SQL_COPT_SS_ACCESS_TOKEN` atributo de conexão para um ponteiro para um `ACCESSTOKEN` estrutura:

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

O `ACCESSTOKEN` é uma estrutura de comprimento variável que consiste em 4 bytes _comprimento_ seguido por _comprimento_ bytes de dados opacos que formam o token de acesso. Devido a como o SQL Server trata os tokens de acesso, obtido por meio de um [OAuth 2.0](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-authentication-scenarios) resposta JSON deve ser expandida para que cada byte é seguido por um 0 byte, semelhante a uma cadeia de caracteres de UCS-2 que contém somente caracteres ASCII de preenchimento; no entanto, o token é um valor opaco e o comprimento especificado, em bytes, não devem incluir qualquer terminador nulo. Devido a suas restrições de tamanho e formato consideráveis, esse método de autenticação só está disponível por meio de programação via o `SQL_COPT_SS_ACCESS_TOKEN` coonnection atributo; não há palavra-chave de cadeia de caracteres de conexão ou DSN correspondente. A cadeia de caracteres de conexão não deve conter `UID`, `PWD`, `Authentication`, ou `Trusted_Connection` palavras-chave.

## <a name="azure-active-directory-authentication-sample-code"></a>Código de exemplo de autenticação do Active Directory do Azure

O exemplo a seguir mostra o código necessário para se conectar ao SQL Server usando o Active Directory do Azure com palavras-chave de conexão. Observe que não há necessidade de alterar o código do aplicativo em si; a cadeia de caracteres de conexão ou DSN se um for usado, é a única modificação necessária para usar o AAD para autenticação:
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
O exemplo a seguir mostra o código necessário para se conectar ao SQL Server usando o Active Directory do Azure com autenticação de token de acesso. Nesse caso, é necessário modificar o código do aplicativo para processar o token de acesso e defina o atributo de conexão associada.
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

## <a name="see-also"></a>Consulte também
[Suporte à autenticação baseada em token para banco de dados do SQL Azure usando a autenticação do AD do Azure](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)


