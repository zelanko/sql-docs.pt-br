---
description: Tabelas
title: Tabelas | Microsoft Docs
ms.custom: ''
ms.date: 09/18/2019
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- tables [SQL Server]
- table components [SQL Server]
ms.assetid: 82d7819c-b801-4309-a849-baa63083e83f
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 55fdb422e4a8dd35a23e8e637cabd165729c97b0
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809972"
---
# <a name="tables"></a>Tabelas
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa-pdw.md)]

Tabelas são objetos de banco de dados que contêm todos os dados em um banco de dados. Nas tabelas, os dados são organizados de maneira lógica em um formato de linha-e-coluna semelhante ao de uma planilha. Cada linha representa um registro exclusivo e cada coluna representa um campo no registro. Por exemplo, uma tabela que contém dados de funcionários de uma empresa pode conter uma linha para cada funcionário e colunas representando as informações sobre o funcionário, como número, nome, endereço, cargo e número do telefone residencial do funcionário. 

- O número de tabelas em um banco de dados é limitado apenas pelo número de objetos permitidos em um banco de dados (2.147.483.647). Uma tabela definida pelo usuário padrão pode ter até 1.024 colunas. O número de linhas na tabela são está limitado apenas pela capacidade de armazenamento do servidor. 

- Você pode atribuir propriedades à tabela e a cada coluna na tabela para controlar os dados que são permitidos e outras propriedades. Por exemplo, você poderá criar restrições em uma coluna para desaprovar valores nulos ou fornecer um valor padrão se um valor não for especificado, ou você poderá atribuir uma restrição chave na tabela que impõe exclusividade ou define uma relação entre tabelas. 

- Os dados da tabela podem ser compactados por linha ou por página. A compactação de dados pode permitir armazenar mais linhas em uma página. Para saber mais, veja [Data Compression](../../relational-databases/data-compression/data-compression.md). 

## <a name="types-of-tables"></a>Tipos de tabelas
 Além da função padrão de tabelas básicas definidas pelo usuário, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece os tipos de tabelas a seguir que servem para propósitos especiais em um banco de dados. 

### <a name="partitioned-tables"></a>Tabelas particionadas

As tabelas particionadas são aquelas cujos dados são divididos horizontalmente em unidades que podem ser disseminadas por mais de um grupo de arquivos em um banco de dados. O particionamento facilita o gerenciamento de tabelas ou índices grandes permitindo o acesso ou o gerenciamento de subconjuntos de dados de forma rápida e eficaz, enquanto mantém a integridade geral da coleção. Por padrão, o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oferece suporte a até 15.000 partições. Para saber mais, confira [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).

### <a name="temporary-tables"></a>Tabelas temporárias

As tabelas temporárias são armazenadas em **tempdb**. Há dois tipos de tabelas temporárias: local e global. Elas diferem uma da outra pelo nome, visibilidade e disponibilidade. As tabelas temporárias locais têm um único sinal numérico (#) como primeiro caractere no nome; elas são visíveis somente na conexão atual para o usuário e são excluídas quando o usuário se desconecta da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As tabelas temporárias globais têm dois sinais numéricos (##) como primeiros caracteres no nome; elas são visíveis a qualquer usuário após serem criadas e são excluídas quando todos os usuários que consultam a tabela se desconectam da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 


#### <a name="reduced-recompilations-for-workloads-using-temporary-tables-across-multiple-scopes"></a><a name="ctp23"></a> Recompilações reduzidas para cargas de trabalho usando tabelas temporárias em vários escopos

[!INCLUDE[ss2019](../../includes/sssqlv15-md.md)] em todos os níveis de compatibilidade do banco de dados reduz recompilações para cargas de trabalho usando tabelas temporárias em vários escopos. Esse recurso também está habilitado no Banco de Dados SQL do Azure em nível de compatibilidade do banco de dados 150 para todos os modelos de implantação.  Antes desse recurso, ao fazer referência a uma tabela temporária com uma instrução DML (linguagem de manipulação de dados) (`SELECT`, `INSERT`, `UPDATE`, `DELETE`), se a tabela temporária tivesse sido criada por um lote de escopo externo, isso resultaria em uma recompilação da instrução DML cada vez que ela fosse executada. Com essa melhoria, o SQL Server executa verificações adicionais leves para evitar recompilações desnecessárias:

- Verifique se o módulo de escopo externo usado para criar a tabela temporária em tempo de compilação é a mesma usada para execuções consecutivas. 
- Controle quaisquer alterações de DDL (linguagem de definição de dados) feitas na compilação inicial e compare-as com as operações de DDL para execuções consecutivas.

O resultado final é uma redução de recompilações desnecessárias e sobrecarga de CPU.

### <a name="system-tables"></a>Tabelas do sistema

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazena os dados que definem a configuração do servidor e todas as suas tabelas em um conjunto especial de tabelas conhecido como tabelas do sistema. Usuários não podem consultar nem atualizar diretamente as tabelas do sistema. A informações das tabelas do sistema são disponibilizadas por meio de exibições do sistema. Para obter mais informações, veja [Exibições do sistema &#40;Transact-SQL&#41;](../../t-sql/language-reference.md). 
 
### <a name="wide-tables"></a>Tabelas largas

As tabelas largas usam [colunas esparsas](../../relational-databases/tables/use-sparse-columns.md) para aumentar para 30.000 o total de colunas que uma tabela pode ter. Colunas esparsas são colunas comuns que têm um armazenamento otimizado para valores nulos. Elas reduzem os requisitos de espaço para valores nulos às custas de maior sobrecarga para recuperar valores não nulos. Uma tabela ampla definiu um [conjunto de colunas](../../relational-databases/tables/use-column-sets.md), que é uma representação em XML sem-tipo que combina todas as colunas esparsas de uma tabela em uma saída estruturada. O número de índices e estatísticas também é aumentado para 1.000 e 30.000, respectivamente. O tamanho máximo de uma linha de tabela larga é de 8.019 bytes. Portanto, a maior parte dos dados contidos em qualquer linha específica deve ser NULL. O número máximo de colunas não esparsas mais as colunas computadas de uma tabela larga continua sendo 1.024. 

Tabelas largas têm as implicações de desempenho a seguir.

- Tabelas amplas podem aumentar o custo de manutenção dos índices na tabela. É recomendável que o número de índices em uma tabela larga seja limitado aos índices exigidos pela lógica de negócios. Se o número de índices aumenta, aumentam também o tempo de compilação DML e os requisitos de memória. Os índices não clusterizados devem ser índices filtrados aplicados a subconjuntos de dados. Para saber mais, confira [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md). 

- Os aplicativos podem adicionar e remover colunas de tabelas largas dinamicamente. Quando colunas são adicionadas ou removidas, os planos de consulta compilados também são invalidados. É recomendável criar um aplicativo de modo que ele corresponda à carga de trabalho projetada, para que as alterações de esquema sejam minimizadas. 

- Quando dados são adicionados e removem de uma tabela larga, o desempenho pode ser afetado. Os aplicativos devem ser criados para a carga de trabalho projetada, de forma que as alterações nos dados das tabelas sejam minimizadas. 

- Limite a execução de instruções DML em uma tabela larga que atualizam várias linhas de uma chave de clustering. Essas instruções podem exigir recursos de memória consideráveis para compilar e executar. 

- As operações de alternância de partição em tabelas largas podem ser lentas e exigir muita memória para serem processadas. Os requisitos de desempenho e memória são proporcionais ao total de colunas nas partições de origem e de destino. 

- Os cursores de atualização que atualizam colunas específicas de uma tabela larga devem listar as colunas explicitamente na cláusula FOR UPDATE. Isso ajudará a otimizar o desempenho quando você usar cursores. 

## <a name="common-table-tasks"></a>Tarefas comuns de tabela
 A tabela a seguir fornece links a tarefas comuns associadas à criação ou modificação de uma tabela. 

|Tarefas de tabela|Tópico|
|-----------------|-----------|
|Descreve como criar uma tabela.|[Criar tabelas &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/create-tables-database-engine.md)|
|Descreve como excluir uma tabela.|[Excluir tabelas &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/delete-tables-database-engine.md)|
|Descreve como criar uma nova tabela que contém algumas ou todas as colunas em uma tabela existente.|[Duplicar tabelas](../../relational-databases/tables/duplicate-tables.md)|
|Descreve como renomear uma tabela.|[Renomear tabelas &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/rename-tables-database-engine.md)|
|Descreve como exibir as propriedades da tabela.|[Exibir a definição da tabela](../../relational-databases/tables/view-the-table-definition.md)|
|Descreve como determinar se outros objetos, como uma exibição ou procedimento armazenado, dependem de uma tabela.|[Exibir as dependências de uma tabela](../../relational-databases/tables/view-the-dependencies-of-a-table.md)|

 A tabela a seguir fornece links a tarefas comuns associadas à criação ou modificação de colunas em uma tabela. 

|Tarefas de coluna|Tópico|
|------------------|-----------|
|Descreve como adicionar colunas a uma tabela existente.|[Adicionar colunas a uma tabela &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/add-columns-to-a-table-database-engine.md)|
|Descreve como excluir colunas de uma tabela.|[Excluir colunas de uma tabela](../../relational-databases/tables/delete-columns-from-a-table.md)|
|Descreve como alterar o nome de uma coluna.|[Renomear colunas &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/rename-columns-database-engine.md)|
|Descreve como copiar colunas de uma tabela para outra, copiando apenas a definição da coluna ou a definição e os dados.|[Copiar colunas de uma tabela para outra &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/copy-columns-from-one-table-to-another-database-engine.md)|
|Descreve como modificar uma definição de coluna, alterando o tipo de dados ou outra propriedade.|[Modificar colunas &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/modify-columns-database-engine.md)|
|Descreve como alterar a ordem na qual as colunas aparecem.|[Alterar ordem das colunas em uma tabela](../../relational-databases/tables/change-column-order-in-a-table.md)|
|Descreve como criar uma coluna computada em uma tabela.|[Especificar colunas computadas em uma tabela](../../relational-databases/tables/specify-computed-columns-in-a-table.md)|
|Descreve como especificar um valor padrão para uma coluna. Este valor é usado quando outro valor não é fornecido.|[Especificar valores padrão para colunas](../../relational-databases/tables/specify-default-values-for-columns.md)|

## <a name="see-also"></a>Consulte Também
 [Restrições de chave primária e estrangeira](../../relational-databases/tables/primary-and-foreign-key-constraints.md) [Restrições exclusivas e restrições de verificação](../../relational-databases/tables/unique-constraints-and-check-constraints.md)