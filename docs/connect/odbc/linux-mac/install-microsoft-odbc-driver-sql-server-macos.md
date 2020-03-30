---
title: Instalar o Microsoft ODBC Driver for SQL Server (macOS)
ms.date: 03/05/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver, installing
author: rothja
ms.author: v-jizho2
manager: jroth
ms.openlocfilehash: 7ad2b810092fae850a667a1611880f4b03b6a9a8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79078949"
---
# <a name="install-the-microsoft-odbc-driver-for-sql-server-macos"></a>Instalar o Microsoft ODBC Driver for SQL Server (macOS)

Este artigo explica como instalar o Microsoft ODBC Driver for SQL Server no macOS. Também inclui instruções para as ferramentas de linha de comando opcionais para o SQL Server (`bcp` e `sqlcmd`) e os cabeçalhos de desenvolvimento unixODBC.

Este artigo fornece comandos para instalar o driver ODBC por meio do shell Bash. Caso deseje baixar os pacotes diretamente, confira [Baixar o ODBC Driver for SQL Server](../download-odbc-driver-for-sql-server.md).

## <a name="microsoft-odbc-17"></a>Microsoft ODBC 17

Para instalar o Microsoft ODBC Driver 17 for SQL Server no macOS, execute os seguintes comandos:

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
HOMEBREW_NO_ENV_FILTERING=1 ACCEPT_EULA=Y brew install msodbcsql17 mssql-tools
```

> [!IMPORTANT]
> Se você tiver instalado o pacote v17 `msodbcsql` que estava disponível brevemente, deverá removê-lo antes de instalar o pacote `msodbcsql17`. Isso evitará conflitos. O pacote `msodbcsql17` pode ser instalado lado a lado com o pacote `msodbcsql` v13.

## <a name="previous-versions"></a>Versões anteriores

As seções a seguir fornecem instruções sobre como instalar versões anteriores do Microsoft ODBC Driver no macOS.

## <a name="odbc-131"></a><a id="13.1"></a> ODBC 13.1

Use os seguintes comandos para instalar o Microsoft ODBC Driver 13.1 for SQL Server no OS X 10.11 (El Capitan) e no macOS 10.12 (Sierra):

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install msodbcsql@13.1.9.2 mssql-tools@14.0.6.0
```

## <a name="driver-files"></a>Arquivos do driver

O driver ODBC no macOS consiste nos seguintes componentes:

|Componente|DESCRIÇÃO|  
|---------------|-----------------|  
|libmsodbcsql.17.dylib ou libmsodbcsql.13.dylib|O arquivo de biblioteca dinâmica (`dylib`) que contém toda a funcionalidade do driver. Esse arquivo é instalado em `/usr/local/lib/`.|  
|`msodbcsqlr17.rll` ou `msodbcsqlr13.rll`|O arquivo de recursos que acompanha a biblioteca do driver. Esse arquivo é instalado em `[driver .dylib directory]../share/msodbcsql17/resources/en_US/` para o Driver 17 e em `[driver .dylib directory]../share/msodbcsql/resources/en_US/` para o Driver 13. | 
|msodbcsql.h|O arquivo de cabeçalho que contém todas as novas definições necessárias para usar o driver.<br /><br /> **Observação:**  você não pode referenciar msodbcsql.h e odbcss.h no mesmo programa.<br /><br /> msodbcsql.h é instalado em `/usr/local/include/msodbcsql17/` para o Driver 17 e em `/usr/local/include/msodbcsql/` para o Driver 13. |
|LICENSE.txt|O arquivo de texto que contém os termos do Contrato de Licença do Usuário Final. Esse arquivo é colocado no `/usr/local/share/doc/msodbcsql17/` para o Driver 17 e em `/usr/local/share/doc/msodbcsql/` para o Driver 13. |
|RELEASE_NOTES|O arquivo de texto que contém as notas sobre a versão. Esse arquivo é colocado no `/usr/local/share/doc/msodbcsql17/` para o Driver 17 e em `/usr/local/share/doc/msodbcsql/` para o Driver 13. |

## <a name="resource-file-loading"></a>Carregamento de arquivo de recursos

O driver precisa carregar o arquivo de recurso para funcionar. Esse arquivo é denominado `msodbcsqlr17.rll` ou `msodbcsqlr13.rll`, dependendo da versão do driver. O local do arquivo `.rll` é relativo ao local do driver em si (`so` ou `dylib`), conforme observado na tabela acima. A partir da versão 17.1, o driver também tentará carregar o `.rll` do diretório padrão se o carregamento do caminho relativo falhar. O caminho do arquivo de recurso padrão no macOS é `/usr/local/share/msodbcsql17/resources/en_US/`

## <a name="troubleshooting"></a>solução de problemas

Caso não possa estabelecer uma conexão com o SQL Server usando o driver ODBC, confira o artigo sobre problemas conhecidos em [Solução de problemas de conexão](known-issues-in-this-version-of-the-driver.md#connectivity).

## <a name="next-steps"></a>Próximas etapas

Depois de instalar o driver, experimente o [aplicativo de exemplo C++ ODBC](../../odbc/cpp-code-example-app-connect-access-sql-db.md). Para obter mais informações sobre como desenvolver aplicativos ODBC, confira [Desenvolver aplicativos](../../../odbc/reference/develop-app/developing-applications.md).

Para obter mais informações, confira as [notas sobre a versão](release-notes-odbc-sql-server-linux-mac.md) e os [requisitos do sistema](system-requirements.md) do driver ODBC.
