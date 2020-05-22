---
title: Montagem S3 para camadas do HDFS
titleSuffix: SQL Server big data clusters
description: Este artigo explica como configurar camadas do HDFS para montar um sistema de arquivos S3 externo no HDFS em um cluster de Big Data do SQL Server 2019.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fce89b5c2ee40fc7229c0c330fefe9e253a4fdc6
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606585"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>Como montar um S3 para camadas do HDFS em um cluster de Big Data

As seções a seguir fornecem um exemplo de como configurar camadas do HDFS com uma fonte de dados de Armazenamento S3.

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster de Big Data implantado](deployment-guidance.md)
- [Ferramentas de Big Data](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**
- Criar e fazer upload de dados em um bucket de S3 
  - Faça upload de arquivos CSV ou Parquet em seu bucket de S3. Estes são os dados do HDFS externos que serão montados no HDFS no cluster de Big Data.

## <a name="access-keys"></a>Chaves de acesso

### <a name="set-environment-variable-for-access-key-credentials"></a>Definir variável de ambiente para credenciais de chave de acesso

Abra um prompt de comando em um computador cliente que possa acessar o cluster de Big Data. Defina uma variável de ambiente usando o formato a seguir. Observe que as credenciais precisam estar em uma lista separada por vírgula. O comando 'set' é usado no Windows. Se estiver usando o Linux, use 'export'.

   ```text
    set MOUNT_CREDENTIALS=fs.s3a.access.key=<Access Key ID of the key>,
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > Para obter mais informações sobre como criar chaves de acesso de S3, consulte [Chaves de acesso de S3](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys).

## <a name="mount-the-remote-hdfs-storage"></a><a id="mount"></a> Montar o armazenamento HDFS remoto

Agora que preparou um arquivo de credencial com chaves de acesso, você pode iniciar a montagem. As etapas a seguir montam o armazenamento HDFS remoto no S3 no armazenamento HDFS local de seu cluster de Big Data.

1. Use **kubectl** para localizar o endereço IP do serviço **controller-svc-external** do ponto de extremidade em seu cluster de Big Data. Procure **External-IP**.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. Faça logon com **azdata** usando o endereço IP externo do ponto de extremidade do controlador com o nome de usuário e a senha do cluster:

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
   
1. Defina a variável de ambiente MOUNT_CREDENTIALS seguindo as instruções acima

1. Monte o armazenamento HDFS remoto no Azure usando **azdata bdc hdfs mount create**. Substitua os valores de espaço reservado antes de executar o seguinte comando:

   ```bash
   azdata bdc hdfs mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > O comando mount create é assíncrono. Neste momento, não há nenhuma mensagem indicando se a montagem foi bem-sucedida. Confira a seção [status](#status) para verificar o status das montagens.

Se a montagem tiver sido bem-sucedida, você poderá consultar os dados do HDFS e executar trabalhos do Spark com eles. Ela será exibida no HDFS do cluster de Big Data na localização especificada por `--mount-path`.

## <a name="get-the-status-of-mounts"></a><a id="status"></a> Obter o status das montagens

Para listar o status de todas as montagens no cluster de Big Data, use o seguinte comando:

```bash
azdata bdc hdfs mount status
```

Para listar o status de uma montagem em um caminho específico no HDFS, use o seguinte comando:

```bash
azdata bdc hdfs mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>Atualizar uma montagem

O exemplo a seguir atualiza a montagem.

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a name="delete-the-mount"></a><a id="delete"></a> Excluir a montagem

Para excluir a montagem, use o comando **azdata bdc hdfs mount delete** e especifique o caminho da montagem no HDFS:

```bash
azdata bdc hdfs mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
