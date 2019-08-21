---
title: Use a rotação para carregar dados no HDFS | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: Use a rotação para carregar dados no HDFS [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]em.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 729c3af97f98bafced482f7ead8ce85f93b55af3
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652227"
---
# <a name="use-curl-to-load-data-into-hdfs-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Use a rotação para carregar dados no HDFS em[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo explica como usar a **rotação** para carregar dados no HDFS [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (versão prévia).

## <a name="obtain-the-service-external-ip"></a>Obter o IP externo do serviço

WebHDFS é iniciado quando a implantação é concluída e seu acesso passa pelo Knox. O ponto de extremidade do Knox é exposto por meio de um serviço do Kubernetes chamado **gateway-svc-external**.  Para criar a URL de WebHDFS necessária para fazer upload/baixar arquivos, você precisa do endereço IP externo do serviço **gateway-svc-external** e do nome do cluster de Big Data. Você pode obter o endereço IP externo do serviço **gateway-svc-external** executando o seguinte comando:

```bash
kubectl get service gateway-svc-external -n <big data cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> O `<big data cluster name>` aqui está o nome do cluster que você especificou no arquivo de configuração de implantação. O nome padrão é `mssql-cluster`.

## <a name="construct-the-url-to-access-webhdfs"></a>Construir a URL para acessar o WebHDFS

Agora, você pode construir a URL para acessar o WebHDFS da seguinte maneira:

`https://<gateway-svc-external service external IP address>:30443/gateway/default/webhdfs/v1/`

Por exemplo:

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>Listar um arquivo

Para listar o arquivo em **hdfs:///airlinedata**, use o seguinte comando de rotação:

```bash
curl -i -k -u root:root-password -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>Colocar um arquivo local no HDFS

Para colocar um novo arquivo **test.csv** do diretório local no diretório airlinedata, use o seguinte comando de rotação (o parâmetro **Content-Type** é necessário):

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>Criar um diretório

Para criar um diretório **teste** em `hdfs:///`, use o seguinte comando:

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o cluster de Big Data do SQL Server, confira [O que é um cluster de Big Data do SQL Server?](big-data-cluster-overview.md).
