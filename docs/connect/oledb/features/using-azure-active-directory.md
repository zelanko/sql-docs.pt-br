---
title: Usando Azure Active Directory | Microsoft Docs para SQL Server
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: b459877be731da11b33d13772bbf186ecf72198c
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381846"
---
# <a name="using-azure-active-directory"></a>Como usar o Azure Active Directory
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>Finalidade

A partir da versão 18.2.1, o Microsoft OLE DB driver for SQL Server permite que OLE DB aplicativos se conectem a uma instância do banco de dados SQL do Azure usando uma identidade federada. Os novos métodos de autenticação incluem:
- ID de logon Azure Active Directory e senha
- Token de acesso do Azure Active Directory
- Autenticação integrada do Azure Active Directory
- ID de logon e senha do SQL

A versão 18,3 adiciona suporte para os seguintes métodos de autenticação:
- Autenticação interativa do Azure Active Directory
- Autenticação do MSI do Azure Active Directory

> [!NOTE]
> **Não** há suporte para o uso dos seguintes modos de autenticação com `DataTypeCompatibility` (ou sua propriedade correspondente) definida como `80`:
> - Azure Active Directory autenticação usando a ID de logon e a senha
> - Autenticação Azure Active Directory usando o token de acesso
> - Autenticação integrada do Azure Active Directory
> - Autenticação interativa do Azure Active Directory
> - Autenticação do MSI do Azure Active Directory

## <a name="connection-string-keywords-and-properties"></a>Propriedades e palavras-chave da cadeia de conexão
As seguintes palavras-chave da cadeia de conexão foram introduzidas para dar suporte à autenticação Azure Active Directory:

|Palavras-chave da cadeia de conexão|Propriedades da conexão|Descrição|
|---               |---                |---        |
|Token de acesso|SSPROP_AUTH_ACCESS_TOKEN|Especifica um token de acesso para autenticar Azure Active Directory. |
|Autenticação|SSPROP_AUTH_MODE|Especifica método de autenticação a ser usado.|

Para obter mais informações sobre as novas palavras-chave/propriedades, consulte as seguintes páginas:
- [Uso de palavras-chave de cadeia de conexão com o Driver do OLE DB para SQL Server](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [Propriedades de inicialização e autorização](../ole-db-data-source-objects/initialization-and-authorization-properties.md)

## <a name="encryption-and-certificate-validation"></a>Criptografia e validação de certificado
Esta seção aborda as alterações na criptografia e no comportamento de validação de certificado. Essas alterações **só** são eficazes ao usar as novas palavras-chave de cadeia de conexão de token de acesso ou autenticação (ou suas propriedades correspondentes).

### <a name="encryption"></a>Criptografia
Para melhorar a segurança, quando as novas propriedades de conexão/palavras-chave são usadas, o driver substitui o valor de criptografia padrão definindo-o como `yes`. A substituição ocorre no tempo de inicialização do objeto da fonte de dados. Se a criptografia for definida antes da inicialização por qualquer meio, o valor será respeitado e não será substituído.

> [!NOTE]   
> Em aplicativos ADO e em aplicativos que obtêm a interface `IDBInitialize` por meio de `IDataInitialize::GetDataSource`, o componente principal que implementa a interface define explicitamente a criptografia para seu valor padrão de `no`. Como resultado, as novas palavras-chave/propriedades de autenticação respeitam essa configuração e o valor de criptografia **não é** substituído. Portanto, é **recomendável** que esses aplicativos definam explicitamente `Use Encryption for Data=true` para substituir o valor padrão.

### <a name="certificate-validation"></a>Validação do certificado
Para melhorar a segurança, as novas palavras-chave/propriedades de conexão respeitam a configuração de `TrustServerCertificate` (e suas palavras-chave/propriedades de cadeia de conexão correspondentes), **independentemente da configuração de criptografia do cliente**. Como resultado, o certificado do servidor é validado por padrão.

> [!NOTE]   
> A validação de certificado também pode ser controlada por meio do campo `Value` da entrada de registro `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI18.0\GeneralFlags\Flag2`. Os valores válidos são `0` ou `1`. O driver OLE DB escolhe a opção mais segura entre o registro e as configurações de propriedade/palavra-chave de conexão. Ou seja, o Driver validará o certificado do servidor Contanto que pelo menos uma das configurações de registro/conexão habilite a validação de certificado do servidor.

## <a name="gui-additions"></a>Adições de GUI
A interface gráfica do usuário do driver foi aprimorada para permitir a autenticação Azure Active Directory. Para obter mais informações, consulte:
- [Caixa de diálogo de logon do SQL Server](../help-topics/sql-server-login-dialog.md)
- [Configuração do UDL (Universal Data Link)](../help-topics/data-link-pages.md)

## <a name="example-connection-strings"></a>Cadeias de conexão de exemplo
Esta seção mostra exemplos de palavras-chave de cadeia de conexão novas e existentes que serão usadas com `IDataInitialize::GetDataSource` e `DBPROP_INIT_PROVIDERSTRING` propriedade.

### <a name="sql-authentication"></a>Autenticação SQL
- Usando `IDataInitialize::GetDataSource`:
    - Novo:
        > Provider = MSOLEDBSQL; fonte de dados = [Server]; Initial Catalog = [Database]; **Autenticação = SQLPassword**; ID de usuário = [username]; Senha = [senha]; Usar criptografia para dados = verdadeiro
    - Preterido:
        > Provider = MSOLEDBSQL; fonte de dados = [Server]; Initial Catalog = [Database]; ID de usuário = [username]; Senha = [senha]; Usar criptografia para dados = verdadeiro
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    - Novo:
        > Server = [servidor];Database = [banco de dados];**Authentication = SqlPassword**;UID = [nome de usuário];PWD = [senha];Encrypt = yes
    - Preterido:
        > Server = [servidor];Database = [banco de dados];UID = [nome de usuário];PWD = [senha];Encrypt = yes

### <a name="integrated-windows-authentication-using-security-support-provider-interface-sspi"></a>Autenticação integrada do Windows usando a interface de provedor de suporte de segurança (SSPI)

- Usando `IDataInitialize::GetDataSource`:
    - Novo:
        > Provider = MSOLEDBSQL; fonte de dados = [Server]; Initial Catalog = [Database]; **Autenticação = ActiveDirectoryIntegrated**; Usar criptografia para dados = verdadeiro
    - Preterido:
        > Provider = MSOLEDBSQL; fonte de dados = [Server]; Initial Catalog = [Database]; **Segurança integrada = SSPI**; Usar criptografia para dados = verdadeiro
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    - Novo:
        > Server = [servidor];Database = [banco de dados];**Authentication = ActiveDirectoryIntegrated**;Encrypt = yes
    - Preterido:
        > Server = [servidor];Database = [banco de dados];**Trusted_Connection = yes**;Encrypt = yes

### <a name="azure-active-directory-username-and-password-authentication"></a>Azure Active Directory autenticação de nome de usuário e senha

- Usando `IDataInitialize::GetDataSource`:
    > Provider = MSOLEDBSQL; fonte de dados = [Server]; Initial Catalog = [Database]; **Autenticação = ActiveDirectoryPassword**; ID de usuário = [username]; Senha = [senha]; Usar criptografia para dados = verdadeiro
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    > Server = [servidor];Database = [banco de dados];**Authentication = ActiveDirectoryPassword**;UID = [nome de usuário];PWD = [senha];Encrypt=yes

### <a name="azure-active-directory-integrated-authentication"></a>Autenticação integrada do Azure Active Directory

- Usando `IDataInitialize::GetDataSource`:
    > Provider = MSOLEDBSQL; fonte de dados = [Server]; Initial Catalog = [Database]; **Autenticação = ActiveDirectoryIntegrated**; Usar criptografia para dados = verdadeiro
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    > Server = [servidor];Database = [banco de dados];**Authentication = ActiveDirectoryIntegrated**;Encrypt = yes

### <a name="azure-active-directory-authentication-using-an-access-token"></a>Azure Active Directory autenticação usando um token de acesso

- Usando `IDataInitialize::GetDataSource`:
    > Provider = MSOLEDBSQL; fonte de dados = [Server]; Initial Catalog = [Database]; **Token de acesso = [token de acesso]** ; Usar criptografia para dados = verdadeiro
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    > Não há suporte para o fornecimento de token de acesso por meio de `DBPROP_INIT_PROVIDERSTRING`

### <a name="azure-active-directory-interactive-authentication"></a>Autenticação interativa do Azure Active Directory

- Usando `IDataInitialize::GetDataSource`:
    > Provider = MSOLEDBSQL; fonte de dados = [Server]; Initial Catalog = [Database]; **Autenticação = ActiveDirectoryInteractive**; ID de usuário = [username]; Usar criptografia para dados = verdadeiro
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    > Server = [servidor];D Anco = [banco de dados]; **Autenticação = ActiveDirectoryInteractive**; UID = [username]; Encrypt = Sim

### <a name="azure-active-directory-msi-authentication"></a>Autenticação do MSI do Azure Active Directory

- Usando `IDataInitialize::GetDataSource`:
    - Identidade gerenciada atribuída ao usuário:
        > Provider = MSOLEDBSQL; fonte de dados = [Server]; Initial Catalog = [Database]; **Autenticação = ActiveDirectoryMSI**; ID de usuário = [ID do objeto]; Usar criptografia para dados = verdadeiro
    - Identidade gerenciada atribuída ao sistema:
        > Provider = MSOLEDBSQL; fonte de dados = [Server]; Initial Catalog = [Database]; **Autenticação = ActiveDirectoryMSI**; Usar criptografia para dados = verdadeiro
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    - Identidade gerenciada atribuída ao usuário:
        > Server = [servidor];D Anco = [banco de dados]; **Autenticação = ActiveDirectoryMSI**; UID = [ID do objeto]; Encrypt = Sim
    - Identidade gerenciada atribuída ao sistema:
        > Server = [servidor];D Anco = [banco de dados]; **Autenticação = ActiveDirectoryMSI**; Encrypt = Sim

## <a name="code-samples"></a>Exemplos de código

Os exemplos a seguir mostram o código necessário para se conectar a Azure Active Directory com palavras-chave de conexão. 

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
- [Autorize o acesso a Azure Active Directory aplicativos Web usando o fluxo de concessão de código OAuth 2,0](https://go.microsoft.com/fwlink/?linkid=2072672).

- Saiba mais sobre as [Autenticação do Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=2073783) para SQL Server.

- Configure conexões de driver usando [palavras-chave de cadeia de conexão](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md) às quais o driver de OLE DB dá suporte.
