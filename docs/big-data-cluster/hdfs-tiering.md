---
title: Configurar a disposição em camadas do HDFS
titleSuffix: SQL Server big data clusters
description: Este artigo explica como configurar o HDFS disposição em camadas para montar um sistema de arquivo externo do armazenamento do Azure Data Lake no HDFS em um cluster de big data do SQL Server 2019 (visualização).
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ccafa7914d09971e33d60fc9d25c7b812983aa98
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63472092"
---
# <a name="configure-hdfs-tiering-on-sql-server-big-data-clusters"></a>Configurar o HDFS disposição em camadas em clusters de grandes dados do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Disposição em camadas HDFS fornece a capacidade de montar externa, sistema de arquivos compatível com HDFS no HDFS. Este artigo explica como configurar o HDFS disposição em camadas para clusters de big data de 2019 do SQL Server (versão prévia). Neste momento, damos suporte a se conectar ao armazenamento do Azure Data Lake Gen2 e Amazon S3. 

## <a name="hdfs-tiering-overview"></a>Visão geral de disposição em camadas do HDFS

Com camadas, aplicativos podem acessar diretamente os dados em uma variedade de armazenamentos externos como se os dados residem no HDFS local. Montagem é uma operação de metadados, em que os metadados que descreve o namespace no sistema de arquivo externo é copiado para o HDFS local. Esses metadados incluem informações sobre os diretórios externos e arquivos junto com suas permissões e ACLs. Os dados correspondentes são apenas copiada sob demanda, quando os dados em si são acessados por meio de consulta por exemplo. Os dados do sistema de arquivo externo agora podem ser acessados do cluster de big data do SQL Server. Você pode executar o Spark trabalhos e consultas SQL sobre esses dados da mesma forma que você executaria em todos os dados locais armazenados em HDFS no cluster.

### <a name="caching"></a>Cache
Hoje em dia, por padrão, 1% do armazenamento HDFS total será reservado para o cache de dados montados. Armazenamento em cache é uma configuração global em montagens.

> [!NOTE]
> HDFS disposição em camadas é um recurso desenvolvido pela Microsoft e uma versão anterior dele foi lançada como parte da distribuição do Apache Hadoop 3.1. Para obter mais informações, consulte [ https://issues.apache.org/jira/browse/HDFS-9806 ](https://issues.apache.org/jira/browse/HDFS-9806) para obter detalhes.

As seções a seguir fornecem um exemplo de como configurar o HDFS disposição em camadas com uma fonte de dados do armazenamento do Azure Data Lake Gen2.

## <a name="prerequisites"></a>Prerequisites

- [Cluster de big data implantados](deployment-guidance.md)
- [Ferramentas de big data](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**

## <a name="mounting-instructions"></a>Instruções de montagem

Há suporte para se conectar ao armazenamento do Azure Data Lake Gen2 e Amazon S3. Instruções sobre como montar contra esses tipos de armazenamento podem ser encontradas nos seguintes artigos:

- [Como Gen2 ADLS de montagem para o HDFS disposição em camadas em um cluster de big data](hdfs-tiering-mount-adlsgen2.md)
- [Como montar S3 para o HDFS disposição em camadas em um cluster de big data](hdfs-tiering-mount-s3.md)

## <a id="issues"></a> Limitações e problemas conhecidos

A lista a seguir fornece os problemas conhecidos e limitações atuais ao usar HDFS disposição em camadas em clusters de grandes dados do SQL Server:

- Se a montagem estiver preso em um `CREATING` de estado por um longo tempo, que provavelmente tenha falhado. Nessa situação, cancelar o comando e excluir a montagem, se necessário. Verificar se seus parâmetros e as credenciais estão corretas antes de tentar novamente.

- Não não possível criar montagens de diretórios existentes.

- Não não possível criar montagens dentro de montagens existentes.

- Se qualquer um dos ancestrais do ponto de montagem não existir, serão criados com as permissões padronizada para r xr xr-x (555).

- Criação de montagem pode levar algum tempo dependendo do número e tamanho dos arquivos que está sendo montado. Durante esse processo, os arquivos de montagem não são visíveis aos usuários. Enquanto a montagem é criada, todos os arquivos serão adicionados a um caminho temporário, cujo padrão é `/_temporary/_mounts/<mount-location>`.

- O comando de criação de montagem é assíncrono. Depois que o comando é executado, o status de montagem pode ser verificado para entender o estado da montagem.

- Ao criar a montagem, o argumento usado para **– caminho de montagem** é essencialmente um identificador exclusivo da montagem. A mesma cadeia de caracteres (incluindo o "/" no final, se presente) deve ser usada em comandos subsequentes.

- As montagens são somente leitura. Você não pode criar os diretórios ou arquivos em uma montagem.

- Não recomendamos diretórios de montagem e arquivos que podem ser alterados. Depois que a montagem é criada, quaisquer alterações ou atualizações para o local remoto não serão refletidas na montagem no HDFS. Se houver alterações no local remoto, você pode optar por excluir e recriar a montagem para refletir o estado atualizado.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de big data de 2019 do SQL Server, consulte [quais são os clusters do SQL Server 2019 big data?](big-data-cluster-overview.md).
