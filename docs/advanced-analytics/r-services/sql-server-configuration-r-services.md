---
title: "Configura&#231;&#227;o do SQL Server (R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4b08969f-b90b-46b3-98e7-0bf7734833fc
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# Configura&#231;&#227;o do SQL Server (R Services)
As informações nesta seção fornecem orientação geral sobre a configuração de hardware e de rede do computador que é usado para hospedar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Ele deve ser considerado além gerais [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] informações fornecidas de ajuste de desempenho de [Center de desempenho para o mecanismo de banco de dados do SQL Server e banco de dados SQL](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## Processador

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] pode executar tarefas em paralelo usando núcleos disponíveis na máquina. mais núcleos disponíveis, melhor o desempenho. Uma vez que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] é normalmente usado por vários usuários simultaneamente, o administrador de banco de dados deve determinar o número ideal de núcleos que são necessários para dar suporte a cálculos de carga de trabalho de pico. Embora o número de núcleos pode não ajudar para operações vinculadas de e/s, vinculadas à CPU algoritmos irão se beneficiar com CPUs mais rápidas com vários núcleos.

## Memória

A quantidade de memória disponível no computador pode ter um grande impacto sobre o desempenho dos algoritmos analíticos avançados. Memória insuficiente pode afetar o grau de paralelismo ao usar o contexto de computação do SQL. Ele também pode afetar o tamanho da parte (linhas por operação de leitura) que pode ser processado e o número de sessões simultâneas que podem ser suportados.

Um mínimo de 32GB é altamente recomendável. Se você tiver mais de 32GB disponível, você pode configurar a fonte de dados SQL para usar mais linhas em cada operação de leitura para melhorar o desempenho.

## Opções de energia

No sistema operacional Windows, o __alto desempenho__ energia deve ser usada. Usar uma configuração de energia diferente resultará em desempenho reduzido ou inconsistente ao usar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].

## E/s de disco

Trabalhos de treinamento e previsão usando [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] são inerentemente de e/s associada e depende da velocidade do disco que o banco de dados é armazenado no. Unidades mais rápidas, como unidades de estado sólido (SSD) podem ajudar. 

E/s de disco também é afetado por outros aplicativos que acessam o disco: por exemplo, ler operações em um banco de dados por outros clientes. Desempenho de e/s de disco também pode ser afetado pelas configurações no sistema de arquivos em uso, como o tamanho do bloco utilizado pelo sistema de arquivos. Se houver várias unidades, armazenar os bancos de dados em uma unidade diferente [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] assim que as solicitações para [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] não está atingindo o mesmo disco como as solicitações de dados armazenados no banco de dados.

E/s de disco substancialmente pode afetar o desempenho durante a execução RevoScaleR funções analíticas que usam várias iterações durante o treinamento. Por exemplo, `rxLogit`, `rxDTree`, `rxDForest` e `rxBTrees` todos usam várias iterações. Quando a fonte de dados é [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], esses algoritmos usam arquivos temporários que são otimizados para capturar os dados. Esses arquivos são limpas automaticamente após a sessão. Ter um disco de alto desempenho para operações de leitura/gravação pode melhorar significativamente o tempo total decorrido para esses algoritmos.

> [!NOTE]
> [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] requer suporte de nome de arquivo 8.3 em sistemas operacionais Windows. Você pode usar fsutil.exe para determinar se uma unidade oferece suporte a nomes de 8.3 arquivo, ou se não habilitar o suporte. Para obter mais informações sobre como usar fsutil.exe com nomes de 8.3 arquivo, consulte [Fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx).

### Compactação de tabela

Desempenho de e/s geralmente pode ser melhorado usando compactação ou columstore índices. Em geral, dados geralmente são repetidos em várias colunas dentro de uma tabela, para que usar um índice columnstore aproveita esses repetições ao compactar os dados.

Um índice columnstore não pode ser mais eficiente se houver muitas inserções na tabela, mas é uma boa opção se os dados são estáticos ou altera apenas raramente. Se um repositório de coluna não for apropriado, a habilitação da compactação em uma tabela principal de linha pode ser usada para melhorar a e/s.

Para obter mais informações, consulte os seguintes documentos:

* [Compactação de dados](../../relational-databases/data-compression/data-compression.md)

* [Permitir a compactação em uma tabela ou índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

* [Guia de Índices Columnstore](Columnstore%20Indexes%20Guide.md)

## Arquivo de paginação

O sistema operacional Windows usa um arquivo de paginação para gerenciar os despejos de memória e para armazenar páginas de memória virtual. Se você observar a paginação excessiva, considere aumentar a memória física no computador. Embora ter mais memória física não elimine a paginação, reduz a necessidade de paginação.

A velocidade do disco que o arquivo de paginação é armazenado no também pode afetar o desempenho. Armazenar o arquivo de página em um SSD ou usando vários arquivos de paginação em vários SSDs, pode melhorar o desempenho.

Consulte [como determinar o tamanho do arquivo de página apropriada para versões de 64 bits do Windows](https://support.microsoft.com/en-us/kb/2860880) para obter informações sobre o arquivo de paginação de dimensionamento.

## Governança de recursos

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] oferece suporte a governança de recursos para controlar os vários recursos usados pelo [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Por exemplo, o valor padrão para o consumo de memória por R é limitado a 20% do total de memória disponível para [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Isso é feito para garantir que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] fluxos de trabalho não são gravemente afetados por tarefas de longa duração R. Entretanto, esses limites podem ser alterados pelo administrador de banco de dados. 

Os recursos limitados são __MAX_CPU_PERCENT__, __MAX_MEMORY_PERCENT__, e __MAX_PROCESSES__. Para exibir as configurações atuais, use [!INCLUDE[tsql_md](../../includes/tsql-md.md)] instrução:

```T-SQL
SELECT * FROM sys.resource_governor_external_resource_pools
``` 

Se [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] é principalmente usado para serviços de R, talvez seja útil aumentar MAX_CPU_PERCENT para 40% ou 60%. Se não houver muitas sessões de R usando o mesmo [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ao mesmo tempo, todas as três serão aumentadas. Para alterar os valores de recursos alocado, use [!INCLUDE[tsql_md](../../includes/tsql-md.md)] instruções. 

Este exemplo define o uso de memória para 40%:

```T-SQL
ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)
```
O exemplo a seguir define todos os três valores configuráveis:
```T-SQL
ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`
``` 

> [!NOTE]
> Para fazer alterações nessas configurações entrem em vigor imediatamente, execute a instrução `ALTER RESOURCE GOVERNOR RECONFIGURE` depois de alterar uma memória, CPU ou configuração de processo máximo. 

## Consulte também
[Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)

[CRIAR POOL DE RECURSOS EXTERNOS](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

 [Guia de ajuste de desempenho do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 
 [Estudo de caso de desempenho](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 
 [R e otimização de dados](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)