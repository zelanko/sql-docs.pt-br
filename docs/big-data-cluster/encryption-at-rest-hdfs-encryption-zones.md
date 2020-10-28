---
title: Guia de uso de zonas de criptografia do HDFS nos Clusters de Big Data do SQL Server
titleSuffix: SQL Server big data clusters
description: Este artigo mostra como usar o recurso de zonas de criptografia do HDFS nos BDC do SQL Server
author: DaniBunny
ms.author: dacoelho
ms.reviewer: mihaelab
ms.date: 10/19/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 904b07913a63e226e5e45876f2fc520226411223
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92199553"
---
# <a name="sql-server-big-data-clusters-hdfs-encryption-zones-usage-guide"></a>Guia de uso de zonas de criptografia do HDFS nos Clusters de Big Data do SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este guia demonstra como usar os recursos de Criptografia em Repouso dos Clusters de Big Data do SQL Server para criptografar pastas do HDFS usando zonas de criptografia.

Observe que já existe uma zona de criptografia padrão montada em __```/securelake```__ pronta para uso. Ela foi criada com uma chave de 256 bits gerada pelo sistema chamada __securelakekey__ . Essa chave pode ser usada para criar zonas de criptografia adicionais.

## <a name="prerequisites"></a><a id="prereqs"></a> Pré-requisitos

- [Cluster de Big Data do SQL Server CU8 ou posterior](release-notes-big-data-cluster.md) com Integração ao Active Directory.
- Usuário com privilégios de administrador.

## <a name="login-into-the-name-node"></a>Logon no nó de nome

Use as [instruções de conexão do Active Directory](active-directory-connect.md) para executar o logon do cluster. Faça logon no namenode (nmnode-0-0) para emitir a chave e os comandos de zonas de criptografia.

   ```console
   kubectl exec -it -c hadoop -n <cluster_namespace> nmnode-0-0 -- /bin/bash
   ```

## <a name="create-an-encryption-zone-using-the-provided-system-managed-key"></a>Criar uma zona de criptografia usando a chave gerenciada fornecida pelo sistema

1. Criar uma pasta do HDFS

   ```console
   hdfs dfs -mkdir -p /user/zone/folder
   ```

1. Emita o comando de criação de zona de criptografia para criptografar a pasta usando a chave __securelakekey__ .

   ```console
   hdfs crypto -createZone -keyName securelakekey -path /user/zone/folder
   ```

## <a name="create-a-custom-new-key-and-encryption-zone"></a>Criar chave e zona de criptografia personalizadas

1. Use o padrão a seguir para criar uma chave de 256 bits.

   ```console
   kinit hdfs
   hadoop key create mydatalakekey -size 256
   ```

1. Crie e criptografe um caminho do HDFS usando a chave de usuário.

   ```console
   hdfs dfs -mkdir -p /user/mydatalake
   hdfs crypto -createZone -keyName mydatalakekey -path /user/mydatalake
   ```
