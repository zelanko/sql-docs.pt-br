---
title: Como usar o Azure Active Directory
description: Saiba mais sobre os métodos de autenticação do Azure Active Directory disponíveis no Driver do Microsoft OLE DB para SQL Server que permitem a conexão com os bancos de dados SQL do Azure.
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: bace88bd8ccf42cbef96a34ddb2af2593cedd7be
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727287"
---
# <a name="using-azure-active-directory"></a>Como usar o Azure Active Directory
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>Finalidade

Na versão 18.2.1 e posteriores, o Driver do Microsoft OLE DB para SQL Server permite que aplicativos OLE DB se conectem a uma instância do Banco de Dados SQL do Azure usando uma identidade federada. Os novos métodos de autenticação incluem:
- ID de logon e senha do Azure Active Directory
- Token de acesso do Azure Active Directory
- Autenticação integrada do Azure Active Directory
- ID de logon e senha do SQL

A versão 18.3 adiciona suporte para os seguintes métodos de autenticação:
- Autenticação interativa do Azure Active Directory
- Autenticação de Identidade Gerenciada do Azure Active Directory

> [!NOTE]
> O uso dos seguintes modos de autenticação **não** é compatível com o uso de `DataTypeCompatibility` (ou sua propriedade correspondente) definida como `80`:
> - Autenticação do Azure Active Directory usando ID de logon e senha
> - Autenticação do Azure Active Directory usando token de acesso
> - Autenticação integrada do Azure Active Directory
> - Autenticação interativa do Azure Active Directory
> - Autenticação de Identidade Gerenciada do Azure Active Directory

## <a name="connection-string-keywords-and-properties"></a>Palavras-chave e propriedades da cadeia de conexão
As seguintes palavras-chave da cadeia de conexão foram introduzidas para dar suporte à autenticação do Azure Active Directory:

|Palavras-chave da cadeia de conexão|Propriedade Connection|Descrição|
|---               |---                |---        |
|Token de acesso|SSPROP_AUTH_ACCESS_TOKEN|Especifica um token de acesso para autenticar no Azure Active Directory. |
|Autenticação|SSPROP_AUTH_MODE|Especifica método de autenticação a ser usado.|

Para obter mais informações sobre as novas palavras-chave/propriedades, confira as seguintes páginas:
- [Uso de palavras-chave de cadeia de conexão com o Driver do OLE DB para SQL Server](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [Propriedades de inicialização e autorização](../ole-db-data-source-objects/initialization-and-authorization-properties.md)

## <a name="encryption-and-certificate-validation"></a>Criptografia e validação de certificado
Esta seção aborda as alterações no comportamento de criptografia e validação de certificado. Essas alterações **somente** entram em vigor ao usar as novas palavras-chave de cadeia de conexão de token de acesso ou de autenticação (ou suas propriedades correspondentes).

### <a name="encryption"></a>Criptografia
Para aprimorar a segurança, quando as novas propriedades de conexão/palavras-chave são usadas, o driver substitui o valor de criptografia padrão, configurando-o como `yes`. A substituição ocorre no tempo de inicialização do objeto de fonte de dados. Se a criptografia for definida por qualquer meio antes da inicialização, o valor será respeitado e não será substituído.

> [!NOTE]   
> Em aplicativos ADO e em aplicativos que obtêm a interface `IDBInitialize` por meio de `IDataInitialize::GetDataSource`, o componente principal que implementa a interface define explicitamente a criptografia para seu valor padrão de `no`. Como resultado, as novas palavras-chave/propriedades de autenticação respeitam essa configuração e o valor de criptografia **não é** substituído. Portanto, é **recomendado** que esses aplicativos definam `Use Encryption for Data=true` explicitamente para substituir o valor padrão.

### <a name="certificate-validation"></a>Validação do certificado
Para aprimorar a segurança, as novas palavras-chave/propriedades de conexão respeitam a configuração de `TrustServerCertificate` (e as respectivas palavras-chave/propriedades de cadeia de conexão correspondentes) **independentemente da configuração de criptografia de cliente**. Como resultado, o certificado do servidor é validado por padrão.

> [!NOTE]   
> A validação de certificado também pode ser controlada por meio do campo `Value` da entrada do Registro `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI18.0\GeneralFlags\Flag2`. Os valores válidos são `0` ou `1`. O driver OLE DB escolhe a opção mais segura entre o Registro e as configurações de propriedade/palavra-chave de conexão. Ou seja, o driver validará o certificado do servidor contanto que pelo menos uma das configurações do Registro/conexão habilite a validação de certificado do servidor.

## <a name="gui-additions"></a>Adições de GUI
A interface gráfica do usuário do driver foi aprimorada para permitir a autenticação do Azure Active Directory. Para obter mais informações, consulte:
- [Caixa de diálogo de logon do SQL Server](../help-topics/sql-server-login-dialog.md)
- [Configuração do UDL (Universal Data Link)](../help-topics/data-link-pages.md)

## <a name="example-connection-strings"></a>Cadeias de conexão de exemplo
Esta seção mostra exemplos de palavras-chave de cadeia de conexão novas e existentes que serão usadas com `IDataInitialize::GetDataSource` e a propriedade `DBPROP_INIT_PROVIDERSTRING`.

### <a name="sql-authentication"></a>Autenticação SQL
- Usando `IDataInitialize::GetDataSource`:
    - Novo:
        > Provider=MSOLEDBSQL;Data Source=[servidor];Initial Catalog=[banco de dados];**Authentication=SqlPassword**;User ID=[nome de usuário];Password=[senha];Use Encryption for Data=true
    - Preterido:
        > Provider=MSOLEDBSQL;Data Source=[servidor];Initial Catalog=[banco de dados];User ID=[nome de usuário];Password=[senha];Use Encryption for Data=true
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    - Novo:
        > Server = [servidor];Database = [banco de dados];**Authentication = SqlPassword**;UID = [nome de usuário];PWD = [senha];Encrypt = yes
    - Preterido:
        > Server = [servidor];Database = [banco de dados];UID = [nome de usuário];PWD = [senha];Encrypt = yes

### <a name="integrated-windows-authentication-using-security-support-provider-interface-sspi"></a>Autenticação Integrada do Windows usando a interface SSPI

- Usando `IDataInitialize::GetDataSource`:
    - Novo:
        > Provider=MSOLEDBSQL;Data Source=[servidor];Initial Catalog=[banco de dados];**Authentication=ActiveDirectoryIntegrated**;Use Encryption for Data=true
    - Preterido:
        > Provider=MSOLEDBSQL;Data Source=[servidor];Initial Catalog=[banco de dados];**Integrated Security=SSPI**;Use Encryption for Data=true
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    - Novo:
        > Server = [servidor];Database = [banco de dados];**Authentication = ActiveDirectoryIntegrated**;Encrypt = yes
    - Preterido:
        > Server = [servidor];Database = [banco de dados];**Trusted_Connection = yes**;Encrypt = yes

### <a name="azure-active-directory-username-and-password-authentication"></a>Autenticação do Azure Active Directory com nome de usuário e senha

- Usando `IDataInitialize::GetDataSource`:
    > Provider=MSOLEDBSQL;Data Source=[servidor];Initial Catalog=[banco de dados];**Authentication=ActiveDirectoryPassword**;User ID=[nome de usuário];Password=[senha];Use Encryption for Data=true
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    > Server = [servidor];Database = [banco de dados];**Authentication = ActiveDirectoryPassword**;UID = [nome de usuário];PWD = [senha];Encrypt=yes

### <a name="azure-active-directory-integrated-authentication"></a>Autenticação integrada do Azure Active Directory

- Usando `IDataInitialize::GetDataSource`:
    > Provider=MSOLEDBSQL;Data Source=[servidor];Initial Catalog=[banco de dados];**Authentication=ActiveDirectoryIntegrated**;Use Encryption for Data=true
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    > Server = [servidor];Database = [banco de dados];**Authentication = ActiveDirectoryIntegrated**;Encrypt = yes

### <a name="azure-active-directory-authentication-using-an-access-token"></a>Autenticação do Azure Active Directory usando um token de acesso

- Usando `IDataInitialize::GetDataSource`:
    > Provider=MSOLEDBSQL;Data Source=[servidor];Initial Catalog=[banco de dados];**Access Token=[token de acesso]**;Use Encryption for Data=true
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    > O fornecimento de um token de acesso por meio de `DBPROP_INIT_PROVIDERSTRING` não é um procedimento compatível

### <a name="azure-active-directory-interactive-authentication"></a>Autenticação interativa do Azure Active Directory

- Usando `IDataInitialize::GetDataSource`:
    > Provider=MSOLEDBSQL;Data Source=[servidor];Initial Catalog=[banco de dados];**Authentication=ActiveDirectoryInteractive**;User ID=[nome de usuário];Use Encryption for Data=true
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    > Server=[servidor];Database=[banco de dados];**Authentication=ActiveDirectoryInteractive**;UID=[nome de usuário];Encrypt=yes

### <a name="azure-active-directory-managed-identity-authentication"></a>Autenticação de Identidade Gerenciada do Azure Active Directory

- Usando `IDataInitialize::GetDataSource`:
    - Identidade gerenciada atribuída ao usuário:
        > Provider=MSOLEDBSQL;Data Source=[servidor];Initial Catalog=[banco de dados];**Authentication=ActiveDirectoryMSI**;User ID=[ID do Objeto];Use Encryption for Data=true
    - Identidade gerenciada atribuída ao sistema:
        > Provider=MSOLEDBSQL;Data Source=[servidor];Initial Catalog=[banco de dados];**Authentication=ActiveDirectoryMSI**;Use Encryption for Data=true
- Usando `DBPROP_INIT_PROVIDERSTRING`:
    - Identidade gerenciada atribuída ao usuário:
        > Server=[servidor];Database=[banco de dados];**Authentication=ActiveDirectoryMSI**;UID=[ID do Objeto];Encrypt=yes
    - Identidade gerenciada atribuída ao sistema:
        > Server=[servidor];Database=[banco de dados];**Authentication=ActiveDirectoryMSI**;Encrypt=yes

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
- [Autorizar o acesso a aplicativos Web do Azure Active Directory usando o fluxo de concessão de código do OAuth 2.0](/azure/active-directory/azuread-dev/v1-protocols-oauth-code).

- Saiba mais sobre as [Autenticação do Azure Active Directory](/azure/azure-sql/database/authentication-aad-overview) para SQL Server.

- Configure conexões de driver usando [palavras-chave da cadeia de conexão](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md) compatíveis com o driver OLE DB.