---
title: Configurar a disposição em camadas do HDFS
titleSuffix: SQL Server big data clusters
description: Este artigo explica como configurar a camada do HDFS para montar um sistema de arquivos Azure Data Lake Storage externo no HDFS em um cluster SQL Server 2019 Big Data (versão prévia).
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 17eedf9f0797a0adb5eda6ca8ee090fc762e1491
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419381"
---
# <a name="configure-hdfs-tiering-on-sql-server-big-data-clusters"></a>Configurar a camada do HDFS em clusters SQL Server Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

A disposição em camadas do HDFS fornece a capacidade de montar o sistema de arquivos externo e compatível com HDFS no HDFS. Este artigo explica como configurar a disposição em camadas do HDFS para SQL Server clusters de Big Data 2019 (versão prévia). Neste momento, damos suporte à conexão com o Azure Data Lake Storage Gen2 e ao Amazon S3. 

## <a name="hdfs-tiering-overview"></a>Visão geral de camadas do HDFS

Com o nivelamento, os aplicativos podem acessar diretamente os dados em uma variedade de armazenamentos externos, como se os dados residirem no HDFS local. A montagem é uma operação de metadados, em que os metadados que descrevem o namespace no sistema de arquivos externo são copiados para o HDFS local. Esses metadados incluem informações sobre os diretórios e arquivos externos junto com suas permissões e ACLs. Os dados correspondentes são copiados sob demanda apenas quando os próprios dados são acessados por exemplo, uma consulta. Os dados do sistema de arquivos externos agora podem ser acessados por meio do cluster SQL Server Big Data. Você pode executar trabalhos do Spark e consultas SQL sobre esses dados da mesma forma que executá-los em qualquer dado local armazenado no HDFS no cluster.

### <a name="caching"></a>Cache
Hoje, por padrão, 1% do armazenamento de HDFS total será reservado para cache de dados montados. O Caching é uma configuração global em montagens.

> [!NOTE]
> A camada do HDFS é um recurso desenvolvido pela Microsoft e uma versão anterior dele foi lançada como parte da distribuição Apache Hadoop 3,1. Para obter mais informações, [https://issues.apache.org/jira/browse/HDFS-9806](https://issues.apache.org/jira/browse/HDFS-9806) consulte para obter detalhes.

As seções a seguir fornecem um exemplo de como configurar a disposição em camadas do HDFS com uma fonte de dados Azure Data Lake Storage Gen2.

## <a name="refresh"></a>Atualizar

A camada do HDFS dá suporte à atualização. Atualize uma montagem existente para o instantâneo mais recente dos dados remotos.

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster Big Data implantado](deployment-guidance.md)
- [Ferramentas de Big data](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a name="mounting-instructions"></a>Instruções de montagem

Damos suporte à conexão com o Azure Data Lake Storage Gen2 e o Amazon S3. As instruções sobre como montar esses tipos de armazenamento podem ser encontradas nos seguintes artigos:

- [Como montar ADLS Gen2 para a disposição em camadas do HDFS em um cluster Big Data](hdfs-tiering-mount-adlsgen2.md)
- [Como montar S3 para camadas do HDFS em um cluster Big Data](hdfs-tiering-mount-s3.md)

## <a id="issues"></a>Limitações e problemas conhecidos

A lista a seguir fornece problemas conhecidos e limitações atuais ao usar a camada do HDFS em clusters SQL Server Big Data:

- Se a montagem estiver presa em um `CREATING` estado por muito tempo, isso provavelmente terá falhado. Nessa situação, cancele o comando e exclua a montagem, se necessário. Verifique se os parâmetros e as credenciais estão corretos antes de tentar novamente.

- Não é possível criar montagens em diretórios existentes.

- Não é possível criar montagens em montagens existentes.

- Se qualquer um dos ancestrais do ponto de montagem não existir, ele será criado com as permissões padronizadas para r-XR-xr-x (555).

- A criação da montagem pode levar algum tempo, dependendo do número e do tamanho dos arquivos que estão sendo montados. Durante esse processo, os arquivos sob a montagem não são visíveis para os usuários. Enquanto a montagem é criada, todos os arquivos serão adicionados a um caminho temporário, cujo padrão `/_temporary/_mounts/<mount-location>`é.

- O comando de criação de montagem é assíncrono. Depois que o comando é executado, o status de montagem pode ser verificado para entender o estado da montagem.

- Ao criar a montagem, o argumento usado para **--Mount-path** é essencialmente um identificador exclusivo da montagem. A mesma cadeia de caracteres (incluindo "/" no final, se presente) deve ser usada em comandos subsequentes.

- As montagens são somente leitura. Você não pode criar diretórios ou arquivos em uma montagem.

- Não recomendamos a montagem de diretórios e arquivos que podem ser alterados. Após a criação da montagem, qualquer alteração ou atualização no local remoto não será refletida na montagem no HDFS. Se as alterações ocorrerem no local remoto, você poderá optar por excluir e recriar a montagem para refletir o estado atualizado.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters SQL Server de Big Data 2019, consulte [o que são SQL Server Big data clusters de 2019?](big-data-cluster-overview.md).
