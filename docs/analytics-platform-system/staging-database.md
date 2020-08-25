---
title: Usando um banco de dados de preparo
description: SQL Server o PDW (data warehouse paralelo) usa um banco de dados de preparo para armazenar os dados temporariamente durante o processo de carregamento.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: dcd7f95833695cc5f9f791d83a6221c35e88f58e
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400278"
---
# <a name="using-a-staging-database-in-parallel-data-warehouse-pdw"></a>Usando um banco de dados de preparo em Parallel data warehouse (PDW)
SQL Server o PDW (data warehouse paralelo) usa um banco de dados de preparo para armazenar os dados temporariamente durante o processo de carregamento. Por padrão, SQL Server PDW usa o banco de dados de destino como o banco de dados de preparo, o que pode causar a fragmentação da tabela. Para reduzir a fragmentação da tabela, você pode criar um banco de dados de preparo definido pelo usuário. Ou, quando a reversão de uma falha de carregamento não é uma preocupação, você pode usar o modo de carregamento fastappend para melhorar o desempenho, ignorando a tabela temporária e carregando diretamente na tabela de destino.  
  
## <a name="staging-database-basics"></a><a name="StagingDatabase"></a>Noções básicas do banco de dados de preparo  
Um *banco de dados de preparo* é um banco de dados de PDW criado pelo usuário, que armazena o dado temporariamente enquanto é carregado no dispositivo. Quando um banco de dados de preparo for especificado para uma carga, o dispositivo copiará primeiro os dados para o banco de dado de preparo e, em seguida, copiará os dados das tabelas temporárias no banco de dados de preparo para tabelas permanentes no banco de dados de destino.  
  
Quando um banco de dados de preparo não é especificado para uma carga, o SQL ServerPDW cria as tabelas temporárias no banco de dados de destino e as usa para armazenar os dados carregados antes de inserir os dados carregados nas tabelas de destino permanentes.  
  
Quando uma carga usa o *modo fastappend*, o SQL ServerPDW ignora o uso de tabelas temporárias e anexa os dados diretamente à tabela de destino. O modo fastappend melhora o desempenho de carga para cenários ELT em que os dados são carregados em uma tabela que é uma tabela temporária do ponto de vista do aplicativo. Por exemplo, um processo ELT poderia carregar dados em uma tabela temporária, processar os dados por meio de limpeza e duping e, em seguida, inserir os dados na tabela de fatos de destino. Nesse caso, não é necessário que o PDW carregue primeiro os dados em uma tabela temporária interna antes de inserir os dados na tabela temporária do aplicativo. O modo fastappend evita a etapa de carregamento extra, o que melhora significativamente o desempenho da carga. Para usar o modo fastappend, você deve usar o modo de várias transações, o que significa que a recuperação de uma carga com falha ou anulada deve ser tratada pelo seu próprio processo de carregamento.  
  
**Benefícios do banco de dados de preparo**  
  
O principal benefício de um banco de dados de preparo é reduzir a fragmentação da tabela. Se um banco de dados de preparo não for usado, os dados serão carregados em tabelas temporárias no banco de dados de destino. Quando as tabelas temporárias são criadas e descartadas no banco de dados de destino, as páginas das tabelas temporárias e das tabelas permanentes se tornam intercaladas. Ao longo do tempo, a fragmentação da tabela ocorre e degrada o desempenho. Por outro lado, um banco de dados de preparo garante que as tabelas temporárias sejam criadas e removidas em um espaço de arquivo separado do que as tabelas permanentes.  
  
**Estruturas de tabela de banco de dados de preparo**  
  
A estrutura de armazenamento para cada tabela de banco de dados depende da tabela de destino.  
  
-   Para cargas em um heap ou índice columnstore clusterizado, a tabela de preparo é um heap.  
  
-   Para cargas em um índice clusterizado do repositório de armazenamento, a tabela de preparo é um índice clusterizado do armazenamento.  
  
## <a name="permissions"></a><a name="Permissions"></a>Permissões  
Requer a permissão CREATE (para criar uma tabela temporária) no banco de dados de preparo. 

<!-- MISSING LINKS

For more information, see [Grant Permissions to load data](grant-permissions-to-load-data.md).  

-->
  
## <a name="best-practices-for-creating-a-staging-database"></a><a name="CreatingStagingDatabase"></a>Práticas recomendadas para criar um banco de dados de preparo  
  
1.  Deve haver apenas um banco de dados de preparo por dispositivo. O banco de dados de preparo pode ser compartilhado por todos os trabalhos de carga para todos os bancos de dados de destino.  
  
2.  O tamanho do banco de dados de preparo é específico do cliente. Inicialmente, ao preencher o dispositivo pela primeira vez, o banco de dados de preparo deve ser grande o suficiente para acomodar os trabalhos de carga inicial. Esses trabalhos de carga tendem a ser grandes porque várias cargas podem ocorrer simultaneamente. Depois que os trabalhos de carregamento inicial forem concluídos e o sistema estiver em produção, o tamanho de cada trabalho de carga provavelmente será menor. Quando as cargas são pequenas, você pode reduzir o tamanho do banco de dados de preparo para acomodar os tamanhos de carga menores. Para reduzir o tamanho, você pode remover o banco de dados de preparo e criá-lo novamente com alocações de tamanho menor ou pode usar a instrução [ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) .  
  
    Ao criar o banco de dados de preparo, use as diretrizes a seguir.  
  
    -   O tamanho da tabela replicada deve ser o tamanho estimado, por nó de computação, de todas as tabelas replicadas que serão carregadas simultaneamente. Normalmente, o tamanho é 25-30 GB.  
  
    -   O tamanho da tabela distribuída deve ser o tamanho estimado, por dispositivo, de todas as tabelas distribuídas que serão carregadas simultaneamente.  
  
    -   O tamanho do log normalmente é semelhante ao tamanho da tabela replicada.  
  
## <a name="examples"></a><a name="Examples"></a>Exemplos  
  
### <a name="a-create-a-staging-database"></a>a. Criar um banco de dados de preparo 
O exemplo a seguir cria um banco de dados de preparo, Stagedb, para uso com todas as cargas no dispositivo. Suponha que você estima que cinco tabelas replicadas de tamanho de 5 GB cada uma delas será carregada simultaneamente. Essa simultaneidade resulta na alocação de pelo menos 25 GB para o tamanho replicado. Suponha que você estima que seis tabelas distribuídas de tamanhos 100, 200, 400, 500, 500 e 550 GB serão carregadas simultaneamente. Essa simultaneidade resulta na alocação de pelo menos 2250 GB para o tamanho da tabela distribuída.  
  
```sql  
CREATE DATABASE Stagedb  
WITH (  
  
    AUTOGROW = ON,  
  
    REPLICATED_SIZE = 25 GB,  
  
    DISTRIBUTED_SIZE = 2250 GB,  
  
    LOG_SIZE = 25 GB  
  
);  
```  

<!-- MISSING LINKS
 
## See Also  
[Common metadata query examples](metadata-query-examples.md)  

-->
  
