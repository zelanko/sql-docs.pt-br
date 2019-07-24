---
title: Instalar ferramentas de Big Data
titleSuffix: SQL Server big data clusters
description: Saiba como instalar ferramentas usadas com SQL Server clusters de Big Data 2019 (versão prévia).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 757209ff89fd40dcc737b65d3b19f2a7d4ef247b
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419459"
---
# <a name="install-sql-server-2019-big-data-tools"></a>Instalar as ferramentas do SQL Server 2019 Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve as ferramentas de cliente que devem ser instaladas para criar, gerenciar e usar SQL Server clusters de Big Data 2019 (versão prévia). A seção a seguir fornece uma lista de ferramentas e links para instruções de instalação. Antes de implantar um cluster Big Data, configure as ferramentas marcadas necessárias no Windows ou no Linux.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>Ferramentas de cluster de Big data

A tabela a seguir lista as ferramentas de cluster Big Data comuns e como instalá-las:

| Ferramenta | Obrigatório | Descrição | Instalação |
|---|---|---|---|
| **Python** | Sim | O Python é uma linguagem de programação de alto nível interpretada e orientada a objeto com semântica dinâmica. Muitas partes de Big Data clusters para SQL Server usam o Python. | [Instalar o Python](#python)|
| **azdata** | Sim | Ferramenta de linha de comando para instalar e gerenciar um cluster Big Data. | [Instalar](deploy-install-azdata.md) |
| **kubectl**<sup>1</sup> | Sim | Ferramenta de linha de comando para monitorar o cluster Kuberentes subjacente ([mais informações](https://kubernetes.io/docs/tasks/tools/install-kubectl/)). | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio (pessoas)** | Sim | Ferramenta gráfica de plataforma cruzada para consultar SQL Server ([mais informações](https://docs.microsoft.com/sql/azure-data-studio/what-is?view=sql-server-ver15)). | [Instalar](https://aka.ms/azdata-insiders) |
| **Extensão SQL Server 2019** | Sim | Extensão para Azure Data Studio que dá suporte à conexão com o cluster Big Data. Também fornece um assistente de virtualização de dados. | [Instalar](../azure-data-studio/sql-server-2019-extension.md) |
| **CLI do Azure** <sup>2</sup> | Para AKS | Interface de linha de comando moderna para gerenciar serviços do Azure. Usado com implantações de cluster do AKS Big Data ([mais informações](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)). | [Instalar](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | Opcional | Interface de linha de comando moderna para consultar SQL Server ([mais informações](https://github.com/dbcli/mssql-cli/blob/master/README.rst)). | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | Para alguns scripts | Ferramenta de linha de comando herdada para consultar SQL Server ([mais informações](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15)). | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | Para alguns scripts | Ferramenta de linha de comando para transferir dados com URLs. | [Windows](https://curl.haxx.se/windows/) \| Linux: instalar pacote de ondulação |

<sup>1</sup> você deve usar o kubectl versão 1,10 ou posterior. Além disso, a versão de kubectl deve ser mais ou menos uma versão secundária do cluster kubernetes. Se você quiser instalar uma versão específica no cliente do kubectl, consulte [instalar o binário do kubectl via ondulação](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) (no Windows 10, usar cmd. exe e não o Windows PowerShell para executar a rotação). 

> [!TIP]
> Para usar o kubectl com um cluster implantado anteriormente no AKS (serviço kubernetes do Azure), você deve definir o contexto do cluster com o seguinte comando de CLI do Azure:
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> você deve estar usando CLI do Azure versão 2.0.4 ou posterior. Execute `az --version` para localizar a versão, se necessário.

<sup>3</sup> se você estiver executando no Windows 10, a **rotação** já estará em seu caminho ao executar a partir de um prompt cmd. Para outras versões do Windows, faça  o download da ondulação usando o link e coloque-o em seu caminho.

## <a name="which-tools-are-required"></a>Quais ferramentas são necessárias?

A tabela anterior fornece todas as ferramentas comuns que são usadas com clusters Big Data. Quais ferramentas são necessárias depende do seu cenário. Mas, em geral, as seguintes ferramentas são mais importantes para gerenciar, conectar e consultar o cluster:

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **Extensão SQL Server 2019**

As ferramentas restantes só são necessárias em determinados cenários. **CLI do Azure** pode ser usado para gerenciar os serviços do Azure associados a implantações do AKS. **MSSQL-CLI** é uma ferramenta opcional, mas útil que permite que você se conecte à instância mestra de SQL Server no cluster e execute consultas na linha de comando. E **sqlcmd** e **ondulação** serão necessários se você planeja instalar dados de exemplo com o script do github.

### <a id="python"></a>Instalar Python offline

1. Em um computador com acesso à Internet, baixe um dos seguintes arquivos compactados que contêm Python:

   | Sistema Operacional | Download |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Copie o arquivo compactado no computador de destino e extraia-o para uma pasta de sua escolha.

1. Somente para Windows, execute `installLocalPythonPackages.bat` a partir dessa pasta e passe o caminho completo para a mesma pasta que um parâmetro.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

## <a name="next-steps"></a>Próximas etapas

Depois de configurar as ferramentas, implante um cluster SQL Server 2019 Big Data no kubernetes na nuvem ou no local. Para obter mais informações, consulte os seguintes artigos de implantação:

- [Início Rápido: Implantar SQL Server Cluster de Big Data no serviço de kubernetes do Azure (AKS)](quickstart-big-data-cluster-deploy.md)
- [Como implantar SQL Server clusters de Big Data no kubernetes](deployment-guidance.md)

Para obter mais informações sobre clusters de Big Data, consulte [o que são SQL Server 2019 Big data clusters?](big-data-cluster-overview.md).
