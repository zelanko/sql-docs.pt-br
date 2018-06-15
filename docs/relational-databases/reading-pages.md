---
title: Lendo páginas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: relational-databases-misc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- server-general
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- pages
ms.assetid: f8da760e-aacb-4661-9f3a-2578d8c11e4e
caps.latest.revision: 3
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 34fc49117e2d406b58a8dce9731b8fdf89634c52
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32957421"
---
# <a name="reading-pages"></a>Lendo páginas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A E/S de uma instância do SQL Server [!INCLUDE[ssDE](../includes/ssde-md.md)] inclui leituras lógicas e físicas. Uma leitura lógica ocorre sempre que o [!INCLUDE[ssDE](../includes/ssde-md.md)] solicita uma página do [cache do buffer](../relational-databases/memory-management-architecture-guide.md). Se a página não estiver atualmente no cache do buffer, a leitura física copiará primeiramente a página de disco no cache.

As solicitações de leitura geradas por uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] são controladas pelo mecanismo relacional e otimizadas pelo mecanismo de armazenamento. O mecanismo relacional determina o método de acesso (como um exame de tabela, um exame de índice ou uma leitura de chave) mais efetivo; os métodos de acesso e os componentes do gerenciador de buffer do mecanismo de armazenamento determinam o padrão geral de leituras a serem executadas e otimizam as leituras exigidas para implementar o método de acesso. O thread que executa o lote agenda as leituras.

## <a name="read-ahead"></a>Read-Ahead
O [!INCLUDE[ssDE](../includes/ssde-md.md)] oferece suporte a um mecanismo de otimização de desempenho chamado read-ahead. O read-ahead antecipa os dados e as páginas de índice necessários para atender a um plano de execução de consulta e traz as páginas ao cache do buffer antes de elas serem realmente usadas pela consulta. Isso permite a sobreposição da computação e da E/S, aproveitando ao máximo a CPU e o disco. 

O mecanismo read-ahead permite ao [!INCLUDE[ssDE](../includes/ssde-md.md)] ler até 64 páginas contíguas (512KB) de um arquivo. A leitura é executada como uma única leitura de dispersão e coleta para o número apropriado (provavelmente não contíguo) de buffers no cache do buffer. Se alguma página do intervalo já estiver presente no cache do buffer, a página correspondente da leitura será descartada quando ela for concluída. O intervalo de páginas também pode ser “cortado” em qualquer ponto se as páginas correspondentes já estiverem presentes no cache.

Há dois tipos de read-ahead: um para páginas de dados e um para páginas de índice.

### <a name="reading-data-pages"></a>Lendo Páginas de dados
Exames de tabela usados para ler páginas de dados são muito eficientes no [!INCLUDE[ssDE](../includes/ssde-md.md)]. As páginas IAM (Index Allocation Map) em um banco de dados do SQL Server listam as extensões usadas por uma tabela ou um índice. O mecanismo de armazenamento pode ler a página IAM para criar uma lista ordenada de endereços de disco que deve ser lida. Isso permite ao mecanismo de armazenamento otimizar suas E/S como grandes leituras sequenciais, executadas em sequência, com base em seu local no disco. Para saber mais sobre as páginas IAM, veja [Gerenciando espaço usado por objetos](../relational-databases/pages-and-extents-architecture-guide.md).

### <a name="reading-index-pages"></a>Lendo páginas de índice
O mecanismo de armazenamento lê páginas de índice em série na ordem de chave. Por exemplo, essa ilustração mostra uma representação simplificada de um conjunto de páginas folha que contém um conjunto de chaves e o nó de índice intermediário que mapeia as páginas folha. Para saber mais sobre a estrutura de páginas em um índice, veja [Estruturas de índice clusterizado](../relational-databases/pages-and-extents-architecture-guide.md).

![Reading_Pages](../relational-databases/media/reading-pages.gif)

O mecanismo de armazenamento usa as informações na página de índice intermediário acima do nível folha para agendar read-aheads consecutivos para as páginas que contêm as chaves. Se uma solicitação for feita para todas as chaves de ABC para DEF, o mecanismo de armazenamento primeiro lerá a página de índice acima da página folha. No entanto, ele não lê cada página de dados em sequência da página 504 a 556 (a última página com chaves no intervalo especificado). Em vez disso, o mecanismo de armazenamento examina a página de índice intermediário e cria uma lista de páginas folha que deve ser lida. O mecanismo de armazenamento agenda todas as leituras em ordem de chave. O mecanismo de armazenamento também reconhece que as páginas 504/505 e 527/528 são contíguas e executa uma única leitura de dispersão para recuperar as páginas adjacentes em uma única operação. Quando há muitas páginas a serem recuperadas em uma operação consecutiva, o mecanismo de armazenamento agenda um bloco de leituras por vez. Quando um subconjunto dessas leituras é concluído, o mecanismo de armazenamento agenda um número igual de leituras novas até que todas as leituras exigidas sejam agendadas.

O mecanismo de armazenamento usa a pré-busca para acelerar as pesquisas de tabela base de índices não cluster. As linhas de folha de um índice não clusterizado contêm ponteiros para as linhas de dados que contém cada valor de chave específico. Como o mecanismo de armazenamento lê as páginas de folha do índice não clusterizado, também inicia o agendamento de leituras assíncronas das linhas de dados cujos ponteiros já foram recuperados. Isso permite ao mecanismo de armazenamento recuperar linhas de dados da tabela subjacente antes de concluir o exame do índice não clusterizado. A pré-busca é usada independentemente de a tabela ter um índice clusterizado. O SQL Server Enterprise usa mais pré-buscas do que as outras edições do SQL Server, permitindo que a leitura read-ahead seja feita em um número maior de páginas. O nível de pré-busca não é configurável em nenhuma edição. Para saber mais sobre índices não clusterizados, veja [Estruturas de índice não clusterizado](../relational-databases/pages-and-extents-architecture-guide.md).

## <a name="advanced-scanning"></a>Exame avançado
No SQL Server Enterprise, o recurso de verificação avançada permite que diversas tarefas compartilhem verificações de tabelas completas. Se o plano de execução de uma instrução Transact-SQL exigir um exame das páginas de dados em uma tabela e o [!INCLUDE[ssDE](../includes/ssde-md.md)] detectar que a tabela já está sendo examinada para outro plano de execução, o [!INCLUDE[ssDE](../includes/ssde-md.md)] associará o exame à primeira, no local atual do segundo exame. O [!INCLUDE[ssDE](../includes/ssde-md.md)] lê uma vez cada página e passa as linhas de cada página para ambos os planos de execução. Isso continua até o término da tabela ser alcançado. 

Nesse ponto, o primeiro plano de execução tem os resultados completos de um exame, mas o segundo plano de execução ainda precisa recuperar as páginas de dados que eram lidas antes de serem associadas ao exame em andamento. O exame do segundo plano de execução volta para a primeira página de dados da tabela e examina mais adiante o local em que ele foi associado ao primeiro exame. Qualquer número de exames pode ser combinado dessa forma. O [!INCLUDE[ssDE](../includes/ssde-md.md)] continuará executando loop pelas páginas de dados até que sejam concluídos todos os exames. Esse mecanismo também é conhecido como “exame carrossel” e demonstra o motivo pelo qual a ordem dos resultados retornada de uma instrução SELECT não pode ser garantida sem uma cláusula ORDER BY. 

Por exemplo, suponha que você tenha uma tabela com 500.000 páginas. O UserA executa uma instrução Transact-SQL que exige um exame da tabela. Quando esse exame tiver processado 100.000 páginas, o UserB executará outra instrução Transact-SQL que examinará a mesma tabela. O [!INCLUDE[ssDE](../includes/ssde-md.md)] agendará um conjunto de solicitações de leitura para as páginas após 100.001 e passará as linhas de cada página de volta para ambos os exames. Quando o exame alcançar 200.000 páginas, o UserC executará outra instrução Transact-SQL que examinará a mesma tabela. Iniciando com a página 200.001, o [!INCLUDE[ssDE](../includes/ssde-md.md)] passará as linhas de cada página lida de volta para todas os três exames. Depois de ler a linha 500.000, o exame do UserA será concluído, e os exames do UserB e UserC voltarão para o início e começarão a ler as páginas começando com a página 1. Quando o [!INCLUDE[ssDE](../includes/ssde-md.md)] alcançar a página 100.000, o exame do UserB estará concluído. O exame do UserC continuará sendo executado sozinho até alcançar a página 200.000. Nesse ponto, todos os exames estarão concluídos. 

Sem o exame avançado, cada usuário teria de competir pelo espaço do buffer e isso causaria a contenção do braço do disco. As mesmas páginas seriam lidas uma vez para cada usuário, em vez de serem lidas uma vez e compartilhadas por vários usuários, reduzindo a velocidade do desempenho e sobrecarregando os recursos.

## <a name="see-also"></a>Consulte Também
[Guia de arquitetura de página e extensões](../relational-databases/pages-and-extents-architecture-guide.md)   
 [Gravando Páginas](../relational-databases/writing-pages.md)
