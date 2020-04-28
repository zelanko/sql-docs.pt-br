---
title: Transações em tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2cd07d26-a1f1-4034-8d6f-f196eed1b763
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c953060e082ade1e325589cc712f723dabb4909d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175387"
---
# <a name="transactions-in-memory-optimized-tables"></a>Transações em tabelas com otimização de memória
  O controle de versão de linha em tabelas baseadas em disco (usando o isolamento SNAPSHOT ou READ_COMMITTED_SNAPSHOT) fornece um formulário de controle de simultaneidade otimista. Os leitores e gravadores não bloqueiam um ao outro. Com as tabelas com otimização de memória, gravadores não bloqueiam gravadores. Com o controle de versão de linha em tabelas baseadas em disco, uma transação bloqueia a linha e as transações simultâneas que tentassem atualizar a linha estariam bloqueadas. Não há bloqueio com tabelas com otimização de memória. Em vez disso, se duas transações tentassem atualizar a mesma linha, ocorreria um conflito de gravação/gravação (erro 41302).

 Ao contrário das tabelas baseadas em disco, as tabelas com otimização de memória permitem o controle de simultaneidade otimista com os níveis de isolamento mais altos, REPEATABLE READ e SERIALIZABLE. Os bloqueios não são aplicados para impor os níveis de isolamento. Em vez disso, no final da transação, uma validação assegura as suposições de serialização ou leitura repetida. Se as suposições forem violadas, a transação será encerrada. Para obter mais informações, consulte [Transaction Isolation Levels](../../2014/database-engine/transaction-isolation-levels.md).

 As semânticas de transação importantes para tabelas com otimização de memória são:

-   Controle de várias versões

-   Isolamento de transação com base em instantâneo

-   Otimistas

-   Detecção de conflitos

 Cada uma dessas semânticas é explicada nas seções a seguir.

## <a name="multi-versioning-in-memory-optimized-tables"></a>Controle de várias versões em tabelas com otimização de memória
 As linhas em tabelas com otimização de memória podem ter versões diferentes. As transações simultâneas possivelmente acessam versões diferentes da mesma linha.

 Os dados da tabela com otimização da memória são baseados em versão. Para qualquer linha pode haver diferentes versões de linha que são válidas em diferentes momentos. As tabelas baseadas em disco mantêm diferentes versões de linha quando READ_COMMITTED_SNAPSHOT ou ALLOW_SNAPSHOT_ISOLATION são definidos como ON. As tabelas com otimização de memória mantêm diferentes versões de linha, mesmo se READ_COMMITTED_SNAPSHOT e ALLOW_SNAPSHOT_ISOLATION estiverem OFF. As versões de linha das tabelas com otimização de memória não são mantidas em tempdb. Em vez disso, as versões de linha são mantidas embutidas, como parte das estruturas de dados com otimização de memória que armazenam as linhas na memória.

## <a name="snapshot-based-transaction-isolation-for-memory-optimized-tables"></a>Isolamento da transação com base em instantâneos para tabelas com otimização de memória
 Todas as operações em uma única transação usam o mesmo instantâneo transacionalmente consistente das tabelas com otimização de memória. Todo isolamento de transação para tabelas com otimização de memória se baseia em instantâneo. Por exemplo, uma transação que usa o nível de isolamento serializável para acessar tabelas com otimização de memória executará todas as operações no mesmo instantâneo transacionalmente consistente.

 As transações que acessam tabelas com otimização de memória usam esse controle de versão de linha para obter um instantâneo transacionalmente consistente de linhas nas tabelas. Os dados lidos por qualquer instrução na transação serão a versão transacionalmente consistente dos dados que existia no momento em que a transação foi iniciada. Portanto, todas as modificações feitas pelas transações em execução simultaneamente não ficarão visíveis para instruções na transação atual.

## <a name="optimistic-concurrency-control-for-memory-optimized-tables"></a>Controle de simultaneidade otimista para tabelas com otimização de memória
 Os conflitos e as falhas são raros e as transações em tabelas com otimização de memória supõem que não há conflitos com transações e operações simultâneas realizadas com êxito. As transações não utilizam bloqueios ou travas na tabela com otimização de memória para garantir o isolamento da transação. Os gravadores não bloqueiam leitores. O gravadores não bloqueiam gravadores. Em vez disso, as transações prosseguem sob a suposição (otimista) de que não haverá conflitos com outras transações. Não usar bloqueios e travas e não esperar outras transações para concluir o processamento das mesmas linhas melhora o desempenho.

 Além disso, se uma transação (TxA) ler linhas que foram inseridas ou modificadas por outra transação (TxB) que está no processo de confirmação, ela suporá, de forma otimista, que a outra transação será confirmada, em vez de aguardar que a confirmação ocorra. Nesse caso, a transação TxA terá uma dependência de confirmação da transação TxB.

## <a name="conflict-detection-validation-and-commit-dependency-checks"></a>Verificações de detecção de conflito, validação e dependência de confirmação
 O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] detecta os conflitos entre transações simultâneas, bem como violações no nível de isolamento, e condenará uma das transações conflitantes. Essa transação precisará ser repetida. (Para obter mais informações, consulte [Guidelines for Retry Logic for Transactions on Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md).)

 De modo otimista, o sistema supõe que não há conflitos nem violações de isolamento da transação. Se ocorrerem conflitos que possam causar inconsistências no banco de dados ou que possam violar o isolamento da transação, eles serão detectados e a transação será encerrada.

 Se um conflito for detectado, a transação será encerrada e o cliente precisará repetir.

 A tabela a seguir resume as condições de erro para transações que acessam tabelas com otimização de memória.

### <a name="error-conditions-for-transactions-accessing-memory-optimized-tables"></a>Condições de erro das transações que acessam tabelas com otimização de memória.

|Erro|Cenário|
|-----------|--------------|
|Conflito de gravação. Tentando atualizar um registro que foi atualizado desde que a transação foi iniciada.|ATUALIZAR ou EXCLUIR uma linha que foi atualizada ou excluída por uma transação simultânea.|
|Falha de validação de leitura repetida.|Uma linha que foi lida pela transação foi alterada (atualizada ou excluída) desde que a transação foi iniciada. A validação de leitura repetida geralmente ocorre ao usar os níveis de isolamento da transação REPEATABLE READ e SERIALIZABLE.|
|Falha de validação serializável.|Uma linha nova (fantasma) foi inserida em um dos intervalos de verificação na transação, desde que a transação foi iniciada. A linha estaria visível para a transação se a linha tivesse sido confirmada no banco de dados antes do início da transação. A validação SERIALIZABLE normalmente ocorre ao usar o isolamento SERIALIZABLE e validar as restrições PRIMARY KEY.|
|Falha de dependência de confirmação.|A transação obteve uma dependência em outra transação, que não foi confirmada, devido a uma das falhas nessa tabela, a uma condição de insuficiência de memória ou à falha de confirmação no log de transações. Essa falha pode ocorrer com transações de leitura/gravação e somente leitura.|

### <a name="transaction-lifetime"></a>Tempo de vida da transação
 As falhas mencionadas na tabela anterior podem ocorrer em pontos diferentes durante a transação. A figura a seguir ilustra as fases de uma transação que acessa tabelas com otimização de memória.

 ![Tempo de vida de uma transação.](../../2014/database-engine/media/hekaton-transactions.gif "Tempo de vida de uma transação.")
Tempo de vida de uma transação que acessa tabelas com otimização de memória.

#### <a name="regular-processing"></a>Processamento regular
 Nessa fase, as instruções [!INCLUDE[tsql](../includes/tsql-md.md)] emitidas pelo usuário são executadas. As linhas são lidas das tabelas, e as novas versões de linha são gravadas no banco de dados. A transação é isolada de todas as outras transações simultâneas. A transação utiliza o instantâneo das tabelas com otimização de memória que existe no início da transação.

 As gravações nas tabelas nessa fase da transação ainda não estão visíveis para outras transações, com uma exceção: as atualizações e exclusões de linha são visíveis para operações de atualização e exclusão em outras transações, de modo a detectar conflitos de gravação.

 Se uma operação de atualização ou exclusão que vê que uma linha foi atualizada ou excluída desde o início lógico da transação, a operação falhará com o erro 41302. A mensagem do erro 41302 é "A transação atual tentou atualizar um registro na tabela X que foi atualizado desde que esta transação foi iniciada. A transação foi anulada".

 Esse erro sempre condena a transação (mesmo que XACT_ABORT esteja como OFF), o que significa que a transação será revertida quando a sessão do usuário termina. As transações condenadas não podem ser confirmadas e somente dão suporte a operações de leitura que não são gravadas no log e não acessam tabelas com otimização de memória.

#####  <a name="commit-dependencies"></a><a name="cd"></a>Dependências de confirmação
 Durante o processamento regular, uma transação pode ler as linhas gravadas por outras transações que estão na fase de validação ou confirmação, mas que ainda não foram confirmadas. As linhas são visíveis, pois a hora de término lógica das transações foi atribuída no início da fase de validação.

 Se uma transação ler essas linhas não confirmadas, ela obterá uma dependência de confirmação nessa transação. Isso tem duas consequências importantes:

-   A transação não pode confirmar até que as transações das quais ela depende tenham sido confirmadas. Em outras palavras, ela não pode entrar na fase de confirmação até que todas as dependências tenham sido eliminadas.

-   Além disso, os conjuntos de resultados não são retornados ao cliente até que todas as dependências tenham sido eliminadas. Isso impede que o cliente observe dados não confirmados.

 Se alguma das transações dependentes não for confirmada, haverá uma falha de dependência de confirmação. Isso significa que a transação falhará ao ser confirmada apresentando o erro 41301 ("Uma transação anterior na qual a transação atual obteve uma dependência foi anulada, e a transação atual não pode mais ser confirmada.").

#### <a name="validation-phase"></a>Fase de validação
 Durante a fase de validação, o sistema verifica se as suposições necessárias para o nível de isolamento da transação solicitado são verdadeiras entre o início e o término lógicos da transação.

 No início da fase de validação, a transação é atribuída a uma hora de término lógica. As versões de linha gravadas no banco de dados se tornarão visíveis para outras transações na hora de término lógica. Para obter mais informações, consulte [Dependências de confirmação](#cd).

##### <a name="repeatable-read-validation"></a>Validação de leitura repetida
 Se o nível de isolamento da transação for REPEATABLE READ ou SERIALIZABLE, ou as tabelas forem acessadas no isolamento REPEATABLE READ ou SERIALIZABLE (para obter mais informações, consulte a seção sobre Isolamento de operações individuais em [Transaction Isolation Levels](../../2014/database-engine/transaction-isolation-levels.md)), o sistema confirmará que as leituras são repetidas. Isso significa que ele confirmará que as versões das linhas lidas pela transação ainda são versões de linha válidas na hora de término lógica da transação.

 Se alguma das linhas for atualizada ou alterada, a transação falhará ao confirmar apresentando o erro 41305 ("A transação atual não foi confirmada devido a uma falha de validação de leitura repetida.").

 Esse erro também poderá ocorrer se uma tabela for descartada após uma operação de inserção, atualização ou exclusão e antes da confirmação da transação. Isso se aplica apenas às operações de inserção, atualização ou exclusão em procedimentos armazenados compilados nativamente. Essas operações de gravação executadas por meio do [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado fazem com que a instrução DROP TABLE seja bloqueada e aguarde até que a transação seja confirmada.

##### <a name="serializable-validation"></a>Validação serializável
 A validação serializável é executada em dois casos:

-   Se o nível de isolamento da transação for SERIALIZABLE ou as tabelas forem acessadas no isolamento SERIALIZABLE.

-   Se as linhas forem inseridas em um índice exclusivo, como o índice criado para uma restrição PRIMARY KEY. O sistema valida que nenhuma linha com a mesma chave foi inserida simultaneamente.

 O sistema valida que nenhuma linha fantasma foi gravada no banco de dados. As operações de leitura executadas pela transação são avaliadas para determinar que nenhuma linha nova foi inserida nos intervalos de verificação dessas operações de leitura.

 A inserção de uma chave em um índice exclusivo inclui uma operação de leitura implícita, de modo a determinar que a chave não é uma duplicação. A validação serializável para índices exclusivos assegura que esses índices não possam ter duplicatas no caso de duas transações inserirem simultaneamente a mesma chave.

 Se linhas fantasmas forem detectadas, a transação falhará ao confirmar apresentando o erro 41325 ("A transação atual não foi confirmada devido a uma falha de validação serializável.").

#### <a name="commit-processing"></a>Processamento de confirmação
 Se a validação for bem-sucedida e todas as dependências de transação forem eliminadas, a transação entrará na fase de processamento de confirmação. Nessa fase, as alterações nas tabelas duráveis são gravadas no log e o log é gravado no disco, para garantir a durabilidade. Uma vez que o registro de log da transação foi gravado no disco, o controle é retornado para o cliente.

 Todas as dependências de confirmação nessa transação serão eliminadas e todas as transações que estiveram aguardando por essa transação para serem confirmadas poderão prosseguir.

## <a name="limitations"></a>Limitações

-   As transações entre bancos de dados não têm suporte com tabelas com otimização de memória. Cada transação que acessa tabelas com otimização de memória não pode acessar mais de um banco de dados, com exceção do acesso de leitura-gravação ao tempdb e o acesso somente leitura ao mestre do banco de dados do sistema.

-   As transações distribuídas não têm suporte com tabelas com otimização de memória. As transações distribuídas iniciadas com BEGIN DISTRIBUTED TRANSACTION não podem acessar tabelas com otimização de memória.

-   As tabelas com otimização de memória não oferecem suporte a bloqueio. Os bloqueios explícitos por meio de dicas de bloqueio (como TABLOCK, XLOCK, ROWLOCK) não têm suporte com tabelas com otimização de memória.

## <a name="see-also"></a>Consulte Também
 [Compreendendo transações em tabelas com otimização de memória](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)


