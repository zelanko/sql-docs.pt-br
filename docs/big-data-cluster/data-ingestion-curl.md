---
title: Use a rotação para carregar dados no HDFS | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: Use curl para carregar dados no HDFS em clusters de Big Data do SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ae893bb1e291b244b5101ccfb2ed66bcf765f049
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866849"
---
# <a name="use-curl-to-load-data-into-hdfs-on-big-data-clusters-2019"></a>Usar curl para carregar dados no HDFS no [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo explica como usar **curl** para carregar dados no HDFS no [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].

## <a name="prerequisites"></a><a id="prereqs"></a> Pré-requisitos

- [Carregar dados de exemplo em seu cluster de Big Data](tutorial-load-sample-data.md)

## <a name="obtain-the-service-external-ip"></a>Obter o IP externo do serviço

WebHDFS é iniciado quando a implantação é concluída e seu acesso passa pelo Knox. O ponto de extremidade do Knox é exposto por meio de um serviço do Kubernetes chamado **gateway-svc-external**.  Para criar a URL de WebHDFS necessária para fazer upload/baixar arquivos, você precisa do endereço IP externo do serviço **gateway-svc-external** e do nome do cluster de Big Data. Você pode obter o endereço IP externo do serviço **gateway-svc-external** executando o seguinte comando:

```terminal
kubectl get service gateway-svc-external -n <big data cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> O `<big data cluster name>` aqui está o nome do cluster que você especificou no arquivo de configuração de implantação. O nome padrão é `mssql-cluster`.

## <a name="construct-the-url-to-access-webhdfs"></a>Construir a URL para acessar o WebHDFS

Agora, você pode construir a URL para acessar o WebHDFS da seguinte maneira:

`https://<gateway-svc-external service external IP address>:30443/gateway/default/webhdfs/v1/`

Por exemplo:

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="authentication-with-active-directory"></a>Autenticação com o Active Directory

Para implantações com o Active Directory, use o parâmetro de autenticação com `curl` com a autenticação Negociate. 

Para usar `curl` com a autenticação do Active Directory, execute este comando:

```
kinit <username>
```

O comando gera um token Kerberos para uso do `curl`. Os comandos demonstrados nas próximas seções especificam o parâmetro `--anyauth` para `curl`. Para as URLs que exigem a autenticação Negociate, o `curl` detecta e usa automaticamente o token Kerberos gerado em vez do nome de usuário e da senha para autenticação nas URLs.

## <a name="list-a-file"></a>Listar um arquivo

Para listar o arquivo em **hdfs:///product_review_data**, use o seguinte comando curl:

```terminal
curl -i -k --anyauth -u root:<AZDATA_PASSWORD> -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/?op=liststatus'
```

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

Em pontos de extremidade que não usam raiz, use o seguinte comando curl:

```terminal
curl -i -k --anyauth -u <AZDATA_USERNAME>:<AZDATA_PASSWORD> -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>Colocar um arquivo local no HDFS

Para colocar um novo arquivo **test.csv** do diretório local em product_review_data directory, use o seguinte comando curl (o parâmetro **Content-Type** é necessário):

```terminal
curl -i -L -k --anyauth -u root:<AZDATA_PASSWORD> -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

Em pontos de extremidade que não usam raiz, use o seguinte comando curl:

```terminal
curl -i -L -k --anyauth -u <AZDATA_USERNAME>:<AZDATA_PASSWORD> -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>Criar um diretório

Para criar um diretório **teste** em `hdfs:///`, use o seguinte comando:

```terminal
curl -i -L -k --anyauth -u root:<AZDATA_PASSWORD> -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]
Em pontos de extremidade que não usam raiz, use o seguinte comando curl:

```terminal
curl -i -L -k --anyauth -u <AZDATA_USERNAME>:<AZDATA_PASSWORD> -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o cluster de Big Data do SQL Server, confira [O que é um cluster de Big Data do SQL Server?](big-data-cluster-overview.md).
