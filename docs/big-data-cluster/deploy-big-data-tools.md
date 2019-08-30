---
title: Instalar ferramentas de Big Data
titleSuffix: SQL Server big data clusters
description: Saiba como instalar ferramentas usadas com [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] o (Preview).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 84c7181bfd7c0ee014b382052bb6493d68251331
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153607"
---
# <a name="install-sql-server-2019-big-data-tools"></a>Instalar as ferramentas de Big Data do SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve as ferramentas de cliente que devem ser instaladas para criar, gerenciar e [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] usar o (Preview). A seção a seguir fornece uma lista de ferramentas e links para instruções de instalação. Antes de implantar um cluster de Big Data, configure as ferramentas marcadas como necessárias no Windows ou no Linux.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>Ferramentas de cluster de Big Data

A seguinte tabela lista as ferramentas comuns de cluster de Big Data e como instalá-las:

| Ferramenta | Obrigatório | Descrição | Instalação |
|---|---|---|---|
| **python** | Sim | O Python é uma linguagem de programação de alto nível interpretada e orientada a objeto com semântica dinâmica. Muitas partes dos clusters de Big Data do SQL Server usam o Python. | [Instalar o Python](#python)|
| **azdata** | Sim | Ferramenta de linha de comando para instalar e gerenciar um cluster de Big Data. | [Instalar](deploy-install-azdata.md) |
| **kubectl**<sup>1</sup> | Sim | Ferramenta de linha de comando para monitorar o cluster do Kubernetes subjacente ([mais informações](https://kubernetes.io/docs/tasks/tools/install-kubectl/)). | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio-SQL Server Release Candidate 2019 (RC)** | Sim | Ferramenta gráfica de plataforma cruzada para consultar SQL Server. | [Instalar](#download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc) |
| **Extensão do SQL Server 2019** | Sim | Extensão do Azure Data Studio que dá suporte à conexão com o cluster de Big Data. Também fornece um assistente de Virtualização de Dados. | [Instalar](../azure-data-studio/sql-server-2019-extension.md) |
| **CLI do Azure**<sup>2</sup> | Para o AKS | Interface de linha de comando moderna para gerenciar serviços do Azure. Usada com implantações de cluster de Big Data do AKS ([mais informações](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)). | [Instalar](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | Opcional | Interface de linha de comando moderna para consulta do SQL Server ([mais informações](https://github.com/dbcli/mssql-cli/blob/master/README.rst)). | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | Para alguns scripts | Ferramenta de linha de comando herdada para consulta do SQL Server ([mais informações](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15)). | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | Para alguns scripts | Ferramenta de linha de comando para transferência de dados com URLs. | [Windows](https://curl.haxx.se/windows/) \| Linux: instalar pacote do curl |

<sup>1</sup> É necessário usar o kubectl versão 1.10 ou posterior. Além disso, a versão do kubectl deve estar acima ou abaixo de uma versão secundária do cluster do Kubernetes. Caso deseje instalar uma versão específica no cliente do kubectl, confira [Instalar o binário do kubectl por meio do curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) (no Windows 10, use cmd.exe e não o Windows PowerShell para executar o curl).

> [!TIP]
> Para usar o kubectl com um cluster implantado anteriormente no AKS (Serviço de Kubernetes do Azure), é necessário definir o contexto do cluster com o seguinte comando da CLI do Azure:
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> É necessário estar usando a CLI do Azure versão 2.0.4 ou posterior. Execute `az --version` para localizar a versão, se necessário.

<sup>3</sup> Caso esteja executando-a no Windows 10, o **curl** já estará no CAMINHO ao executar em um prompt de comando. Para outras versões do Windows, baixe o **curl** usando o link e coloque-o no CAMINHO.

## <a name="which-tools-are-required"></a>Quais ferramentas são necessárias?

A tabela anterior fornece todas as ferramentas comuns que são usadas com clusters de Big Data. As ferramentas que são necessárias dependem do cenário. Mas, em geral, as seguintes ferramentas são mais importantes para gerenciar, conectar e consultar o cluster:

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **Extensão do SQL Server 2019**

As ferramentas restantes só são necessárias em determinados cenários. A **CLI do Azure** pode ser usada para gerenciar os serviços do Azure associados a implantações do AKS. **mssql-cli** é uma ferramenta opcional, mas útil, que permite que você se conecte à instância mestra do SQL Server no cluster e execute consultas na linha de comando. O **sqlcmd** e o **curl** são necessários se você planeja instalar dados de exemplo com o script do GitHub.

### <a id="python"></a> Instalar o Python offline

1. Em um computador com acesso à Internet, baixe um dos seguintes arquivos compactados que contêm o Python:

   | Sistema operacional | Download |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. Copie o arquivo compactado para o computador de destino e extraia-o em uma pasta de sua escolha.

1. Somente para o Windows, execute `installLocalPythonPackages.bat` nessa pasta e passe o caminho completo para a mesma pasta como um parâmetro.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

## <a name="download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc"></a>Baixe e instale o Azure Data Studio SQL Server 2019 Release Candidate (RC)

Azure Data Studio SQL Server 2019 RC fornece recursos e recursos especificamente para SQL Server 2019 RC.

Para versões normais de produção do Azure Data Studio, siga as instruções em [baixar e instalar o Azure Data Studio](../azure-data-studio/download.md).

|Plataforma|Download|Data de liberação| Versão |
|:---|:---|:---|:---|
|Windows|[Instalador do usuário (recomendado)](https://go.microsoft.com/fwlink/?linkid=2102435)<br>[Instalador do sistema](https://go.microsoft.com/fwlink/?linkid=2102523)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2102524)|27 de agosto de 2019 |1\.11.0 de RC – pessoas internas|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2102436)|27 de agosto de 2019 |1\.11.0 de RC – pessoas internas|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2102526)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2102437)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2102525)|27 de agosto de 2019 |1\.11.0 de RC – pessoas internas|

Para obter detalhes sobre a versão mais recente, consulte as [notas de versão](../big-data-cluster/release-notes-big-data-cluster.md).

### <a name="get-azure-data-studio-for-windows"></a>Obter o Azure Data Studio para Windows

Esta versão do [!INCLUDE[name-sos](../includes/name-sos-short.md)] inclui uma experiência padrão do Windows Installer e um arquivo .zip.

O *instalador do usuário* é recomendado porque não exige privilégios de administrador, o que simplifica as instalações e as atualizações. O instalador do usuário não exige privilégios de administrador, pois a localização está na pasta AppData Local (LOCALAPPDATA) do usuário. O instalador do usuário também fornece uma experiência de atualização em segundo plano mais tranquila. Para obter mais informações, confira [Configuração de usuário para Windows](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows).

**Instalador do usuário** (recomendado)

1. Baixe e execute o [instalador do *usuário* do [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Windows](https://go.microsoft.com/fwlink/?linkid=2102435).
2. Inicie o aplicativo [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].

**Instalador do sistema**

1. Baixe e execute o [instalador do *sistema* do [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Windows](https://go.microsoft.com/fwlink/?linkid=2102523).
2. Inicie o aplicativo [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].

**arquivo zip**

1. Baixe o [arquivo .zip do [!INCLUDE[name-sos](../includes/name-sos-short.md)] para o Windows](https://go.microsoft.com/fwlink/?linkid=2102524).
2. Navegue até o arquivo baixado e o extraia.
3. Execute `\azuredatastudio-windows\azuredatastudio.exe`

### <a name="get-azure-data-studio-for-macos"></a>Obtenha o Azure Data Studio para macOS

1. Baixe o [[!INCLUDE[name-sos](../includes/name-sos-short.md)] para macOS](https://go.microsoft.com/fwlink/?linkid=2102436).
2. Para expandir o conteúdo do zip, clique duas vezes nele.
3. Para disponibilizar o [!INCLUDE[name-sos](../includes/name-sos-short.md)] no *Launchpad*, arraste *Azure Data Studio.app* para a pasta *Aplicativos*.

### <a name="get-azure-data-studio-for-linux"></a>Obtenha o Azure Data Studio para Linux

1. Baixe o [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Linux usando um dos instaladores ou o arquivo morto gz:
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2102526)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2102437)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2102525)
1. Para extrair o arquivo e inicializá-lo [!INCLUDE[name-sos](../includes/name-sos-short.md)], abra uma nova janela do Terminal e digite os seguintes comandos:

   **Instalação do Debian:**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/azuredatastudio-linux-<version string>.deb

   azuredatastudio
   ```

   **Instalação do RPM:**
   ```bash
   cd ~
   yum install ./Downloads/azuredatastudio-linux-<version string>.rpm

   azuredatastudio
   ```

   **instalação gz:**
   ```bash 
   cd ~ 
   cp ~/Downloads/azuredatastudio-linux-<version string>.tar.gz ~ 
   tar -xvf ~/azuredatastudio-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/azuredatastudio-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   azuredatastudio 
   ``` 

   > [!NOTE]
   > No Debian, Redhat e Ubuntu, você pode ter dependências ausentes. Use os seguintes comandos para instalar estas dependências, de acordo com sua versão do Linux:
   

   **Debian:** 
   ```bash
   sudo apt-get install libunwind8
   ```

   **Red Hat:** 
   ```bash
   yum install libXScrnSaver
   ```

   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```

### <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

[!INCLUDE[name-sos](../includes/name-sos-short.md)] pode ser executado no Windows, macOS e Linux e é suportado nas seguintes plataformas:

#### <a name="windows"></a>Windows

- Windows 10 (64 bits)
- Windows 8.1 (64 bits)
- Windows 8 (64 bits)
- Windows 7 (SP1) (64 bits) – exige o [KB2533623](https://www.microsoft.com/download/details.aspx?id=26767)
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2 (64 bits)
- Windows Server 2012 (64 bits)
- Windows Server 2008 R2 (64 bits)

#### <a name="macos"></a>macOS

- macOS 10.13 High Sierra
- macOS 10.12 Sierra

#### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>Próximas etapas

Depois de configurar as ferramentas, implante um cluster de Big Data do SQL Server 2019 no Kubernetes na nuvem ou localmente. Para obter mais informações, confira os seguintes artigos sobre implantação:

- [Início Rápido: Implantar um cluster de Big Data do SQL Server no AKS (Serviço de Kubernetes do Azure)](quickstart-big-data-cluster-deploy.md)
- [Como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] o no kubernetes](deployment-guidance.md)

Para obter mais informações sobre clusters de Big Data, consulte [o que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
