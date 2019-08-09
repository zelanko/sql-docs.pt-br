---
title: Montagem S3 para camadas do HDFS
titleSuffix: SQL Server big data clusters
description: Este artigo explica como configurar camadas do HDFS para montar um sistema de arquivos S3 externo no HDFS em um cluster de Big Data do SQL Server 2019 (versão prévia).
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/31/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 10e7d0e30135622fedfcbe8f8dba67bfaf1908cd
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702872"
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

## <a id="mount"></a> Montar o armazenamento HDFS remoto

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

1. Monte o armazenamento HDFS remoto no Azure usando **azdata bdc storage-pool mount create**. Substitua os valores de espaço reservado antes de executar o seguinte comando:

   ```bash
   azdata bdc storage-pool mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > O comando mount create é assíncrono. Neste momento, não há nenhuma mensagem indicando se a montagem foi bem-sucedida. Confira a seção [status](#status) para verificar o status das montagens.

Se a montagem tiver sido bem-sucedida, você poderá consultar os dados do HDFS e executar trabalhos do Spark com eles. Ela será exibida no HDFS do cluster de Big Data na localização especificada por `--mount-path`.

## <a id="status"></a> Obter o status das montagens

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

## <a id="delete"></a> Excluir a montagem

Para excluir a montagem, use o comando **azdata bdc storage-pool mount delete** e especifique o caminho da montagem no HDFS:

```bash
azdata bdc hdfs mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data do SQL Server 2019, confira [O que são clusters de Big Data do SQL Server 2019?](big-data-cluster-overview.md).
