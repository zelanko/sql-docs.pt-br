---
title: Use o curl para carregar dados no HDFS | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: Use o curl para carregar dados no HDFS em clusters do SQL Server 2019 big data.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aae991c6dfdade4145f1e5578273e3b6aeb83299
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958637"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-big-data-clusters"></a>Use o curl para carregar dados no HDFS em clusters de grandes dados do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo explica como usar **curl** para carregar dados no HDFS em clusters de big data de 2019 do SQL Server (versão prévia).

## <a name="obtain-the-service-external-ip"></a>Obter o IP externo do serviço

WebHDFS é iniciado quando a implantação for concluída, e seu acesso passa pelo Knox. O ponto de extremidade do Knox é exposto por meio de um serviço de Kubernetes chamado **gateway-svc-externo**.  Para criar a URL de WebHDFS necessário para carregar/baixar arquivos, é necessário o **gateway-svc-externo** endereço IP externo e o nome do seu cluster de big data de serviço. Você pode obter o **gateway-svc-externo** endereço IP externo do serviço, executando o seguinte comando:

```bash
kubectl get service gateway-svc-external -n <big data cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> O `<big data cluster name>` aqui é o nome do cluster que você especificou no arquivo de configuração de implantação. O nome padrão é `mssql-cluster`.

## <a name="construct-the-url-to-access-webhdfs"></a>Construir a URL para acessar o WebHDFS

Agora, você pode construir a URL para acessar o WebHDFS da seguinte maneira:

`https://<gateway-svc-external service external IP address>:30443/gateway/default/webhdfs/v1/`

Por exemplo:

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>Lista de um arquivo

Arquivo de lista sob **hdfs: / / / airlinedata**, use o seguinte comando curl:

```bash
curl -i -k -u root:root-password -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>Colocar um arquivo local no HDFS

Para colocar um novo arquivo **CSV** no diretório local ao diretório airlinedata, use o seguinte comando curl (o **Content-Type** parâmetro é obrigatório):

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>Crie um diretório

Para criar um diretório **testar** sob `hdfs:///`, use o seguinte comando:

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o cluster de big data do SQL Server, consulte [o que é o cluster de big data do SQL Server?](big-data-cluster-overview.md).
