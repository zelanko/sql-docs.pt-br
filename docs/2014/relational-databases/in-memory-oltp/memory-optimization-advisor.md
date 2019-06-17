---
title: Orientador de Otimização de Memória | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
f1_keywords:
- sql12.swb.memoryoptimizationwizard.f1
- swb.memoryoptimizationwizard.f1
ms.assetid: 181989c2-9636-415a-bd1d-d304fc920b8a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d2fe137a21f2bd48113e65524b4315494f40a49
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63157996"
---
# <a name="memory-optimization-advisor"></a>Orientador de otimização da memória
  A ferramenta de relatórios de desempenho de transação (consulte [Determinando se uma tabela ou um procedimento armazenado deve ser movido para o OLTP na memória](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) informa sobre as tabelas em seu banco de dados que se beneficiarão se forem compatibilizadas para usar o OLTP na memória. Após identificar uma tabela que você gostaria de compatibilizar para usar o OLTP na memória, você poderá usar o orientador de otimização de memória para ajudá-lo a migrar a tabela de banco de dados baseada em disco para o OLTP na memória.  
  
 Para começar, conecte-se à instância que contém a tabela de banco de dados baseada em disco. Você pode se conectar a uma instância do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] . No entanto, se você desejar executar uma operação de migração com o orientador, deverá se conectar a uma instância do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] na qual a funcionalidade de OLTP na memória está habilitada. Para obter mais informações sobre os requisitos de OLTP na memória, consulte [Requirements for Using Memory-Optimized Tables](memory-optimized-tables.md).  
  
 Para obter informações sobre as metodologias de migração, confira [In-Memory OLTP – Common Workload Patterns and Migration Considerations](https://msdn.microsoft.com/library/dn673538.aspx)(OLTP in-memory – Padrões comuns de carga de trabalho e considerações de migração).  
  
## <a name="walkthrough-using-the-memory-optimization-advisor"></a>Passo a passo usando o orientador de otimização da memória  
 No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela que você deseja converter e selecione **Orientador de Otimização da Memória**. Isso exibirá a página de boas-vindas do **Orientador de Otimização da Memória da Tabela**.  
  
### <a name="memory-optimization-checklist"></a>Lista de verificação de otimização da memória  
 Quando você clicar em **Avançar** na página de boas-vindas para o **Orientador de Otimização da Memória da Tabela**, verá a lista de verificação de otimização da memória. As tabelas com otimização de memória não dão suporte a todos os recursos em uma tabela baseada em disco. A lista de verificação de otimização da memória informa se a tabela baseada em disco usa algum recurso que seja incompatível com uma tabela com otimização de memória. O **Orientador de Otimização de Memória de Tabela** não altera a tabela baseada em disco para que possa ser migrada para usar o OLTP in-memory. Você deve fazer essas alterações antes de continuar a migração. Para cada incompatibilidade localizada, o **Orientador de Otimização de Memória de Tabela** exibe um link para informações que podem ajudar a modificar as tabelas baseadas em disco.  
  
 Se quiser manter uma lista dessas incompatibilidades, para planejar a migração, clique em **Gerar Relatório** para gerar uma lista em HTML.  
  
 Se a tabela não tiver nenhuma incompatibilidade e você estiver conectado a uma instância do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] com o OLTP in-memory, clique em **Avançar**.  
  
### <a name="memory-optimization-warnings"></a>Avisos de otimização da memória  
 A página a seguir, avisos de otimização da memória, contém uma lista de problemas que não impedem a tabela de ser migrada para usar o OLTP na memória, mas que podem causar um comportamento inesperado ou a falha de comportamento de outros objetos (como procedimentos armazenados ou funções CLR).  
  
 Os primeiros avisos da lista são informativos e podem ou não ser aplicáveis à tabela. Os links na coluna à direita da tabela terão mais informações.  
  
 A tabela de avisos também exibirá as condições de avisos potenciais que não estão presentes na tabela.  
  
 Os avisos acionáveis terão um triângulo amarelo na coluna à esquerda. Se houver avisos acionáveis, você deverá sair da migração, resolver os avisos e reiniciar o processo. Se você não resolver os avisos, sua tabela migrada poderá causar uma falha.  
  
 Clique em **Gerar Relatório** para gerar um relatório HTML desses avisos. Clique em **Avançar** para continuar.  
  
### <a name="review-optimization-options"></a>Examine as opções de otimização  
 A tela a seguir permite alterar as opções para a migração para OLTP na memória:  
  
 Grupo de arquivos com otimização de memória  
 O nome para o grupo de arquivos com otimização de memória. Para que uma tabela com otimização de memória possa ser criada, um banco de dados deve ter um grupo de arquivos com otimização de memória com pelo menos um arquivo.  
  
 Se você não tiver um grupo de arquivos com otimização de memória, poderá alterar o nome padrão. Os grupos de arquivos com otimização de memória não podem ser excluídos. A existência de um grupo de arquivos com otimização de memória pode desabilitar alguns recursos em nível de banco de dados, como o AUTO CLOSE e o espelhamento de banco de dados.  
  
 Se um banco de dados já tiver um grupo de arquivos com otimização de memória, este campo será pré-populado com o nome e você não poderá alterar o valor desse campo.  
  
 Nome lógico do arquivo e caminho do arquivo  
 O nome do arquivo que conterá a tabela com otimização de memória. Para que uma tabela com otimização de memória possa ser criada, um banco de dados deve ter um grupo de arquivos com otimização de memória com pelo menos um arquivo.  
  
 Se você não tiver um grupo de arquivos com otimização de memória, poderá alterar o nome e o caminho padrão do arquivo a ser criado no fim do processo de migração.  
  
 Se você tiver um grupo de arquivos com otimização de memória existente, esses campos serão pré-populados e você não poderá alterar os valores.  
  
 Renomear a tabela original como  
 Ao término do processo de migração, uma nova tabela com otimização de memória será criada com o nome atual da tabela. Para evitar um conflito de nome, a tabela atual deverá ser renomeada. Você pode alterar esse nome nesse campo.  
  
 Custo estimado da memória atual (MB)  
 O Orientador de Otimização da Memória estima a quantidade de memória que a nova tabela com otimização de memória consumirá com base nos metadados da tabela baseada em disco. O cálculo do tamanho da tabela é explicado em [Tamanho da tabela e da linha em tabelas com otimização de memória](table-and-row-size-in-memory-optimized-tables.md).  
  
 Se não for alocada memória suficiente, o processo de migração poderá falhar.  
  
 Além disso, copie os dados da tabela para a nova tabela com otimização de memória  
 Selecione essa opção se você também quiser mover os dados na tabela atual para uma nova tabela com otimização de memória. Se esta opção não estiver selecionada, a nova tabela com otimização de memória será criada sem linhas.  
  
 A tabela será migrada como uma tabela durável por padrão  
 O OLTP na memória dá suporte a tabelas não duráveis com desempenho superior comparado com as tabelas com otimização de memória duráveis. No entanto, os dados em uma tabela não durável serão perdidos ao reinicializar o servidor.  
  
 Se essa opção for selecionada, o Orientador de Otimização da Memória criará uma tabela não durável em vez de uma tabela durável.  
  
> [!WARNING]  
>  Selecione essa opção apenas se você entender o risco de perda de dados associado a tabelas não duráveis.  
  
 Clique em **Avançar** para continuar.  
  
### <a name="review-primary-key-conversion"></a>Examinar conversão de chaves primárias  
 A tela seguinte é **Examinar Conversão de Chaves Primárias**. O Orientador de Otimização da Memória detectará se há uma ou mais chaves primárias na tabela, e populará a lista de colunas com base nos metadados de chave primária. Caso contrário, se desejar migrar para uma tabela com otimização de memória durável, você deverá criar uma chave primária.  
  
 Se não existir uma chave primária e a tabela estiver sendo migrada para uma tabela não durável, esta tela não aparecerá.  
  
 Para as colunas textuais (colunas com tipos `char`, `nchar`, `varchar` e `nvarchar`), selecione uma ordenação adequada. O OLTP na memória somente dá suporte a ordenações BIN2 para colunas em uma tabela com otimização de memória e não dá suporte a ordenações com caracteres suplementares. Consulte [Páginas de código de ordenações](../../database-engine/collations-and-code-pages.md) para obter informações sobre as ordenações com suporte e o impacto potencial de uma alteração na ordenação.  
  
 Você pode configurar os seguintes parâmetros para a chave primária:  
  
 Selecione um nome novo para essa chave primária  
 O nome da chave primária para essa tabela deve ser exclusivo dentro do banco de dados. É possível alterar o nome da chave primária aqui.  
  
 Selecione o tipo dessa chave primária  
 O OLTP na memória dá suporte a dois tipos de índices em uma tabela com otimização de memória:  
  
-   Um índice NONCLUSTERED HASH. Esse índice é melhor para índices com várias pesquisas de ponto. Você pode configurar o número de buckets para esse índice no campo **Número de Buckets** .  
  
-   Um índice NONCLUSTERED. Esse tipo de índice é melhor para índices com muitas consultas de intervalo. Você pode configurar a ordem de classificação para cada coluna na lista **Coluna e ordem de classificação** .  
  
 Para entender o melhor tipo de índice para sua chave primária, consulte [Índices de hash](../../database-engine/hash-indexes.md).  
  
 Clique em **Avançar** depois de fazer suas escolhas de chave primária.  
  
### <a name="review-index-conversion"></a>Examinar conversão de índice  
 A próxima página é **Examinar conversão de índice**. O Orientador de Otimização da Memória detectará se há um ou mais índices na tabela, e populará a lista de colunas e tipo de dados. Os parâmetros que você pode configurar na página **Examinar conversão de índice** são semelhantes à página anterior, **Examinar conversão de chaves primárias** .  
  
 Se a tabela tiver somente uma chave primária e estiver sendo migrada para uma tabela durável, esta tela não aparecerá.  
  
 Depois de tomar uma decisão para cada índice na tabela, clique em **Avançar**.  
  
### <a name="verify-migration-actions"></a>Verificar ações de migração  
 A próxima página é **Verificar ações de migração**. Para criar o script da operação de migração, clique em **Script** para gerar um script [!INCLUDE[tsql](../../includes/tsql-md.md)] . Você pode em seguida modificar e executar o script. Clique em **Migrar** para iniciar a migração da tabela.  
  
 Depois que o processo estiver concluído, atualize o **Pesquisador de Objetos** para ver a nova tabela com otimização de memória e a antiga tabela baseada em disco. Você pode manter a tabela antiga ou excluí-la de acordo com a conveniência.  
  
## <a name="see-also"></a>Consulte também  
 [Migrando para OLTP na memória](migrating-to-in-memory-oltp.md)  
  
  
