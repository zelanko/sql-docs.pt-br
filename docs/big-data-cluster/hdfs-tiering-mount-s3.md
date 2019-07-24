---
title: Montagem S3 para camadas do HDFS
titleSuffix: SQL Server big data clusters
description: Este artigo explica como configurar a camada do HDFS para montar um sistema de arquivos S3 externo no HDFS em um cluster SQL Server 2019 Big Data (versão prévia).
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 28c80d6076f07c8a4f1605149f4b5c730c8349a1
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419342"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>Como montar S3 para camadas do HDFS em um cluster Big Data

As seções a seguir fornecem um exemplo de como configurar a disposição em camadas do HDFS com uma fonte de dados de armazenamento S3.

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster Big Data implantado](deployment-guidance.md)
- [Ferramentas de Big data](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**
- Criar e carregar dados para um Bucket S3 
  - Carregue arquivos CSV ou parquet em seu Bucket S3. Estes são os dados de HDFS externos que serão montados no HDFS no cluster Big Data.

## <a name="access-keys"></a>Chaves de acesso

### <a name="set-environment-variable-for-access-key-credentials"></a>Definir variável de ambiente para credenciais de chave de acesso

Abra um prompt de comando em um computador cliente que possa acessar o cluster Big Data. Defina uma variável de ambiente usando o formato a seguir. Observe que as credenciais precisam estar em uma lista separada por vírgulas. O comando ' Set ' é usado no Windows. Se você estiver usando o Linux, use "exportar" em seu lugar.

   ```text
    set MOUNT_CREDENTIALS=fs.s3a.access.key=<Access Key ID of the key>,
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > Para obter mais informações sobre como criar chaves de acesso S3, consulte [chaves de acesso S3](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys).

## <a id="mount"></a>Montar o armazenamento HDFS remoto

Agora que você preparou um arquivo de credencial com chaves de acesso, você pode iniciar a montagem. As etapas a seguir montam o armazenamento HDFS remoto em S3 para o armazenamento HDFS local de seu cluster Big Data.

1. Use **kubectl** para localizar o endereço IP para o serviço controlador de ponto de extremidade **-svc-external** no cluster Big Data. Procure o **IP externo**.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. Faça logon com **azdata** usando o endereço IP externo do ponto de extremidade do controlador com o nome de usuário e a senha do cluster:

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
   
1. Definir a variável de ambiente MOUNT_CREDENTIALS seguindo as instruções acima

1. Monte o armazenamento HDFS remoto no Azure usando o **azdata BDC Storage-Pool Mount criar**. Substitua os valores de espaço reservado antes de executar o seguinte comando:

   ```bash
   azdata bdc storage-pool mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > O comando Mount Create é assíncrono. Neste momento, não há nenhuma mensagem indicando se a montagem foi bem-sucedida. Consulte a seção [status](#status) para verificar o status de suas montagens.

Se montado com êxito, você deve ser capaz de consultar os dados do HDFS e executar trabalhos do Spark em relação a ele. Ele aparecerá no HDFS para o cluster Big Data no local especificado por `--mount-path`.

## <a id="status"></a>Obter o status de montagens

Para listar o status de todas as montagens no cluster Big Data, use o seguinte comando:

```bash
azdata bdc storage-pool mount status
```

Para listar o status de uma montagem em um caminho específico no HDFS, use o seguinte comando:

```bash
azdata bdc storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>Atualizar uma montagem

O exemplo a seguir atualiza a montagem.

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a>Excluir a montagem

Para excluir a montagem, use o comando **azdata BDC Storage-Pool Mount Delete** e especifique o caminho de montagem no HDFS:

```bash
azdata bdc storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters SQL Server de Big Data 2019, consulte [o que são SQL Server Big data clusters de 2019?](big-data-cluster-overview.md).
