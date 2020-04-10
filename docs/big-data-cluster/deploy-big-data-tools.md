---
title: Instalar ferramentas de Big Data
titleSuffix: SQL Server big data clusters
description: Saiba como instalar ferramentas usadas com [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 77acaa43c1360c1f5d1126f46b5d79dc6d74b4ce
ms.sourcegitcommit: 335d27d0493ddf4ffb770e13f8fe8802208d25ae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2020
ms.locfileid: "81002705"
---
# <a name="install-sql-server-2019-big-data-tools"></a>Instalar as ferramentas de Big Data do SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve as ferramentas de cliente que devem ser instaladas para criar, gerenciar e usar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. A seção a seguir fornece uma lista de ferramentas e links para instruções de instalação. Antes de implantar um cluster de Big Data, configure as ferramentas marcadas como necessárias no Windows ou no Linux.

## <a name="big-data-cluster-tools"></a>Ferramentas de cluster de Big Data

A seguinte tabela lista as ferramentas comuns de cluster de Big Data e como instalá-las:

| Ferramenta | Obrigatório | Descrição | Instalação |
|---|---|---|---|
| `python` | Sim | O Python é uma linguagem de programação de alto nível interpretada e orientada a objeto com semântica dinâmica. Muitas partes dos clusters de Big Data do SQL Server usam o Python. | [Instalar o Python](#python)|
| `azdata` | Sim | Ferramenta de linha de comando para instalar e gerenciar um cluster de Big Data. | [Instalar](deploy-install-azdata.md) |
| `kubectl`<sup>1</sup> | Sim | Ferramenta de linha de comando para monitorar o cluster do Kubernetes subjacente ([mais informações](https://kubernetes.io/docs/tasks/tools/install-kubectl/)). | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-using-native-package-management) |
| **Azure Data Studio** | Sim | Ferramenta gráfica multiplataforma para consultar o SQL Server. | [Instalar](https://aka.ms/getazuredatastudio) |
| **Extensão de Virtualização de Dados** | Sim | Extensão para o Azure Data Studio que fornece um assistente de Virtualização de Dados. | [Instalar](../azure-data-studio/data-virtualization-extension.md) |
| **CLI do Azure**<sup>2</sup> | Para o AKS | Interface de linha de comando moderna para gerenciar serviços do Azure. Usada com implantações de cluster de Big Data do AKS ([mais informações](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)). | [Instalar](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | Opcional | Interface de linha de comando moderna para consulta do SQL Server ([mais informações](../tools/mssql-cli.md)). | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | Para alguns scripts | Ferramenta de linha de comando herdada para consulta do SQL Server ([mais informações](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15)). Talvez seja necessário instalar o Microsoft ODBC Driver 11 for SQL Server antes de instalar o pacote SQLCMD. | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| `curl` <sup>3</sup> | Para alguns scripts | Ferramenta de linha de comando para transferência de dados com URLs. | [Windows](https://curl.haxx.se/windows/) \| Linux: instalar pacote do curl |

<sup>1</sup> É necessário usar o `kubectl` versão 1.13 ou posterior. Além disso, a versão do `kubectl` deve estar acima ou abaixo de uma versão secundária do cluster do Kubernetes. Caso deseje instalar uma versão específica no cliente do `kubectl`, confira [Instalar o binário do `kubectl` por meio da ondulação](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) (no Windows 10, use cmd.exe e não o Windows PowerShell para executar a ondulação).

> [!TIP]
> Para usar o `kubectl` com um cluster implantado anteriormente no AKS (Serviço de Kubernetes do Azure), é necessário definir o contexto do cluster com o seguinte comando da CLI do Azure:
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> É necessário estar usando a CLI do Azure versão 2.0.4 ou posterior. Execute `az --version` para localizar a versão, se necessário.

<sup>3</sup> Caso esteja executando-a no Windows 10, o `curl` já estará no CAMINHO ao executar em um prompt de comando. Para outras versões do Windows, baixe o `curl` usando o link e coloque-o no CAMINHO.

## <a name="which-tools-are-required"></a>Quais ferramentas são necessárias?

A tabela anterior fornece todas as ferramentas comuns que são usadas com clusters de Big Data. As ferramentas que são necessárias dependem do cenário. Mas, em geral, as seguintes ferramentas são mais importantes para gerenciar, conectar e consultar o cluster:

- `azdata`
- `kubectl`
- **Azure Data Studio**
- **Extensão de Virtualização de Dados**

As ferramentas restantes só são necessárias em determinados cenários. A **CLI do Azure** pode ser usada para gerenciar os serviços do Azure associados a implantações do AKS. **mssql-cli** é uma ferramenta opcional, mas útil, que permite que você se conecte à instância mestra do SQL Server no cluster e execute consultas na linha de comando. O **sqlcmd** e o `curl` são necessários se você planeja instalar dados de exemplo com o script do GitHub.

### <a name="install-python-offline"></a><a id="python"></a> Instalar o Python offline

1. Em um computador com acesso à Internet, baixe um dos seguintes arquivos compactados que contêm o Python:

   | Sistema operacional | Baixar |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Copie o arquivo compactado para o computador de destino e extraia-o em uma pasta de sua escolha.

1. Somente para o Windows, execute `installLocalPythonPackages.bat` nessa pasta e passe o caminho completo para a mesma pasta como um parâmetro.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

## <a name="download-and-install-azure-data-studio"></a>Baixar e instalar o Azure Data Studio

O Azure Data Studio fornece recursos e funcionalidades especificamente para Clusters de Big Data do SQL Server.

[Obter o Azure Data Studio mais recente](https://aka.ms/getazuredatastudio).

Para obter detalhes sobre a versão mais recente, confira as [notas sobre a versão](../big-data-cluster/release-notes-big-data-cluster.md).

## <a name="next-steps"></a>Próximas etapas

Depois de configurar as ferramentas, implante um cluster de Big Data do SQL Server 2019 no Kubernetes na nuvem ou localmente. Para obter mais informações, confira os seguintes artigos sobre implantação:

- [Início Rápido: Implantar um cluster de Big Data do SQL Server no AKS (Serviço de Kubernetes do Azure)](quickstart-big-data-cluster-deploy.md)
- [Como implantar o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md)

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
