---
title: Notas de versão do SQL Server 2019 clusters de big data | Microsoft Docs
description: Este artigo descreve as últimas atualizações e problemas conhecidos para clusters de big data de 2019 do SQL Server (versão prévia).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 13d5cfa95b9a37ecf26658ee255f93c8099faa8f
ms.sourcegitcommit: 0d6e4cafbb5d746e7d00fdacf8f3ce16f3023306
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49085542"
---
# <a name="release-notes-for-sql-server-2019-big-data-clusters"></a>Notas de versão do SQL Server 2019 clusters de big data

Este artigo fornece as últimas atualizações e problemas conhecidos para a versão mais recente dos clusters de grandes dados do SQL Server.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="ctp-20-october-2018"></a>CTP 2.0 (outubro de 2018)

As seções a seguir descrevem os novos recursos e problemas conhecidos para clusters de grandes dados no SQL Server de 2019 CTP 2.0.

### <a name="whats-in-the-ctp-20-release"></a>Novidades na versão CTP 2.0

- Experiência de implantação simples usando a ferramenta de gerenciamento mssqlctl
- Experiência de notebook nativo no estúdio de dados do Azure
- Arquivos HDFS de consulta por meio do armazenamento de instância do SQL Server
- Virtualização de dados por meio do mestre do SQL Server, Oracle, MongoDB e HDFS
- Assistente de virtualização de dados do SQL Server e Oracle no estúdio de dados do Azure
- Serviços de ML no mestre
- Portal de administração de cluster que você pode usar para monitoramento e solução de problemas
- Envio de trabalho do Spark no estúdio de dados do Azure 
- Interface do usuário do Spark no portal de administração do cluster
- Volume de montagem para classes de armazenamento
- Consultas em pools de dados do mestre
- Mostrar plano para consultas distribuídas no SSMS
- Pacote de PIP para a ferramenta de gerenciamento mssqlctl
- Mecanismo de implantação interna por meio do serviço de controlador

### <a name="known-issues"></a>Problemas conhecidos

As seções a seguir fornecem os problemas conhecidos para clusters de grandes dados do SQL Server no CTP 2.0.

#### <a name="deployment"></a>Implantação

- Se você estiver usando o serviço de Kubernetes do Azure (AKS), a versão recomendada do Kubernetes é 1.10. *, que não oferece suporte a redimensionamento de disco. Você deve verificar se você está dimensionando o armazenamento de forma adequada no momento da implantação. Para obter mais informações sobre como ajustar os tamanhos de armazenamento, consulte o [persistência de dados](concept-data-persistence.md) artigo. Para o Kubernetes implantado em VMs, a versão recomendada é 1.11.

- Depois de implantar no AKS, você poderá ver os seguintes dois eventos de aviso da implantação. Os dois eventos são problemas conhecidos, mas eles não evitam que você implantar com êxito o cluster de big data no AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Se uma implantação de cluster de big data falhar, o namespace associado não é removido. Isso pode resultar em um namespace órfão no cluster. Uma solução alternativa é excluir o namespace manualmente antes de implantar um cluster com o mesmo nome.

#### <a name="external-tables"></a>Tabelas externas

- É possível criar uma tabela externa do pool de dados para uma tabela que tem sem suporte a tipos de coluna. Se você consultar a tabela externa, você receberá uma mensagem semelhante à seguinte:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Se você consultar uma tabela externa do pool de armazenamento, você poderá receber um erro se o arquivo subjacente está sendo copiado no HDFS ao mesmo tempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark e notebooks

- Endereços IP de POD podem mudar no ambiente do Kubernetes como reinicializações de PODs. No cenário em que o pod de mestre é reiniciado, a sessão do Spark pode falhar com `NoRoteToHostException`. Isso é causado por caches JVM que não são atualizados com o novo IP endereços.

- Se você tiver o Jupyter já instalado e um Python separado no Windows, os blocos de anotações do Spark podem falhar. Para contornar esse problema, atualize o Jupyter para a versão mais recente.

- Em um bloco de anotações, se você clicar na **adicionar texto** de comando, a célula de texto for adicionada no modo de visualização, em vez de modo de edição. Você pode clicar no ícone de visualização para alternar para modo de edição e editar a célula.

#### <a name="hdfs"></a>HDFS

- Se o botão direito do mouse em um arquivo no HDFS para visualizá-lo, você poderá ver o seguinte erro:

   `Error previewing file: File exceeds max size of 30MB`

   Atualmente não há nenhuma maneira de visualizar arquivos maiores do que 30 MB no estúdio de dados do Azure.

- Não há suporte para alterações de configuração para o HDFS que envolvem alterações para o hdfs-site. XML.

#### <a name="security"></a>Segurança

- O SA_PASSWORD faz parte do ambiente e detectáveis (por exemplo, em um arquivo de despejo de cabo). Você deve redefinir o SA_PASSWORD na instância mestre após a implantação. Isso não é um bug, mas uma etapa de segurança. Para obter mais informações sobre como alterar o SA_PASSWORD em um contêiner do Linux, consulte [alterar a senha SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Logs AKS podem conter a senha SA para implantações de cluster de big data.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de grandes dados do SQL Server, consulte [quais são os clusters do SQL Server 2019 big data?](big-data-cluster-overview.md).
