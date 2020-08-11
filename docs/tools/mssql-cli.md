---
title: mssql-cli
description: O mssql-cli é uma ferramenta de consulta de linha de comando interativa para SQL Server que é executada no Windows, no macOS ou no Linux.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, sstein, maghan
ms.custom: tools|mssql-cli
ms.date: 02/22/2018
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 03bc52a6f8941bbc8d04f8f795876b0ca664f08c
ms.sourcegitcommit: 6c2232c4d2c1ce5710296ce97b909f5ed9787f66
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84462280"
---
# <a name="mssql-cli-command-line-query-tool-for-sql-server-preview"></a>Ferramenta de consulta de linha de comando mssql-cli para SQL Server (versão prévia)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

O mssql-cli é uma ferramenta de linha de comando interativa para consultar o SQL Server e execute no Windows, macOS ou Linux.

## <a name="install-mssql-cli"></a>Instalar o mssql-cli

Para obter instruções de instalação detalhadas, confira o [Guia de Instalação](https://github.com/dbcli/mssql-cli/tree/master/doc/installation). Os cenários de instalação mais comuns são resumidos abaixo.

### <a name="windows-and-macos-installation"></a>Instalação do Windows e macOS

mssql-cli é instalado no Windows e macOS usando `pip`:

```$ pip install mssql-cli```

Para obter instruções mais detalhadas, confira o [Guia de Instalação](https://github.com/dbcli/mssql-cli/tree/master/doc/installation).

### <a name="linux-installation"></a>Instalação do Linux

Depois de registrar o repositório da Microsoft, o mssql-cli pode ser instalado e atualizado por meio de gerenciadores de pacotes em várias distribuições do Linux.

O exemplo a seguir se aplica ao Ubuntu 18.04 (Bionic). Mais informações e exemplos para outras distribuições podem ser encontrados no [Guia de Instalação](https://github.com/dbcli/mssql-cli/tree/master/doc/installation).

```
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
sudo apt-add-repository https://packages.microsoft.com/ubuntu/18.04/prod

# Update the list of products
sudo apt-get update

# Install mssql-cli
sudo apt-get install mssql-cli

# Install missing dependencies
sudo apt-get install -f
```

## <a name="mssql-cli-documentation"></a>Documentação do mssql-cli

A documentação do mssql-cli está localizada no [repositório do GitHub do mssql-cli](https://github.com/dbcli/mssql-cli).

- [Página principal/leiame](https://github.com/dbcli/mssql-cli)
- [Guia de instalação](https://github.com/dbcli/mssql-cli/tree/master/doc/installation)
- [Guia de uso](https://github.com/dbcli/mssql-cli/blob/master/doc/usage_guide.md)

A documentação adicional está localizada na [pasta doc](https://github.com/dbcli/mssql-cli/tree/master/doc).
