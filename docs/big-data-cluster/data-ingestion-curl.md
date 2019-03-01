---
title: Use o curl para carregar dados no HDFS em clusters do SQL Server 2019 big data | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 1a7c7691ec20f459f39a39270e9a78fc9d8ad96f
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017542"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-2019-big-data-clusters"></a>Use o curl para carregar dados no HDFS em clusters do SQL Server 2019 big data

Este artigo explica como usar **curl** para carregar dados no HDFS em clusters de big data de 2019 do SQL Server (versão prévia).

## <a name="obtain-the-service-external-ip"></a>Obter o IP externo do serviço

WebHDFS é iniciado quando a implantação for concluída, e seu acesso passa pelo Knox. O ponto de extremidade do Knox é exposto por meio de um serviço de Kubernetes chamado **segurança de ponto de extremidade**.  Para criar a URL de WebHDFS necessário para carregar/baixar arquivos, é necessário o **segurança de ponto de extremidade** endereço IP externo e o nome do seu cluster do serviço. Você pode obter o **segurança de ponto de extremidade** endereço IP externo do serviço, executando o seguinte comando:

```bash
kubectl get service endpoint-security -n <cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> O `<cluster name>` aqui é o nome do cluster que você forneceu quando você executou `mssqlctl cluster create --name <cluster name>`.

## <a name="construct-the-url-to-access-webhdfs"></a>Construir a URL para acessar o WebHDFS

Agora, você pode construir a URL para acessar o WebHDFS da seguinte maneira:

`https://<endpoint-security service external IP address>:30443/gateway/default/webhdfs/v1/`

Por exemplo:

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>Lista de um arquivo

Arquivo de lista sob **hdfs: / / / airlinedata**, use o seguinte comando curl:

```bash
curl -i -k -u root:root-password -X GET 'https://<endpoint-security IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>Colocar um arquivo local no HDFS

Para colocar um novo arquivo **CSV** no diretório local ao diretório airlinedata, use o seguinte comando curl (o **Content-Type** parâmetro é obrigatório):

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<endpoint-security IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>Crie um diretório

Para criar um diretório **testar** sob `hdfs:///`, use o seguinte comando:

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<endpoint-security IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o cluster de big data do SQL Server, consulte [o que é o cluster de big data do SQL Server?](big-data-cluster-overview.md).
