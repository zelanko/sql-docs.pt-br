---
title: Introdução às tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 12/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ef1cc7de-63be-4fa3-a622-6d93b440e3ac
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e9f652b23295e47842981035348771125b627bd7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="introduction-to-memory-optimized-tables"></a>Introdução às tabelas com otimização de memória
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Tabelas com otimização de memória são criadas com [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 Por padrão, as tabelas com otimização de memória são completamente duráveis e, assim como as transações em tabelas com base em disco tradicionais, elas são completamente ACID (atômico, consistente, isolado e durável). As tabelas com otimização de memória e procedimentos armazenados compilados nativamente oferecem suporte apenas a um subconjunto de recursos do [!INCLUDE[tsql](../../includes/tsql-md.md)].
 
Começando com o SQL Server 2016 e no banco de dados SQL do Azure, não há nenhuma limitação para [agrupamentos ou páginas de código](../../relational-databases/collations/collation-and-unicode-support.md) que são específicos para OLTP na memória.
  
 O repositório primário para tabelas com otimização de memória é a memória principal. As linhas da tabela são lidas e gravadas na memória. Uma segunda cópia dos dados da tabela é mantida em disco, mas apenas para fins de durabilidade. Veja [Criando e gerenciando armazenamento para objetos com otimização de memória](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md) para obter mais informações sobre as tabelas duráveis. Os dados das tabelas com otimização de memória são lidos apenas no disco durante a recuperação do banco de dados (por exemplo, após a reinicialização de um servidor).  
  
 Para obter ganhos de desempenho ainda maiores, o OLTP na Memória oferece suporte a tabelas duráveis com a durabilidade da transação atrasada. As transações duráveis atrasadas são salvas em disco logo após a confirmação da transação e o retorno do controle ao cliente. Em compensação ao desempenho aprimorado, as transações confirmadas que não foram salvas em disco serão perdidas em caso de falha ou failover do servidor.  
  
 Além das tabelas padrão com otimização de memória duráveis, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também oferece suporte a tabelas com otimização de memória não duráveis, que não são registradas e seus dados não são persistidos no disco. Isso significa que as transações nessas tabelas não requerem nenhuma E/S de disco, mas os dados não serão recuperados se houver falha ou failover do servidor.  
  
 O OLTP na memória é integrado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fornecer uma experiência perfeita em todas as áreas, como desenvolvimento, implantação, capacidade de gerenciamento e suporte. Um banco de dados pode conter objetos residentes na memória e baseados em disco.  
  
 As linhas nas tabelas com otimização de memória têm controle de versão. Isso significa que cada linha da tabela, possivelmente, tem várias versões. Todas as versões de linha são mantidas na mesma estrutura de dados da tabela. O controle de versão de linha é usado para permitir leituras e gravações simultâneas na mesma linha. Para obter mais informações sobre leituras e gravações simultâneas na mesma linha, veja [Transações com tabelas com otimização de memória](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md).  
  
 A figura a seguir ilustra o controle de várias versões. A figura mostra uma tabela com três linhas, e cada linha tem versões diferentes.  
  
![Controle de várias versões.](../../relational-databases/in-memory-oltp/media/hekaton-tables-1.gif "Controle de várias versões.")  
  
 A tabela tem três linhas: r1, r2 e r3. r1 tem três versões, r2 tem duas versões e r3 tem quatro versões. Observe que as versões diferentes da mesma linha não ocupam necessariamente locais de memória consecutivos. As versões de linha diferentes podem ser dispersas em toda a estrutura de dados da tabela.  
  
 A estrutura de dados da tabela com otimização de memória pode ser considerada uma coleção de versões de linha. As linhas nas tabelas baseadas em disco são organizadas em páginas e extensões, e as linhas individuais são resolvidas através do número e do deslocamento da página, as versões de linha nas tabelas com otimização de memória são resolvidas através dos ponteiros de memória de 8 bytes.  
  
 Os dados nas tabelas com otimização de memória são acessados de duas maneiras:  
  
-   Por meio de procedimentos armazenados compilados nativamente.  
  
-   Com [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretado, fora de um procedimento armazenado compilado nativamente. Essas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] podem ser procedimentos armazenados interpretados internos ou instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc.  
  
## <a name="accessing-data-in-memory-optimized-tables"></a>Acessando dados nas tabelas com otimização de memória  

As tabelas com otimização de memória podem ser acessadas com mais eficiência por meio de procedimentos armazenados compilados de modo nativo ([Procedimentos armazenados compilados de modo nativo](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)). As tabelas com otimização de memória também podem ser acessadas com [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretado (tradicional). O termo [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado refere-se ao acesso a tabelas com otimização de memória sem um procedimento armazenado compilado nativamente. Alguns exemplos de acesso ao [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado incluem o acesso a uma tabela com otimização de memória de um gatilho DML ou de um lote [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc, exibição e função com valor de tabela.  
  
 A tabela a seguir resume o acesso ao [!INCLUDE[tsql](../../includes/tsql-md.md)] nativo e interpretado de vários objetos.  
  
|Recurso|Acesso através de um procedimento armazenado compilado nativamente|Acesso [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado|Acesso à CLR|  
|-------------|-------------------------------------------------------|-------------------------------------------|----------------|  
|Tabela com otimização de memória|Sim|Sim|Não*|  
|Tipo de tabela com otimização de memória|Sim|Sim|não|  
|Procedimento armazenado compilado nativamente|Agora há suporte para o aninhamento de procedimentos armazenados nativamente compilados. Você pode usar a sintaxe EXECUTE dentro dos procedimentos armazenados, desde que o procedimento referenciado também seja nativamente compilado.|Sim|Não*|  
  
 *Não é possível acessar uma tabela com otimização de memória ou um procedimento armazenado compilado de modo nativo por meio da conexão de contexto (a conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao executar um módulo CLR). No entanto, é possível criar e abrir outra conexão, da qual você pode acessar tabelas com otimização de memória e procedimentos armazenados compilados nativamente.  
  
## <a name="performance-and-scalability"></a>Desempenho e escalabilidade  

Os seguintes fatores afetarão os ganhos de desempenho que podem ser obtidos com o OLTP na memória:  
  
*Comunicação:* um aplicativo com muitas chamadas para procedimentos armazenados curtos pode ver um ganho de desempenho menor em comparação com um aplicativo com menos chamadas e mais funcionalidade implementada em cada procedimento armazenado.  
  
*[!INCLUDE[tsql](../../includes/tsql-md.md)] :* o OLTP in-memory atinge o melhor desempenho usando procedimentos armazenados compilados de modo nativo do que usando procedimentos armazenados interpretados ou execução de consulta. Pode ser vantajoso acessar tabelas com otimização de memória de tais procedimentos armazenados.  
  
*Varredura de intervalo vs pesquisa de ponto:* os índices não clusterizados com otimização de memória dão suporte a exames de intervalo e exames ordenados. Para pesquisas de ponto, os índices de hash com otimização de memória têm desempenho melhor que os índices não clusterizados com otimização de memória. Os índices não clusterizados com otimização de memória têm desempenho melhor que os índices baseados em disco.

- A partir do SQL Server 2016, o plano de consulta de uma tabela com otimização de memória pode examinar a tabela em paralelo. Isso melhora o desempenho de consultas analíticas.
  - Índices de hash também se tornaram verificáveis em paralelo no SQL Server 2016.
  - Índices não clusterizados também se tornaram verificáveis em paralelo no SQL Server 2016.
  - Índices columnstore são verificáveis em paralelo desde sua criação no SQL Server 2014.
  
*Operações de índice:* as operações de índice não são registradas e existem apenas na memória.  
  
*Simultaneidade:* os aplicativos cujo desempenho é afetado pela simultaneidade no nível de mecanismo, como contenção de trava ou bloqueio, melhoram significativamente quando o aplicativo é movido para o OLTP in-memory.  
  
A tabela a seguir lista os problemas de desempenho e escalabilidade que geralmente são encontrados em bancos de dados relacionais e como o OLTP na memória pode melhorar o desempenho.  
  
|Problema|Impacto do OLTP na memória|  
|-----------|----------------------------|  
|Desempenho<br /><br /> Alto uso de recursos (CPU, E/S, rede ou memória).|CPU<br /> Os procedimentos armazenados compilados nativamente podem reduzir significativamente o uso da CPU, pois exigem muito menos instruções para executar uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] comparada com os procedimentos armazenados interpretados.<br /><br /> O OLTP na memória pode ajudar a reduzir o investimento de hardware em cargas de trabalho expandidas, pois um servidor pode potencialmente fornecer a taxa de transferência de cinco a dez servidores.<br /><br /> E/S<br /> Se você encontrar um gargalo de E/S, do processamento às páginas de dados ou índice, o OLTP na memória poderá reduzir esse gargalo. Além disso, o ponto de verificação de objetos OLTP na memória é contínuo e não resulta em aumentos repentinos nas operações de E/S. No entanto, se o conjunto de trabalho das tabelas críticas de desempenho não se ajustar na memória, o OLTP na memória não melhorará o desempenho, pois ele exige que os dados sejam residentes na memória. Se você encontrar um gargalo de E/S no log, o OLTP na memória poderá reduzi-lo, pois ele gera menos registros. Se uma ou mais tabelas com otimização de memória forem configuradas como tabelas não duráveis, você poderá eliminar o registro de dados.<br /><br /> Memória<br /> O OLTP na memória não oferece nenhum benefício de desempenho. Além disso, o OLTP na memória pode fazer mais pressão na memória, pois os objetos precisam ser residentes na memória.<br /><br /> Rede<br /> O OLTP na memória não oferece nenhum benefício de desempenho. Os dados precisam ser comunicados da camada de dados à camada de aplicativos.|  
|Escalabilidade<br /><br /> A maioria dos problemas de colocação em escala nos aplicativos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é causada por problemas de simultaneidade, como contenção em bloqueios, travas e spinlocks.|Contenção de trava<br /> Um cenário típico é a contenção na última página de um índice na inserção de linhas simultaneamente na ordem de chave. Como o OLTP na memória não usa travas ao acessar dados, os problemas de escalabilidade relacionados a contenções de trava são totalmente removidos.<br /><br /> Contenção de spinlock<br /> Como o OLTP na memória não usa travas ao acessar dados, os problemas de escalabilidade relacionados a contenções de spinlock são totalmente removidos.<br /><br /> Contenção relacionada ao bloqueio<br /> Se seu aplicativo de banco de dados detectar problemas de bloqueio entre operações de leitura e gravação, o OLTP na memória removerá esses problemas, pois ele usa um novo formulário de controle de simultaneidade otimista para implementar todos os níveis de isolamento de transação. O OLTP na memória não usa TempDB para armazenar versões de linha.<br /><br /> Se o problema de colocação em escala for causado por um conflito entre duas operações de gravação, como duas transações simultâneas tentando atualizar a mesma linha, o OLTP na memória permitirá que uma transação tenha êxito e que a outra falhe. A transação com falha deve ser reenviada explícita ou implicitamente, repetindo a transação. Em ambos os casos, você precisa fazer alterações no aplicativo.<br /><br /> Se seu aplicativo apresentar conflitos frequentes entre duas operações de gravação, o valor do bloqueio otimista será diminuído. O aplicativo não é apropriado para o OLTP na memória. A maioria dos aplicativos OLTP não apresentam conflitos de gravação, a menos que o conflito seja induzido pelo escalonamento de bloqueios.|  
  
##  <a name="rls"></a> Segurança em nível de linha em tabelas com otimização de memória  

Há suporte para a[segurança em nível de linha](../../relational-databases/security/row-level-security.md) em tabelas com otimização de memória. Aplicar políticas de segurança de nível de linha a tabelas com otimização de memória é essencialmente o mesmo que fazê-lo a tabelas baseadas em disco, exceto que as funções embutidas com valor de tabela usadas como predicados de segurança devem ser compiladas nativamente (criadas usando a opção WITH NATIVE_COMPILATION). Para obter detalhes, confira a seção [Compatibilidade entre recursos](../../relational-databases/security/row-level-security.md#Limitations) do tópico [Segurança em nível de linha](../../relational-databases/security/row-level-security.md) .  
  
 Várias funções de segurança internas que são essenciais para a segurança em nível de linha foram habilitadas para tabelas in-memory. Para obter detalhes, veja [Funções internas em módulos de compilados de modo nativo](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#bfncsp).  
  
 **EXECUTE AS CALLER** – Todos os módulos nativos agora dão suporte e usam EXECUTE AS CALLER por padrão, mesmo se a dica não for especificada. Isso ocorre porque espera-se que todas as funções de predicado de segurança de nível de linha usem EXECUTE AS CALLER, de modo que a função (e quaisquer funções internas usadas nela) serão avaliadas no contexto do usuário efetuando a chamada.   
EXECUTE AS CALLER tem um impacto pequeno (aproximadamente 10%) sobre o desempenho causado pelas verificações de permissão no chamador. Se o módulo especificar EXECUTE AS OWNER ou EXECUTE AS SELF explicitamente, essas verificações de permissão e o custo de desempenho associado serão evitados. No entanto, usar qualquer uma dessas opções em conjunto com as funções internas acima incorrerá em um impacto significativamente maior sobre o desempenho devido à alternância de contexto necessária.  
  
## <a name="scenarios"></a>Cenários

Para ver uma breve discussão de cenários típicos em que o [!INCLUDE[hek_1](../../includes/hek-1-md.md)] pode melhorar o desempenho, veja [OLTP in-memory](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte Também

[OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
