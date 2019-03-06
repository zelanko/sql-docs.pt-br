---
title: Usando o Active Directory do Azure | Documentos do Microsoft para SQL Server
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: 44f92e782a497005ea47847301279e4341722d36
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744783"
---
# <a name="using-azure-active-directory"></a>Como usar o Azure Active Directory
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>Finalidade

Começando com a versão 18.2.1, Microsoft Driver do OLE DB para SQL Server permite que os aplicativos OLE DB para se conectar a uma instância do banco de dados SQL usando uma identidade federada. Os novos métodos de autenticação incluem:
- ID de logon do Active Directory do Azure e a senha
- Token de acesso do Azure Active Directory
- Autenticação integrada do Azure Active Directory
- ID de logon do SQL e a senha

> [!NOTE]  
> Ao usar as seguintes opções do Azure Active Directory com o driver do OLE DB, certifique-se de que o [Active Directory Authentication Library para SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072) foi instalado:
> - ID de logon do Active Directory do Azure e a senha
> - Autenticação integrada do Azure Active Directory
>
> ADAL não é necessária para os outros métodos de autenticação ou operações de banco de dados OLE.

> [!NOTE]
> Usando os seguintes modos de autenticação com `DataTypeCompatibility` (ou sua propriedade correspondente) definido como `80` é **não** com suporte:
> - Autenticação do Active Directory do Azure usando a ID de logon e senha
> - Autenticação do Active Directory do Azure usando o token de acesso
> - Autenticação integrada do Azure Active Directory

## <a name="connection-string-keywords-and-properties"></a>As propriedades e as palavras-chave de cadeia de caracteres de Conexão
As seguintes palavras chave cadeia de caracteres de conexão foram introduzidas para dar suporte à autenticação do Active Directory do Azure:

|Palavras-chave da cadeia de conexão|Propriedades da conexão|Descrição|
|---               |---                |---        |
|Token de acesso|SSPROP_AUTH_ACCESS_TOKEN|Especifica um token de acesso para autenticar no Azure Active Directory. |
|Autenticação|SSPROP_AUTH_MODE|Especifica o método de autenticação a ser usado.|

Para obter mais informações sobre as novas palavras-chave/propriedades, consulte as seguintes páginas:
- [Uso de palavras-chave de cadeia de conexão com o Driver do OLE DB para SQL Server](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [Propriedades de inicialização e autorização](../ole-db-data-source-objects/initialization-and-authorization-properties.md)

## <a name="encryption-and-certificate-validation"></a>Criptografia e validação de certificado
Esta seção discute as alterações no comportamento de validação de certificado e criptografia. Essas alterações são **apenas** eficaz ao usar as nova autenticação ou Token de acesso conexão palavras-chave (ou suas propriedades correspondentes).

### <a name="encryption"></a>Criptografia
Para melhorar a segurança, quando as nova conexão propriedades/palavras-chave são usadas, o driver substitui o valor de criptografia padrão definindo-a para `yes`. Substituindo ocorre em tempo de inicialização do objeto de fonte de dados. Se a criptografia é definida antes da inicialização por qualquer meio, o valor é respeitado e não é substituído.

> [!NOTE]   
> Em aplicativos ADO e em aplicativos que obtêm as `IDBInitialize` por meio da interface `IDataInitialize::GetDataSource`, o principal componente Implementando a interface explicitamente define a criptografia para seu valor padrão de `no`. Como resultado, as nova autenticação propriedades/palavras-chave respeita essa configuração e o valor de criptografia **não é** substituído. Portanto, é **recomendado** que esses aplicativos definam explicitamente `Use Encryption for Data=true` para substituir o valor padrão.

### <a name="certificate-validation"></a>Validação do certificado
Para melhorar a segurança, as nova conexão propriedades/palavras-chave respeitam a `TrustServerCertificate` configuração (e suas conexão cadeia de caracteres palavras-chave/propriedades correspondentes) **independentemente da configuração de criptografia do cliente**. Como resultado, o certificado do servidor é validado por padrão.

> [!NOTE]   
> Validação do certificado também pode ser controlada por meio de `Value` campo do `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI18.0\GeneralFlags\Flag2` entrada do registro. Os valores válidos são `0` ou `1`. O driver do OLE DB escolhe a opção mais segura entre o registro e as configurações de propriedade/palavra-chave de conexão. Ou seja, o driver validará o certificado do servidor, desde que pelo menos uma das configurações do registro/conexão habilita a validação de certificado do servidor.

## <a name="gui-additions"></a>Adições de GUI
A interface gráfica do usuário do driver foi aprimorada para permitir a autenticação do Active Directory do Azure. Para obter mais informações, consulte:
- [Caixa de diálogo de logon do SQL Server](../help-topics/sql-server-login-dialog.md)
- [Configuração do UDL (Link) de dados universal](../help-topics/data-link-pages.md)

## <a name="example-connection-strings"></a>Cadeias de conexão de exemplo
Esta seção mostra exemplos de conexão nova e existente palavras-chave de cadeia de caracteres a ser usado com `IDataInitialize::GetDataSource` e `DBPROP_INIT_PROVIDERSTRING` propriedade.

### <a name="sql-authentication"></a>Autenticação SQL
- Usando `IDataInitialize::GetDataSource`:
    - Novo:
        > Provedor = MSOLEDBSQL; fonte de dados = [servidor]; Initial Catalog = [database]; **Autenticação = SqlPassword**; ID de usuário = [username]; Senha = [senha]; Usar a criptografia de dados = true
    - Preterido:
        > Provedor = MSOLEDBSQL; fonte de dados = [servidor]; Initial Catalog = [database]; ID de usuário = [username]; Senha = [senha]; Usar a criptografia de dados = true
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    - Novo:
        > Server = [servidor];Database = [banco de dados];**Authentication = SqlPassword**;UID = [nome de usuário];PWD = [senha];Encrypt = yes
    - Preterido:
        > Server = [servidor];Database = [banco de dados];UID = [nome de usuário];PWD = [senha];Encrypt = yes

### <a name="integrated-windows-authentication-using-security-support-provider-interface--sspi"></a>Autenticação integrada do Windows usando a Interface de provedor de suporte de segurança (SSPI)

- Usando `IDataInitialize::GetDataSource`:
    - Novo:
        > Provedor = MSOLEDBSQL; fonte de dados = [servidor]; Initial Catalog = [database]; **Autenticação = ActiveDirectoryIntegrated**; Usar a criptografia de dados = true
    - Preterido:
        > Provedor = MSOLEDBSQL; fonte de dados = [servidor]; Initial Catalog = [database]; **a segurança integrada = SSPI**; Usar a criptografia de dados = true
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    - Novo:
        > Server = [servidor];Database = [banco de dados];**Authentication = ActiveDirectoryIntegrated**;Encrypt = yes
    - Preterido:
        > Server = [servidor];Database = [banco de dados];**Trusted_Connection = yes**;Encrypt = yes

### <a name="aad-username-and-password-authentication-using-adal"></a>Autenticação de nome de usuário e senha do AAD usando a ADAL

- Usando `IDataInitialize::GetDataSource`:
    > Provedor = MSOLEDBSQL; fonte de dados = [servidor]; Initial Catalog = [database]; **Autenticação = ActiveDirectoryPassword**; ID de usuário = [username]; Senha = [senha]; Usar a criptografia de dados = true
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    > Server = [servidor];Database = [banco de dados];**Authentication = ActiveDirectoryPassword**;UID = [nome de usuário];PWD = [senha];Encrypt=yes

### <a name="integrated-azure-active-directory-authentication-using-adal"></a>Autenticação integrada do Active Directory do Azure usando a ADAL

- Usando `IDataInitialize::GetDataSource`:
    > Provedor = MSOLEDBSQL; fonte de dados = [servidor]; Initial Catalog = [database]; **Autenticação = ActiveDirectoryIntegrated**; Usar a criptografia de dados = true
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    > Server = [servidor];Database = [banco de dados];**Authentication = ActiveDirectoryIntegrated**;Encrypt = yes

### <a name="azure-active-directory-authentication-using-an-access-token"></a>Autenticação do Active Directory do Azure usando um token de acesso

- Usando `IDataInitialize::GetDataSource`:
    > Provedor = MSOLEDBSQL; fonte de dados = [servidor]; Initial Catalog = [database]; **Token de acesso = [token de acesso]**; Usar a criptografia de dados = true
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    > Fornecendo o token de acesso por meio de `DBPROP_INIT_PROVIDERSTRING` não é suportado

## <a name="code-samples"></a>Exemplos de código

Os exemplos a seguir mostram o código necessário para se conectar ao Azure Active Directory com palavras-chave de conexão. 

### <a name="access-token"></a>Token de acesso
```cpp
#include <string>
#include <iostream>
#include <msdasc.h>

int main()
{
    wchar_t azureServer[] = L"server";
    wchar_t azureDatabase[] = L"mydatabase";
    wchar_t accessToken[] = L"eyJ0eXAiOi...";
    IDBInitialize *pIDBInitialize = nullptr;
    IDataInitialize* pIDataInitialize = nullptr;
    HRESULT hr = S_OK;

    CoInitialize(nullptr);

    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(azureServer) + L";Initial Catalog=" + 
                              std::wstring(azureDatabase) + L";Access Token=" + accessToken + L";Use Encryption for Data=true;";
    hr = CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, 
                          IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to create an IDataInitialize instance." << std::endl;
        goto Cleanup;
    }
    hr = pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), 
                                         IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to get data source object." << std::endl;
        goto Cleanup;
    }
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr))
    {
        std::cout << "Failed to establish connection." << std::endl;
        goto Cleanup;
    }

Cleanup:
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
    }
    if (pIDataInitialize)
    {
        pIDataInitialize->Release();
    }

    CoUninitialize();
}
```
### <a name="active-directory-integrated"></a>Integrado ao Active Directory
```cpp
#include <string>
#include <iostream>
#include <msdasc.h>

int main()
{
    wchar_t azureServer[] = L"server";
    wchar_t azureDatabase[] = L"mydatabase";
    IDBInitialize *pIDBInitialize = nullptr;
    IDataInitialize* pIDataInitialize = nullptr;
    HRESULT hr = S_OK;

    CoInitialize(nullptr);

    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(azureServer) + L";Initial Catalog=" + 
                              std::wstring(azureDatabase) + L";Authentication=ActiveDirectoryIntegrated;Use Encryption for Data=true;";

    hr = CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, 
                          IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize));
    if (FAILED(hr)) 
    {
        std::cout << "Failed to create an IDataInitialize instance." << std::endl;
        goto Cleanup;
    }
    hr = pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), 
                                         IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to get data source object." << std::endl;
        goto Cleanup;
    }
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr))
    {
        std::cout << "Failed to establish connection." << std::endl;
        goto Cleanup;
    }

Cleanup:
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
    }
    if (pIDataInitialize)
    {
        pIDataInitialize->Release();
    }

    CoUninitialize();
}
```

## <a name="next-steps"></a>Próximas etapas
- [Autorizar o acesso a aplicativos de web do Azure Active Directory usando o fluxo de concessão de código OAuth 2.0](https://go.microsoft.com/fwlink/?linkid=2072672).

- Saiba mais sobre as [Autenticação do Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=2073783) para SQL Server.

- Configurar conexões de driver usando o [palavras-chave de cadeia de caracteres de conexão](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md) o oferece suporte ao driver de banco de dados OLE.
