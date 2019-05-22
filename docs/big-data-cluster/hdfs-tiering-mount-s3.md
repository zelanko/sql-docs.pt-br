---
title: Montagem S3 para camadas do HDFS
titleSuffix: SQL Server big data clusters
description: Este artigo explica como configurar o HDFS disposição em camadas para montar um sistema de arquivo externo do S3 no HDFS em um cluster de big data do SQL Server 2019 (visualização).
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4254c1c47e64013533574345c14518fdc2afcb7c
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993954"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>Como montar S3 para o HDFS disposição em camadas em um cluster de big data

As seções a seguir fornecem um exemplo de como configurar o HDFS disposição em camadas com uma fonte de dados do armazenamento de S3.

## <a name="prerequisites"></a>Prerequisites

- [Cluster de big data implantados](deployment-guidance.md)
- [Ferramentas de big data](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**
- Criar e carregar dados para um bucket S3 
  - Carregar CSV ou Parquet arquivos para o bucket S3. Isso é que os dados externos do HDFS que serão montados no HDFS no cluster de big data.

## <a name="access-keys"></a>Chaves de acesso

1. Abra um prompt de comando em um computador cliente que possa acessar seu cluster de big data.

1. Crie um arquivo local chamado **filename.creds** que contém suas credenciais de conta S3 usando o seguinte formato:

   ```text
    fs.s3a.access.key=<Access Key ID of the key>
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > Para obter mais informações sobre como criar chaves de acesso de S3, confira [chaves de acesso do S3](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys).

## <a id="mount"></a> Montar o armazenamento HDFS remoto

Agora que você preparou um arquivo de credencial com chaves de acesso, você pode começar a montagem. As etapas a seguir montagem o armazenamento remoto do HDFS no S3 no armazenamento local de HDFS do seu cluster de big data.

1. Use **kubectl** para localizar o endereço IP para o ponto de extremidade **controlador-svc-externo** serviço em seu cluster de big data. Procure os **External-IP**.

   ```bash
   kubectl get svc controller-svc-external -n <your-cluster-name>
   ```

1. Faça logon com **mssqlctl** usando o endereço IP externo do ponto de extremidade de controlador com seu nome de usuário do cluster e a senha:

   ```bash
   mssqlctl login -e https://<IP-of-controller-svc-external>:30080/
   ```

1. Montar o armazenamento HDFS remoto no Azure usando **mssqlctl montagem do pool de armazenamento do cluster crie**. Substitua os valores de espaço reservado antes de executar o comando a seguir:

   ```bash
   mssqlctl cluster storage-pool mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name> --credential-file <path-to-s3-credentials>/file.creds
   ```

   > [!NOTE]
   > A montagem criar comando é assíncrona. Neste momento, não há nenhuma mensagem que indica se a montagem foi bem-sucedida. Consulte a [status](#status) seção para verificar o status do seu montagens.

Se montado com êxito, você deve ser capaz de consultar os dados do HDFS e executar trabalhos do Spark em relação a ela. Ele aparecerá no HDFS para o cluster de big data no local especificado pelo `--mount-path`.

## <a id="status"></a> Obter o status de montagens

Para listar o status de todas as montagens no seu cluster de big data, use o seguinte comando:

```bash
mssqlctl cluster storage-pool mount status
```

Para listar o status de uma montagem de um caminho específico no HDFS, use o seguinte comando:

```bash
mssqlctl cluster storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> Excluir a montagem

Para excluir a montagem, use o **mssqlctl exclusão de montagem de pool de armazenamento de cluster** de comando e especifique o caminho de montagem no HDFS:

```bash
mssqlctl cluster storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de big data de 2019 do SQL Server, consulte [quais são os clusters do SQL Server 2019 big data?](big-data-cluster-overview.md).
