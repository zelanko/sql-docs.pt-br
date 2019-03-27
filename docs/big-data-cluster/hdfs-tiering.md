---
title: Configurar a disposição em camadas do HDFS
titleSuffix: SQL Server 2019 big data clusters
description: Este artigo explica como configurar o HDFS disposição em camadas para montar um sistema de arquivo externo do armazenamento do Azure Data Lake no HDFS em um cluster de big data do SQL Server 2019 (visualização).
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: craigg
ms.date: 03/27/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1199d8d522df83c626f04f30c8937b57a5359f5c
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493768"
---
# <a name="configure-hdfs-tiering-on-sql-server-2019-big-data-clusters"></a>Configurar camadas em clusters do SQL Server 2019 grandes dados do HDFS

Disposição em camadas HDFS fornece a capacidade de montar externa, sistema de arquivos compatível com HDFS no HDFS. Este artigo explica como configurar o HDFS disposição em camadas para clusters de big data de 2019 do SQL Server (versão prévia). Neste momento, o CTP 2.4 suporta apenas conectar-se ao Azure Data Lake armazenamento Gen2, que é o foco deste artigo.

## <a name="hdfs-tiering-overview"></a>Visão geral de disposição em camadas do HDFS

Com a disposição em camadas, aplicativos podem acessar diretamente dados em uma variedade de armazenamentos externos como se os dados residem no HDFS. Montagem é uma operação de metadados, em que os metadados que descreve o namespace no sistema de arquivo externo é copiado para o HDFS. Esses metadados incluem informações sobre os diretórios externos e arquivos junto com suas permissões e ACLs. Os dados correspondentes são apenas copiada sob demanda, quando os dados em si são acessados. Os dados do sistema de arquivo externo agora podem ser acessados do cluster de big data do SQL Server. Você pode executar o Spark trabalhos e consultas SQL sobre esses dados da mesma forma que você executaria em todos os dados locais armazenados em HDFS no cluster.

> [!NOTE]
> HDFS disposição em camadas é um recurso desenvolvido pela Microsoft e uma versão anterior dele foi lançada como parte da distribuição do Apache Hadoop 3.1. Para obter mais informações, consulte [ https://issues.apache.org/jira/browse/HDFS-9806 ](https://issues.apache.org/jira/browse/HDFS-9806) para obter detalhes.

As seções a seguir fornecem um exemplo de como configurar o HDFS disposição em camadas com uma fonte de dados do armazenamento do Azure Data Lake Gen2.

## <a name="prerequisites"></a>Prerequisites

- [Cluster de big data implantados](deployment-guidance.md)
- [Ferramentas de big data](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**

## <a id="load"></a> Carregar dados no armazenamento do Azure Data Lake

A seção a seguir descreve como configurar o Azure Data Lake armazenamento Gen2 para testar a disposição em camadas do HDFS. Se você já tiver dados armazenados no armazenamento do Azure Data Lake, você pode ignorar esta seção para usar seus próprios dados.

1. [Criar uma conta de armazenamento com os recursos do Data Lake armazenamento Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account).

1. [Criar um contêiner de blob](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal) nessa conta de armazenamento para os dados externos.

1. Carrega um arquivo CSV ou Parquet no contêiner. Isso é que os dados externos do HDFS que serão montados no HDFS no cluster de big data.

## <a id="mount"></a> Montar o armazenamento HDFS remoto

As etapas a seguir montagem o armazenamento remoto do HDFS no Azure Data Lake no armazenamento local de HDFS do seu cluster de big data.

1. Abra um prompt de comando em um computador cliente que possa acessar seu cluster de big data.

1. Crie um arquivo local chamado **files.creds** que contém suas credenciais de conta de armazenamento do Azure Data Lake Gen2 usando o seguinte formato:

   ```text
   fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

   > [!TIP]
   > Para obter mais informações sobre como localizar a chave de acesso (`<storage-account-access-key>`) para sua conta de armazenamento, consulte [exibir e copiar chaves de acesso](https://docs.microsoft.com/azure/storage/common/storage-account-manage?#view-and-copy-access-keys).

1. Use **kubectl** para localizar o endereço IP para o **ponto de extremidade de serviço de proxy** serviço em seu cluster de big data. Procure os **External-IP**.

   ```bash
   kubectl get svc endpoint-service-proxy -n <your-cluster-name>
   ```

1. Faça logon com **mssqlctl** usando o ponto de extremidade de proxy de serviço com o nome de usuário do cluster e a senha:

   ```bash
   mssqlctl login -e https://<IP-of-endpoint-service-proxy>:30777/ -u <username> -p <password>
   ```

1. Montar o armazenamento HDFS remoto no Azure usando **montagem do armazenamento mssqlctl criar**. Substitua os valores de espaço reservado antes de executar o comando a seguir:

   ```bash
   mssqlctl storage mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name> --credential-file <path-to-adls-credentials>/file.creds
   ```

   > [!NOTE]
   > A montagem criar comando é assíncrona. Neste momento, não há nenhuma mensagem que indica se a montagem foi bem-sucedida. Consulte a [status](#status) seção para verificar o status do seu montagens.

Se montado com êxito, você deve ser capaz de consultar os dados do HDFS e executar trabalhos do Spark em relação a ela. Ele aparecerá no HDFS para o cluster de big data no local especificado pelo `--local-path`.

## <a id="status"></a> Obter o status de montagens

Para listar o status de todas as montagens no seu cluster de big data, use o seguinte comando:

```bash
mssqlctl storage mount status
```

Para listar o status de uma montagem de um caminho específico no HDFS, use o seguinte comando:

```bash
mssqlctl storage mount status --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> Excluir a montagem

Para excluir a montagem, use o **mssqlctl armazenamento montagem exclusão** de comando e especifique o caminho de montagem no HDFS:

```bash
mssqlctl storage mount delete --mount-path <mount-path-in-hdfs>
```

## <a id="issues"></a> Limitações e problemas conhecidos

A lista a seguir fornece os problemas conhecidos e limitações atuais ao usar HDFS disposição em camadas em clusters de grandes dados do SQL Server:

- Se o tamanho do diretório externo que está sendo montado for maior que a capacidade do cluster, montagem falhará.

- Se a montagem estiver preso em um `CREATING` de estado por um longo tempo, que provavelmente tenha falhado. Nessa situação, cancelar o comando e excluir a montagem, se necessário. Verificar se seus parâmetros e as credenciais estão corretas antes de tentar novamente.

- Não não possível criar montagens de diretórios existentes.

- Não não possível criar montagens dentro de montagens existentes.

- Se qualquer um dos ancestrais do ponto de montagem não existir, serão criados com as permissões padronizada para r xr xr-x (555).

- Criação de montagem pode levar algum tempo dependendo do número e tamanho dos arquivos que está sendo montado. Durante esse processo, os arquivos de montagem não são visíveis aos usuários. Enquanto a montagem é criada, todos os arquivos serão adicionados a um caminho temporário, cujo padrão é `/_temporary/_mounts/<mount-location>`.

- O comando de criação de montagem é assíncrono. Depois que o comando é executado, o status de montagem pode ser verificado para entender o estado da montagem.

- Ao criar a montagem, o argumento usado para **– caminho de local** é essencialmente um identificador exclusivo da montagem. A mesma cadeia de caracteres (incluindo o "/" no final, se presente) deve ser usada em comandos subsequentes.

- As montagens são somente leitura. Você não pode criar os diretórios ou arquivos em uma montagem.

- Não recomendamos diretórios de montagem e arquivos que podem ser alterados. Depois que a montagem é criada, quaisquer alterações ou atualizações para o local remoto não serão refletidas na montagem no HDFS. Se houver alterações no local remoto, você pode optar por excluir e recriar a montagem para refletir o estado atualizado.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de big data de 2019 do SQL Server, consulte [quais são os clusters do SQL Server 2019 big data?](big-data-cluster-overview.md).
