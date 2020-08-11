---
title: Restaurar permissões do HDFS
titleSuffix: SQL Server Big Data Cluster
description: Restaure os direitos de administrador do HDFS.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 04/21/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c6d09921074ca2f2e386535baff5060620a7a3c8
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669379"
---
# <a name="restore-hdfs-permissions"></a>Restaurar permissões do HDFS

As modificações de ACLs (listas de controle de acesso) do HDFS podem ter afetado as pastas `/system` e `/tmp` no HDFS. A causa mais provável da modificação da ACL é um usuário manipulando manualmente as ACLs da pasta. Não há suporte para a modificação direta de permissões nas pastas /system e /tmp/logs.

## <a name="symptom"></a>Sintoma

Um trabalho do Spark é enviado por meio do ADS e falha com o erro de inicialização SparkContext e AccessControlexception.

```
583 ERROR spark.SparkContext: Error initializing SparkContext.
org.apache.hadoop.security.AccessControlException: Permission denied: user=<UserAccount>, access=WRITE, inode="/system/spark-events":sph:BDCAdmin:drwxr-xr-x
```

A interface do usuário do Yarn mostra a ID do aplicativo no status INTERROMPIDO.

Quando você tenta gravar na pasta como o usuário do domínio, também ocorre uma falha. Você pode testar o seguinte exemplo:

```bash
kinit <UserAccount>
hdfs dfs -touch /system/spark-events/test
hdfs dfs -rm /system/spark-events/test
```

## <a name="cause"></a>Causa

As ACLs do HDFS foram modificadas para o grupo de segurança de domínio do usuário do BDC. As possíveis modificações incluíram ACLs das pastas /system e/tmp. Não há suporte para modificações nessas pastas.

Verifique o efeito nos logs do Livy:

```
INFO utils.LineBufferedStream: YYYY-MM-DD-HH:MM:SS,858 INFO yarn.Client: Application report for application_1580771254352_0041 (state: ACCEPTED)
...
WARN rsc.RSCClient: Client RPC channel closed unexpectedly.
INFO interactive.InteractiveSession: Failed to ping RSC driver for session <ID>. Killing application
```

A interface do usuário do YARN mostra os aplicativos no status INTERROMPIDO para a ID do aplicativo.

Para obter a causa raiz do fechamento da conexão RPC, verifique o log do YARN para o aplicativo correspondente ao desejado. No exemplo anterior, refere-se a `application_1580771254352_0041`. Use `kubectl` para se conectar ao pod sparkhead-0 e execute este comando:

O comando a seguir consulta o log do YARN para o aplicativo.

```bash
yarn logs -applicationId application_1580771254352_0041
```

Nos resultados abaixo, a permissão é negada para o usuário. 

```
YYYY-MM-DD-HH:MM:SS,583 ERROR spark.SparkContext: Error initializing SparkContext.
org.apache.hadoop.security.AccessControlException: Permission denied: user=user1, access=WRITE, inode="/system/spark-events":sph:BDCAdmin:drwxr-xr-x
```

A causa pode ter sido a adição recursiva do usuário do BDC à pasta raiz do HDFS. Isso pode ter afetado as permissões padrão.

## <a name="resolution"></a>Resolução

Restaure as permissões com o seguinte script: Use `kinit` com admin:

```bash
hdfs dfs -chmod 733 /system/spark-events
hdfs dfs -setfacl --set default:user:sph:rwx,default:other::--- /system/spark-events
hdfs dfs -setfacl --set default:user:app-setup:r-x,default:other::--- /system/appdeploy
hadoop fs -chmod 733 /tmp/logs
hdfs dfs -setfacl --set default:user:yarn:rwx,default:other::--- /tmp/logs
```
