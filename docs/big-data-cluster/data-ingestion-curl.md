---
title: Use o curl para carregar dados no HDFS no SQL Server de 2019 CTP 2.1 | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: a5f580ab39ef7338f424975d9667745131ee748f
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221622"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-2019-ctp-21"></a>Use o curl para carregar dados no HDFS no SQL Server de 2019 CTP 2.1

Este artigo explica como usar **curl** para carregar dados no HDFS no SQL Server de 2019 CTP 2.1.

## <a name="obtain-the-service-external-ip"></a>Obter o IP externo do serviço

WebHDFS é iniciado quando a implantação for concluída, e seu acesso passa pelo Knox. O ponto de extremidade do Knox é exposto por meio de um serviço Kubernetes chamado (por enquanto) **serviço de segurança de lb**.  Para criar a URL de WebHDFS que você precisará usar o CURL para carregar/baixar arquivos, será necessário o **serviço de segurança de lb** endereço IP externo e o nome do seu cluster do serviço. Você pode obter o endereço IP externo do serviço do serviço de segurança de lb executando este comando:

```bash
kubectl get service service-security-lb -n <cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> O `<cluster name>` aqui é o nome do cluster que você forneceu quando você executou mssqlctl criar cluster `<cluster name>`.

## <a name="construct-the-url-to-access-webhdfs"></a>Construir a URL para acessar o WebHDFS

Agora, você pode construir a URL para acessar o WebHDFS da seguinte maneira:

`https://<service-security-lb service external IP address>:30433/gateway/default/webhdfs/v1/`

Por exemplo:

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>Lista de um arquivo

Arquivo de lista sob **hdfs: / / / airlinedata** use o seguinte comando curl:

```bash
curl -i -k -u root:root-password -X GET 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>Colocar um arquivo local no HDFS

Para colocar um novo arquivo **CSV** do diretório local ao diretório airlinedata (**Content-Type** parâmetro é necessário) use o seguinte comando curl:

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>Crie um diretório

Para criar um diretório **testar** sob `hdfs:///` use o seguinte comando:

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o cluster de big data do SQL Server, consulte [o que é o cluster de big data do SQL Server?](big-data-cluster-overview.md).