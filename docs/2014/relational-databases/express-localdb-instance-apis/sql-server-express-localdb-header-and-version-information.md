---
title: SQL Server Express informações de cabeçalho e versão do LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_location:
- sqluserinstance.dll
ms.assetid: 506b5161-b902-4894-b87b-9192d7b1664a
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6e390430115daf394c5e94267dad30a87851375d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63128693"
---
# <a name="sql-server-express-localdb-header-and-version-information"></a>Cabeçalho e informações de versão de LocalDB do SQL Server Express
  Não há nenhum arquivo de cabeçalho separado para a API da instância de LocalDB do SQL Server Express; as assinaturas e os códigos de erro da função LocalDB são definidos no arquivo de cabeçalho do SQL Server Native Client (sqlncli.h). Para usar a API de instância LocalDB, você deverá incluir o arquivo de cabeçalho sqlncli.h em seu projeto.  
  
## <a name="localdb-versioning"></a>Controle de versão de LocalDB  
 A instalação de LocalDB usa um único conjunto de binários por versão principal do SQL Server. Estas versões LocalDB são mantidas e corrigidas de maneira independente. Isto significa que o usuário tem que especificar qual versão de linha de base do LocalDB (quer dizer, a versão principal do SQL Server) ele ou ela estará usando. A versão é especificada no formato de versão padrão definido pela classe .NET Framework **System. Version** :  
  
 *principal. secundária [. Build [. revision]]*  
  
 Os dois primeiros números na cadeia de caracteres de versão (*principal* e *secundária*) são obrigatórios. Os dois últimos números na cadeia de caracteres de versão (*compilação* e *revisão*) são opcionais e padrão para zero se o usuário deixá-los fora. Isso significa que, se o usuário especificar apenas "12,2" como o número de versão de LocalDB, ele será tratado como se o usuário tiver especificado "12.2.0.0".  
  
 A versão para a instalação do LocalDB é definida na chave do Registro MSSQLServer\CurrentVersion na chave do Registro da instância do SQL Server, por exemplo:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL12E.LOCALDB\ MSSQLServer\CurrentVersion: "CurrentVersion"="12.0.2531.0"  
```  
  
 Diversas versões do LocalDB na mesma estação de trabalho têm suporte lado a lado. No entanto, o código do usuário sempre usa a DLL de **SQLUserInstance** mais recente disponível no computador local para se conectar às instâncias de LocalDB.  
  
## <a name="locating-the-sqluserinstance-dll"></a>Localizando a DLL SQLUserInstance  
 Para localizar a DLL de **SQLUserInstance** , o provedor do cliente usa a seguinte chave do registro:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions]  
```  
  
 Nesta chave, há uma lista de chaves, uma para cada versão do LocalDB instalada no computador. Cada uma dessas chaves é nomeada com o número de versão do LocalDB no formato * \<Major-Version>*.>de versão secundária (por exemplo, a chave para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] é chamada de 12,0). * \<* Em cada chave de versão há um par de nome-valor `InstanceAPIPath` que define o caminho completo para o arquivo SQLUserInstance.dll instalado com essa versão. O exemplo a seguir mostra as entradas do Registro para um computador que tem as versões 11.0 e 12.0 do LocalDB instaladas:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\12.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\120\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\12.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\120\\LocalDB\\Binn\\SqlUserInstance.dll"]  
```  
  
 O provedor do cliente deve encontrar a versão mais recente entre todas as versões instaladas e carregar o arquivo dll `InstanceAPIPath` do **SQLUserInstance** a partir do valor associado.  
  
### <a name="wow64-mode-on-64-bit-windows"></a>Modo de WOW64 no Windows de 64 bits  
 As instalações de 64 bits do LocalDB terão um conjunto adicional de chave do Registro para permitir que aplicativos de 32 bits executados em modo WOW64 (Windows-32-on-Windows-64) usem LocalDB. Especificamente, no Windows de 64 bits, o LocalDB MSI criará as chave do Registro a seguir:  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\12.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\120\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\12.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\120\\LocalDB\\Binn\\SqlUserInstance.dll"]  
  
```  
  
 os programas de 64 bits que `Installed Versions` lêem a chave verão os valores que apontam para versões de 64 bits da DLL de **SQLUserInstance** , enquanto os programas de 32 bits (executados em janelas de 64 de bits no modo WOW64) serão redirecionados automaticamente `Installed Versions` para `Wow6432Node` uma chave localizada no hive. Essa chave contém valores que apontam para versões de 32 bits da DLL de **SQLUserInstance** .  
  
## <a name="using-localdb_define_proxy_functions"></a>Usando LOCALDB_DEFINE_PROXY_FUNCTIONS  
 A API da instância LocalDB define uma constante chamada LOCALDB_DEFINE_PROXY_FUNCTIONS que automatiza a descoberta e o carregamento da DLL de **SqlUserInstance** .  
  
 A seção de código habilitada por esta constante fornece uma implementação de proxies para cada API do LocalDB. As implementações de proxy usam uma função comum para associar a pontos de entrada na DLL de **SqlUserInstance** mais recente instalada e, em seguida, encaminhar as solicitações.  
  
 As funções de proxy só serão habilitadas se a constante LOCALDB_DEFINE_PROXY_FUNCTIONS estiver definida no código de usuário antes de incluir o arquivo sqlncli.h. A constante deve ser definida em somente um módulo de origem (arquivo .cpp) porque define nomes de função externos para todos os pontos de entrada da API. Fornece uma implementação de proxies para cada API de LocalDB.  
  
 O exemplo de código a seguir mostra como usar a macro do código de C++ nativo:  
  
```  
// Define the LOCALDB_DEFINE_PROXY_FUNCTIONS constant to enable the LocalDB proxy functions   
// The #define has to take place BEFORE the API header file (sqlncli.h) is included  
#define LOCALDB_DEFINE_PROXY_FUNCTIONS  
#include <sqlncli.h>  
...  
HRESULT hr = S_OK;  
  
// Create LocalDB instance by calling the create API proxy function included by macro  
if (FAILED(hr = LocalDBCreateInstance( L"12.0", L"name", 0)))  
{  
...  
}  
...  
  
```  
  
  
