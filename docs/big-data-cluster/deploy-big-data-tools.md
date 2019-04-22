---
title: Instalar ferramentas de Big Data
titleSuffix: SQL Server big data clusters
description: Saiba como instalar as ferramentas usadas com clusters de big data de 2019 do SQL Server (versão prévia).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: dc53bdfb71efeafd55752686ff136355bc79bd34
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860477"
---
# <a name="install-sql-server-2019-big-data-tools"></a>Instalar ferramentas do SQL Server 2019 big data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve as ferramentas de cliente que devem ser instaladas para criar, gerenciar, e usando o SQL Server 2019 clusters de big data (visualização). A seção a seguir fornece uma lista de ferramentas e links para instruções de instalação. Antes de implantar um cluster de big data, configure as ferramentas marcado como obrigatório no Windows ou Linux.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>Ferramentas de cluster de big data

A tabela a seguir lista as ferramentas de cluster de big data comuns e como instalá-los:

| Ferramenta | Obrigatório | Descrição | Instalação |
|---|---|---|---|
| **mssqlctl** | Sim | Ferramenta de linha de comando para instalar e gerenciar um cluster de big data. | [Instalar](deploy-install-mssqlctl.md) |
| **kubectl**<sup>1</sup> | Sim | Ferramenta de linha de comando para monitorar o cluster Kuberentes subjacente ([saber](https://kubernetes.io/docs/tasks/tools/install-kubectl/)). | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio** | Sim | Plataforma cruzada a ferramenta gráfica para consultar o SQL Server ([saber](https://docs.microsoft.com/sql/azure-data-studio/what-is?view=sql-server-ver15)). | [Instalar](../azure-data-studio/download.md) |
| **Extensão do SQL Server de 2019** | Sim | Extensão do Studio de dados do Azure que dá suporte à conexão para o cluster de big data. Também fornece um Assistente de virtualização de dados. | [Instalar](../azure-data-studio/sql-server-2019-extension.md) |
| **CLI do Azure**<sup>2</sup> | Para o AKS | Interface de linha de comando moderna para gerenciar os serviços do Azure. Usado com implantações de cluster do AKS big data ([saber](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)). | [Instalar](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | Opcional | Interface de linha de comando moderna para consultar o SQL Server ([saber](https://github.com/dbcli/mssql-cli/blob/master/README.rst)). | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | Para alguns scripts | Ferramenta de linha de comando herdada para consultar o SQL Server ([saber](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15)). | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | Para alguns scripts | Ferramenta de linha de comando para transferir dados com URLs. | [Windows](https://curl.haxx.se/windows/) \| Linux: pacote de instalação do curl |

<sup>1</sup> você deve usar kubectl versão 1,10 ou posterior. Além disso, a versão do kubectl deve ser mais ou menos de uma versão secundária do seu cluster Kubernetes. Se você quiser instalar uma versão específica no cliente kubectl, consulte [instalar kubectl binário por meio de rotação](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) (no Windows 10, use cmd.exe e não o Windows PowerShell para executar a rotação). 

> [!TIP]
> Para usar o kubectl com um cluster implantado anteriormente no serviço de Kubernetes do Azure (AKS), você deve definir o contexto do cluster com o seguinte comando da CLI do Azure:
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> você deve estar usando a CLI do Azure versão 2.0.4 ou posterior. Executar `az --version` para localizar a versão, se necessário.

<sup>3</sup> se você estiver executando no Windows 10 **curl** já está em seu caminho quando em execução em um prompt de comando. Para outras versões do Windows, baixe **curl** usando o link e coloque-o em seu caminho.

## <a name="which-tools-are-required"></a>Quais ferramentas são necessárias?

A tabela anterior fornece todas as ferramentas comuns que são usadas com clusters de big data. Quais ferramentas são necessárias depende do seu cenário. Mas, em geral, as seguintes ferramentas são mais importantes para gerenciar, conectar-se a e consultar o cluster:

- **mssqlctl**
- **kubectl**
- **Azure Data Studio**
- **Extensão do SQL Server de 2019**

As ferramentas restantes são necessários apenas em determinados cenários. **CLI do Azure** pode ser usado para gerenciar os serviços do Azure associados com implantações do AKS. **MSSQL-cli** é uma ferramenta opcional mas útil que permite que você se conecte à instância mestre do SQL Server no cluster e executar consultas da linha de comando. E **sqlcmd** e **curl** são necessários se você planeja instalar dados de exemplo com o script do GitHub.

## <a name="next-steps"></a>Próximas etapas

Depois de configurar as ferramentas, implante um cluster de big data do SQL Server 2019 para Kubernetes na nuvem ou local. Para obter mais informações, consulte os seguintes artigos de implantação:

- [Guia de início rápido: Implantar um cluster de big data do SQL Server no serviço de Kubernetes do Azure (AKS)](quickstart-big-data-cluster-deploy.md)
- [Como implantar clusters de grandes dados do SQL Server no Kubernetes](deployment-guidance.md)

Para obter mais informações sobre clusters de big data, consulte [quais são os clusters do SQL Server 2019 big data?](big-data-cluster-overview.md).
