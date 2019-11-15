---
title: Atualizar para uma nova versão
titleSuffix: SQL Server Big Data Clusters
description: Saiba como atualizar Clusters de Big Data do SQL Server para uma nova versão.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f44ef17a712d0d5a19707cf94e7d3e4196a2aba3
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706306"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Como atualizar o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo fornece diretrizes sobre como atualizar um cluster de Big Data do SQL Server para uma nova versão. As etapas neste artigo se aplicam especificamente a como atualizar de uma versão prévia para a versão de atualização de serviço do SQL Server 2019.

## <a name="backup-and-delete-the-old-cluster"></a>Fazer backup e excluir o cluster antigo

No momento, não há nenhuma atualização in-loco para clusters de Big Data. A única maneira de atualizar para uma nova versão é remover manualmente e recriar o cluster. Cada versão tem uma versão exclusiva do `azdata` que não é compatível com a versão anterior. Além disso, se um cluster mais antigo precisar baixar uma imagem de contêiner em um novo nó, a imagem mais recente poderá não ser compatível com as imagens mais antigas no cluster. Observe que a imagem mais nova será capturada somente se você estiver usando a tag de imagem `latest` para no arquivo de configuração de implantação para as configurações do contêiner. Por padrão, cada versão tem uma tag de imagem específica correspondente à versão de lançamento do SQL Server. Para fazer a atualização para a última versão, use as seguintes etapas:

1. Antes de excluir o cluster antigo, faça backup dos dados na instância mestra do SQL Server e no HDFS. Para a instância mestra do SQL Server, você poderá usar [Backup e restauração do SQL Server](data-ingestion-restore-database.md). Para o HDFS, você [pode copiar os dados com o `curl`](data-ingestion-curl.md).

1. Exclua o cluster antigo com o comando `azdata delete cluster`.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > Use a versão do `azdata` que corresponde ao cluster. Não exclua um cluster mais antigo com a versão mais recente do `azdata`.

   > [!Note]
   > A emissão de um comando `azdata bdc delete` resultará em todos os objetos criados dentro do namespace identificado com o nome do cluster de Big Data serem excluídos, mas não o próprio namespace. O namespace pode ser reutilizado para implantações subsequentes, desde que esteja vazio e nenhum outro aplicativo tenha sido criado dentro dele.

1. Desinstalar a versão antiga do `azdata`

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. Instalar a versão mais recente do `azdata`. Os comandos a seguir instalam `azdata` da versão mais recente:

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux:**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > Para cada versão, o caminho para a versão `n-1` do `azdata` muda. Mesmo que você tenha instalado o `azdata` anteriormente, precisará reinstalar com base no caminho mais recente antes de criar o cluster.

## <a id="azdataversion"></a> Verificar a versão do azdata

Antes de implantar um novo cluster de Big Data, verifique se você está usando a última versão do `azdata` com o parâmetro `--version`:

```bash
azdata --version
```

## <a name="install-the-new-release"></a>Instalar a nova versão

Depois de remover o cluster de Big Data anterior e instalar o `azdata` mais recente, implante o novo cluster de Big Data usando as instruções de implantação atuais. Para obter mais informações, confira [Como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md). Em seguida, restaure os bancos de dados ou os arquivos necessários.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md).
