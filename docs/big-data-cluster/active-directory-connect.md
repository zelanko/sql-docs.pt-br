---
title: Conectar-se no modo do Active Directory
titleSuffix: SQL Server Big Data Cluster
description: Saiba como se conectar aos Clusters de Big Data do SQL Server em um domínio do Active Directory.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bd8da3642d0a650ea10c54b7ed8e46a54fba2971
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91898661"
---
# <a name="connect-big-data-clusters-2019-active-directory-mode"></a>Conectar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]: Modo do Active Directory

Este artigo descreve como se conectar aos pontos de extremidade do cluster de Big Data do SQL Server implantados no modo do Active Directory. As tarefas deste artigo exigem que você tenha um cluster de Big Data do SQL Server implantado no modo do Active Directory. Caso você não tenha um cluster, veja [Implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo do Active Directory](active-directory-deploy.md).

## <a name="overview"></a>Visão geral

Faça logon na instância mestre do SQL Server com AD Auth.

Para verificar as conexões do AD com a instância do SQL Server, conecte-se à instância do SQL mestre com `sqlcmd`. Os logons são criados automaticamente para os grupos fornecidos na implantação (`clusterUsers` e `clusterAdmins`).

Se estiver usando Linux, primeiro execute `kinit` como o usuário do AD e, em seguida, execute `sqlcmd`. Se estiver usando o Windows, basta fazer logon como o usuário desejado em um **computador cliente ingressado no domínio**.

## <a name="connect-to-master-instance-from-linuxmac"></a>Conectar-se à instância mestre do Linux/Mac

```bash
kinit <username>@<domain name>
sqlcmd -S <DNS name for master instance>,31433 -E
```

## <a name="connect-to-master-instance-from-windows"></a>Conectar-se à instância mestre do Windows

```cmd
sqlcmd -S <DNS name for master instance>,31433 -E
```

## <a name="log-in-to-sql-server-master-instance-using-azure-data-studio-or-ssms"></a>Faça logon na instância mestre do SQL Server usando o Azure Data Studio ou o SSMS

Em um cliente ingressado no domínio, você pode abrir o SSMS ou o Azure Data Studio e conectar-se à instância mestre. Essa é a mesma experiência que se conectar a qualquer instância do SQL Server usando a autenticação do AD.

Do SSMS:

![Conectar-se à caixa de diálogo do SQL Server no SSMS](./media/deploy-active-directory/image23.png)

Do Azure Data Studio:

![Conectar-se à caixa de diálogo do SQL Server no Azure Data Studio](./media/deploy-active-directory/image24.png)}

## <a name="log-in-to-controller-with-ad-authentication"></a>Fazer logon no controlador com a autenticação do AD

### <a name="connect-to-controller-with-ad-authentication-from-linuxmac"></a>Conectar-se ao controlador com a autenticação do AD do Linux/Mac

Há duas opções para se conectar ao ponto de extremidade do controlador usando o `azdata` e a autenticação do AD. Use o parâmetro *--endpoint/-e*:

```bash
kinit <username>@<domain name>
azdata login -e https://<controller DNS name>:30080 --auth ad
```

Como alternativa, você pode se conectar usando o parâmetro *--namespace/-n*, que é o nome do cluster de Big Data:

```bash
kinit <username>@<domain name>
azdata login -n <clusterName> --auth ad
```

### <a name="connect-to-controller-with-ad-authentication-from-windows"></a>Conectar-se ao controlador com a autenticação do AD do Windows

```cmd
azdata login -e https://<controller DNS name>:30080 --auth ad
```

## <a name="use-ad-authentication-to-knox-gateway-webhdfs"></a>Usar a autenticação do AD para o gateway do Knox (webHDFS)

Você também pode emitir comandos do HDFS usando ondulação por meio do ponto de extremidade do gateway do Knox. Isso requer a autenticação do AD para o Knox. O comando de ondulação abaixo emite uma chamada REST webHDFS por meio do gateway do Knox para criar um diretório chamado `products`

```bash
curl -k -v --negotiate -u : https://<Gateway DNS name>:30443/gateway/default/webhdfs/v1/products?op=MKDIRS -X PUT
```

## <a name="next-steps"></a>Próximas etapas

[Solucionar problemas de integração do Active Directory ao cluster de Big Data do SQL Server](troubleshoot-active-directory.md)

[Conceito: implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo do Active Directory](active-directory-deployment-background.md)
