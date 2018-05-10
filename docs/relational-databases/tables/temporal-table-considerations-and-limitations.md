---
title: Considerações e limitações da tabela temporal | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c8a21481-0f0e-41e3-a1ad-49a84091b422
caps.latest.revision: 18
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7127db06d4d2e63304ab870ad3c2c9ee3fe91001
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="temporal-table-considerations-and-limitations"></a>Considerações e limitações da tabela temporal
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Há algumas considerações e limitações a serem consideradas ao trabalhar com tabelas temporais, devido à natureza do controle de versão do sistema.  
  
 Considere o seguinte ao trabalhar com tabelas temporais.  
  
-   Uma tabela temporal deve ter uma chave primária definida para correlacionar registros entre a tabela atual e a tabela de histórico e a tabela de histórico não pode ter uma chave primária definida.  
  
-   As colunas de período SYSTEM_TIME usadas para registrar os valores **SysStartTime** e **SysEndTime** devem ser definidas com um tipo de dados de datetime2.  
  
-   Se o nome de uma tabela de histórico estiver especificado durante a criação da tabela de histórico, você deverá especificar o nome do esquema e da tabela.  
  
-   Por padrão, a tabela de histórico é **PAGE** compactado.  
  
-   Se a tabela atual estiver particionada, a tabela de histórico será criada no grupo de arquivos padrão porque a configuração de particionamento não será replicada automaticamente da tabela atual para a tabela de histórico.  
  
-   As tabelas de histórico e temporais não podem ser **FILETABLE** e podem conter colunas de qualquer tipo de dados com suporte além de **FILESTREAM** porque **FILETABLE** e **FILESTREAM** permitem a manipulação de dados fora de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, portanto, o controle de versão do sistema não pode ser garantido.  
  
-   Embora as tabelas temporais deem suporte a tipos de dados de blobs, como **(n)varchar(max)**, **varbinary(max)**, **(n)text** e **image**, elas incorrerão em custos significativos de armazenamento e terão implicações de desempenho devido a seu tamanho. Assim, ao criar seu sistema, tome cuidado ao usar esses tipos de dados.  
  
-   A tabela de histórico deve ser criada no mesmo banco de dados da tabela atual. As consultas temporais no **Linked Server** não têm suporte.  
  
-   A tabela de histórico não pode ter restrições (chave primária, chave estrangeira, restrições de tabela ou coluna).  
  
-   Não há suporte para exibições indexadas em consultas temporais (consultas que usam a cláusula **FOR SYSTEM_TIME** )  
  
-   A opção online (**WITH (ONLINE = ON**) não tem nenhum efeito em **ALTER TABLE ALTER COLUMN** no caso da tabela temporal com controle de versão do sistema. A coluna ALTER não é executada online, independentemente de qual valor tenha sido especificado para a opção ONLINE.  
  
-   As instruções**INSERT** e **UPDATE** não podem fazer referência às colunas de período SYSTEM_TIME. As tentativas de inserir valores diretamente nessas colunas serão bloqueadas.  
  
-   **TRUNCATE TABLE** quando **SYSTEM_VERSIONING** é **ON**  
  
-   Não é permitida a modificação direta dos dados em uma tabela de histórico.  
  
-   O**ON DELETE CASCADE** e o **ON UPDATE CASCADE** não são permitidos na tabela atual. Em outras palavras, quando a tabela temporal estiver referenciando a tabela na relação de chave estrangeira (correspondente a *parent_object_id* em sys.foreign_keys), as opções CASCADE não serão permitidas. Para trabalhar com essa limitação, use a lógica do aplicativo ou gatilhos AFTER para manter a consistência de exclusão na tabela de chave primária (correspondente a  *referenced_object_id* em sys.foreign_keys). Se a tabela de chave primária for temporal e a tabela de referência não for temporal, não haverá essa limitação. 

    **OBSERVAÇÃO:** essa limitação se aplica apenas ao SQL Server 2016. Opções CASCADE têm suporte no [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] e no SQL Server 2017 a partir do CTP 2.0.  
  
-   Os gatilhos**INSTEAD OF** não são permitidos na tabela atual ou de histórico para evitar a anulação da lógica de DML. Os gatilhos**AFTER** são permitidos somente na tabela atual. Eles são bloqueados na tabela de histórico para evitar a anulação da lógica de DML.  
  
-   O uso de tecnologias de replicação é limitado.  
  
    -   **Sempre ativo:** com suporte total  
  
    -   **Captura de Dados de Alteração e Controle de Dados de Alteração:** com suporte apenas na tabela atual  
  
    -   **Instantâneo e replicação transacional**: com suporte apenas para um único publicador sem o temporal habilitado e um assinante com o temporal habilitado. Nesse caso, o publicador é usado para uma carga de trabalho OLTP, enquanto o assinante serve para o descarregamento de relatórios (incluindo consulta ‘AS OF’).    
        Não há suporte para o uso de vários assinantes porque esse cenário pode levar a dados temporais inconsistentes e cada um deles depende do relógio do sistema local.  
  
    -   **Replicação de mesclagem:** não tem suporte para tabelas temporais  
  
-   As consultas comuns afetam somente os dados na tabela atual. Para consultar os dados na tabela de histórico, você deverá usar consultas temporais. Isso será discutido neste documento na seção intitulada Consultando dados temporais.  
  
-   Uma estratégia de indexação ideal incluirá um índice de repositório de colunas clusterizadas e/ou um índice de rowstore de árvore B na tabela atual e um índice columnstore clusterizado na tabela de histórico para haver um desempenho e um tamanho de armazenamento ideal. Se você criar/usar sua própria tabela de histórico, será altamente recomendável que você crie esse tipo de índice com colunas de período começando com o final da coluna do período para acelerar a consulta temporal, além de acelerar as consultas que fazem parte da verificação de consistência de dados. A tabela de histórico padrão tem um índice rowstore clusterizado criado para você com base nas colunas de período (início, fim). No mínimo, recomenda-se um índice rowstore não clusterizado.  
  
-   Os seguintes objetos/propriedades não serão replicados da tabela atual para a tabela de histórico quando a tabela de histórico for criada  
  
    -   Definição de período  
  
    -   Definição de identidade  
  
    -   Índices  
  
    -   Estatísticas  
  
    -   Verificar restrições  
  
    -   Gatilhos  
  
    -   Configuração de particionamento  
  
    -   Permissões  
  
    -   Predicados de segurança em nível de linha  
  
-   Uma tabela de histórico não pode ser configurada como tabela atual em uma cadeia de tabelas de histórico.  
  

## <a name="see-also"></a>Consulte Também  
 [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)   
 [Introdução a Tabelas Temporais com Controle da Versão do Sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Particionamento de Tabelas Temporais](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Segurança da tabela temporal](../../relational-databases/tables/temporal-table-security.md)   
 [Gerenciar a Retenção de Dados Históricos em Tabelas Temporais com Versão do Sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
