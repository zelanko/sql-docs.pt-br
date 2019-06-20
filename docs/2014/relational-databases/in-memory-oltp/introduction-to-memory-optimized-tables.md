---
title: Introdução às tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ef1cc7de-63be-4fa3-a622-6d93b440e3ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff434efd0a9f4fcb3316143e598e636bff85f487
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63157841"
---
# <a name="introduction-to-memory-optimized-tables"></a>Introdução às tabelas com otimização de memória
  Tabelas com otimização de memória são aquelas criadas com [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql).  
  
 Tabelas com otimização de memória residem na memória. As linhas da tabela são lidas e gravadas na memória. A tabela inteira reside na memória. Uma segunda cópia dos dados da tabela é mantida em disco, mas apenas para fins de durabilidade.  
  
 O OLTP na memória é integrado ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para fornecer uma experiência perfeita em todas as áreas, como desenvolvimento, implantação, capacidade de gerenciamento e suporte. Um banco de dados pode conter objetos residentes na memória e baseados em disco.  
  
 As linhas nas tabelas com otimização de memória têm controle de versão. Isso significa que cada linha da tabela, possivelmente, tem várias versões. Todas as versões de linha são mantidas na mesma estrutura de dados da tabela. O controle de versão de linha é usado para permitir leituras e gravações simultâneas na mesma linha. Para obter mais informações sobre leituras e gravações simultâneas na mesma linha, consulte [Transactions in Memory-Optimized Tables](memory-optimized-tables.md).  
  
 A figura a seguir ilustra o controle de várias versões. A figura mostra uma tabela com três linhas, e cada linha tem versões diferentes.  
  
 ![Controle de várias versões.](../../database-engine/media/hekaton-tables-1.gif "Controle de várias versões.")  
  
 A tabela tem três linhas: r1, r2 e r3. r1 tem três versões, r2 tem duas versões e r3 tem quatro versões. Observe que as versões diferentes da mesma linha não ocupam necessariamente locais de memória consecutivos. As versões de linha diferentes podem ser dispersas em toda a estrutura de dados da tabela.  
  
 A estrutura de dados da tabela com otimização de memória pode ser considerada uma coleção de versões de linha. As linhas nas tabelas baseadas em disco são organizadas em páginas e extensões, e as linhas individuais são resolvidas através do número e do deslocamento da página, as versões de linha nas tabelas com otimização de memória são resolvidas através dos ponteiros de memória de 8 bytes.  
  
## <a name="durability"></a>Durabilidade  
 Por padrão, as tabelas com otimização de memória são completamente duráveis e, assim como as transações em tabelas baseadas em disco (tradicionais), as transações completamente duráveis em tabelas com otimização de memória são completamente ACID (atômicas, consistentes, isoladas e duráveis). As tabelas com otimização de memória e procedimentos armazenados compilados nativamente oferecem suporte a um subconjunto do [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 O OLTP na Memória oferece suporte a tabelas duráveis com a durabilidade da transação atrasada. As transações duráveis atrasadas são salvas em disco logo depois que a transação é confirmada. Em compensação ao desempenho aprimorado, as transações confirmadas que não foram salvas em disco serão perdidas em caso de falha ou failover do servidor.  
  
 Além das tabelas padrão com otimização de memória duráveis, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] também oferece suporte a tabelas com otimização de memória não duráveis, que não são registradas e seus dados não são persistidos no disco. Isso significa que as transações nessas tabelas não requerem nenhuma E/S de disco, mas os dados não serão recuperados se houver falha ou failover do servidor.  
  
## <a name="accessing-data-in-memory-optimized-tables"></a>Acessando dados nas tabelas com otimização de memória  
 Os dados nas tabelas com otimização de memória são acessados de duas maneiras:  
  
-   Com [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado (fora de um procedimento armazenado compilado nativamente). Essas instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] podem ser procedimentos armazenados interpretados internos ou instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] ad hoc.  
  
-   Por meio de procedimentos armazenados compilados nativamente.  
  
 As tabelas com otimização de memória podem ser acessadas com mais eficiência de procedimentos armazenados compilados nativamente ([Procedimentos armazenados compilados nativamente](natively-compiled-stored-procedures.md)). As tabelas com otimização de memória também podem ser acessadas com [!INCLUDE[tsql](../../../includes/tsql-md.md)]interpretado (tradicional). O termo [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado refere-se ao acesso a tabelas com otimização de memória sem um procedimento armazenado compilado nativamente. Alguns exemplos de acesso ao [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado incluem o acesso a uma tabela com otimização de memória de um gatilho DML ou de um lote [!INCLUDE[tsql](../../../includes/tsql-md.md)] ad hoc, exibição e função com valor de tabela.  
  
 A tabela a seguir resume o acesso ao [!INCLUDE[tsql](../../../includes/tsql-md.md)] nativo e interpretado de vários objetos.  
  
|Recurso|Acesso através de um procedimento armazenado compilado nativamente|Acesso [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado|Acesso à CLR|  
|-------------|-------------------------------------------------------|-------------------------------------------|----------------|  
|Tabelas com otimização de memória|Sim|Sim|Não <sup>1</sup>|  
|[Variáveis de tabela com otimização de memória](../../database-engine/memory-optimized-table-variables.md)|Sim|Sim|Não |  
|[Procedimentos armazenados compilados nativamente](https://msdn.microsoft.com/library/dn133184.aspx)|Você não pode usar a instrução EXECUTE para executar nenhum procedimento armazenado em um procedimento armazenado compilado nativamente.|Sim|Não <sup>1</sup>|  
  
 <sup>1</sup> não é possível acessar uma tabela com otimização de memória ou procedimento armazenado compilado nativamente da conexão de contexto (a conexão de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ao executar um módulo CLR). No entanto, é possível criar e abrir outra conexão, da qual você pode acessar tabelas com otimização de memória e procedimentos armazenados compilados nativamente. Para obter mais informações, consulte [vs Regular. Conexões de contexto](../clr-integration/data-access/context-connections-vs-regular-connections.md).  
  
## <a name="performance-and-scalability"></a>Desempenho e escalabilidade  
 Os seguintes fatores afetarão os ganhos de desempenho que podem ser obtidos com o OLTP na memória:  
  
 Comunicação  
 Um aplicativo com muitas chamadas para procedimentos armazenados curtos pode ver um ganho de desempenho menor em comparação com um aplicativo com menos chamadas e mais funcionalidade implementada em cada procedimento armazenado.  
  
 Execução do [!INCLUDE[tsql](../../../includes/tsql-md.md)]  
 O OLTP na memória atinge o melhor desempenho usando procedimentos armazenados compilados nativamente do que usando procedimentos armazenados interpretados ou execução de consulta. Os procedimentos armazenados que executam outros procedimentos armazenados não podem ser compilados nativamente, mas pode ser vantajoso acessar tabelas com otimização de memória nesses procedimentos.  
  
 Varredura de intervalo x pesquisa de ponto  
 Os índices não clusterizados com otimização de memória dão suporte a exames de intervalo e exames ordenados. Para pesquisas de ponto, os índices de hash com otimização de memória têm desempenho melhor que os índices não clusterizados com otimização de memória. Os índices não clusterizados com otimização de memória têm desempenho melhor que os índices baseados em disco.  
  
 As operações de índice não são registradas e existem apenas na memória.  
  
 Simultaneidade  
 Os aplicativos cujo desempenho é afetado pela simultaneidade no nível de mecanismo, como contenção de trava ou bloqueio, melhoram significativamente quando o aplicativo é movido para OLTP na memória.  
  
 A tabela a seguir lista os problemas de desempenho e escalabilidade que geralmente são encontrados em bancos de dados relacionais e como o OLTP na memória pode melhorar o desempenho.  
  
|Problema|Impacto do OLTP na memória|  
|-----------|----------------------------|  
|Desempenho<br /><br /> Alto uso de recursos (CPU, E/S, rede ou memória).|CPU<br /> Os procedimentos armazenados compilados nativamente podem reduzir significativamente o uso da CPU, pois exigem muito menos instruções para executar uma instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] comparada com os procedimentos armazenados interpretados.<br /><br /> O OLTP na memória pode ajudar a reduzir o investimento de hardware em cargas de trabalho expandidas, pois um servidor pode potencialmente fornecer a taxa de transferência de cinco a dez servidores.<br /><br /> E/S<br /> Se você encontrar um gargalo de E/S, do processamento às páginas de dados ou índice, o OLTP na memória poderá reduzir esse gargalo. Além disso, o ponto de verificação de objetos OLTP na memória é contínuo e não resulta em aumentos repentinos nas operações de E/S. No entanto, se o conjunto de trabalho das tabelas críticas de desempenho não se ajustar na memória, o OLTP na memória não melhorará o desempenho, pois ele exige que os dados sejam residentes na memória. Se você encontrar um gargalo de E/S no log, o OLTP na memória poderá reduzi-lo, pois ele gera menos registros. Se uma ou mais tabelas com otimização de memória forem configuradas como tabelas não duráveis, você poderá eliminar o registro de dados.<br /><br /> Memória<br /> O OLTP na memória não oferece nenhum benefício de desempenho. Além disso, o OLTP na memória pode fazer mais pressão na memória, pois os objetos precisam ser residentes na memória.<br /><br /> Rede<br /> O OLTP na memória não oferece nenhum benefício de desempenho. Os dados precisam ser comunicados da camada de dados à camada de aplicativos.|  
|Escalabilidade<br /><br /> A maioria dos problemas de colocação em escala nos aplicativos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é causada por problemas de simultaneidade, como contenção em bloqueios, travas e spinlocks.|Contenção de trava<br /> Um cenário típico é a contenção na última página de um índice na inserção de linhas simultaneamente na ordem de chave. Como o OLTP na memória não usa travas ao acessar dados, os problemas de escalabilidade relacionados a contenções de trava são totalmente removidos.<br /><br /> Contenção de spinlock<br /> Como o OLTP na memória não usa travas ao acessar dados, os problemas de escalabilidade relacionados a contenções de spinlock são totalmente removidos.<br /><br /> Contenção relacionada ao bloqueio<br /> Se seu aplicativo de banco de dados detectar problemas de bloqueio entre operações de leitura e gravação, o OLTP na memória removerá esses problemas, pois ele usa um novo formulário de controle de simultaneidade otimista para implementar todos os níveis de isolamento de transação. O OLTP na memória não usa TempDB para armazenar versões de linha.<br /><br /> Se o problema de colocação em escala for causado por um conflito entre duas operações de gravação, como duas transações simultâneas tentando atualizar a mesma linha, o OLTP na memória permitirá que uma transação tenha êxito e que a outra falhe. A transação com falha deve ser reenviada explícita ou implicitamente, repetindo a transação. Em ambos os casos, você precisa fazer alterações no aplicativo.<br /><br /> Se seu aplicativo apresentar conflitos frequentes entre duas operações de gravação, o valor do bloqueio otimista será diminuído. O aplicativo não é apropriado para o OLTP na memória. A maioria dos aplicativos OLTP não apresenta conflitos de gravação, a menos que o conflito seja induzido pelo escalonamento de bloqueios.|  
  
## <a name="see-also"></a>Consulte também  
 [OLTP in-memory &#40;Otimização na memória&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
