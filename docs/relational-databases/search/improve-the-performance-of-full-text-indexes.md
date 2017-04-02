---
title: "Melhorar o desempenho de &#237;ndices de texto completo | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "desempenho [SQL Server], pesquisa de texto completo"
  - "consultas de texto completo [SQL Server], desempenho"
  - "rastreamentos [pesquisa de texto completo]"
  - "índices de texto completo [SQL Server], desempenho"
  - "pesquisa de texto completo [SQL Server], desempenho"
  - "lotes [SQL Server], pesquisa de texto completo"
ms.assetid: ef39ef1f-f0b7-4582-8e9c-31d4bd0ad35d
caps.latest.revision: 68
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 67
---
# Melhorar o desempenho de &#237;ndices de texto completo
  O desempenho da indexação de texto completo e das consultas de texto completo é influenciado por recursos de hardware, como memória, velocidade de disco, velocidade da CPU, e pela arquitetura do computador.  
  
##  <a name="causes"></a> Causas comuns de problemas de desempenho  
 A principal causa da diminuição do desempenho da indexação de texto completo são os limites em termos de recursos de hardware:  
  
-   Se o uso da CPU pelo processo de host do daemon de filtro (fdhost.exe) ou o processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (sqlservr.exe) está próximo de 100%, a CPU é o afunilamento.  
  
-   Se a média de tamanho da lista de pendências de disco é duas vezes maior do que o número de cabeçotes de disco, há um gargalo no disco. A principal solução alternativa é criar catálogos de texto completo separados dos arquivos e logs de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Coloque os logs, arquivos de banco de dados e catálogos de texto completo em discos separados. Comprar discos mais rápidos e usar RAID também pode ajudar a melhorar desempenho de indexação.  
  
-   Se houver uma escassez de memória física, a memória poderá ser o gargalo.  
  
    > [!NOTE]  
    >  A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], o Mecanismo de Texto Completo pode usar memória AWE, pois o mecanismo faz parte de sqlservr.exe.  
  
 Se o sistema não tiver gargalos de hardware, o desempenho de indexação da pesquisa de texto completo dependerá principalmente do seguinte:  
  
-   O tempo necessário para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criar lotes de texto completo.  
  
-   A rapidez com que o daemon de filtro pode consumir esses lotes.  
  
> [!NOTE]  
>  Ao contrário da população completa, a população de controle de alterações incremental, manual e automática não foi desenvolvida para maximizar os recursos de hardware a fim de obter maior velocidade. Portanto, essas sugestões de ajuste podem não melhorar o desempenho da indexação de texto completo.  
  
 Quando a população for concluída, um processo de mesclagem final será disparado, mesclando os fragmentos de índice em um índice de texto completo mestre. Isso resulta em desempenho aprimorado de consultas, uma vez que apenas o índice precisa ser consultado, em vez de uma série de fragmentos de índice, e melhores estatísticas de pontuação podem ser usadas para classificação de relevância. Observe que a mesclagem mestra pode ser de E/S intensiva, porque grandes quantidades de dados precisam ser gravados e lidos quando os fragmentos de índice são mesclados, embora isso não bloqueie as consultas de entrada.  
  
> [!IMPORTANT]  
>  A mesclagem mestra de grande quantidade de dados pode criar uma transação demorada, atrasando o truncamento do log de transações durante o ponto de verificação. Nesse caso, no modelo de recuperação completa, o log de transações pode crescer significativamente. Como prática recomendada, antes de reorganizar um índice de texto completo grande em um banco de dados que usa o modelo de recuperação completa, verifique se o log de transações contém espaço suficiente para uma transação demorada. Para obter mais informações, veja [Gerenciar o tamanho do arquivo de log de transações](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md).  
  
##  <a name="tuning"></a> Ajustando o desempenho de índices de texto completo  
 Para maximizar o desempenho de seus índices de texto completo, implemente as seguintes práticas recomendadas:  
  
-   Para utilizar ao máximo todos os processadores ou núcleos, defina [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)‘**max full-text crawl ranges**’ como o número de CPUs do sistema. Para obter informações sobre essa opção de configuração, veja [Opção max full-text crawl range de configuração de servidor](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md).  
  
-   Verifique se a tabela base tem um índice clusterizado. Use um tipo de dados integer para a primeira coluna do índice clusterizado. Evite usar GUIDs na primeira coluna do índice clusterizado. Uma população de vários intervalos em um índice clusterizado pode gerar a maior velocidade de população. É recomendável que a coluna que funciona como chave de texto completo tenha um tipo de dados integer.  
  
-   Atualize as estatísticas da tabela base usando a instrução [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md) . E, o mais importante, atualize as estatísticas no índice clusterizado ou na chave de texto completo para uma população completa. Isso ajuda uma população de vários intervalos a gerar boas partições na tabela.  
  
-   Crie um índice secundário em uma coluna **timestamp** para melhorar o desempenho da população incremental.  
  
-   Antes de executar uma população completa em um computador com várias CPUs, é recomendável limitar o tamanho do pool de buffers temporariamente, definindo o valor **max server memory** para deixar memória suficiente para o processo do fdhost.exe e para uso do sistema operacional. Para obter mais informações, consulte "Estimando os requisitos de memória da memória compartilhada de saída do processo do host do daemon de filtro (fdhost.exe)", posteriormente neste tópico.  
  
##  <a name="full"></a> Solucionando problemas do desempenho de populações completas  
 Para diagnosticar problemas de desempenho, examine os logs de rastreamento de texto completo. Para obter informações sobre logs de rastreamento, veja [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
 É recomendável seguir a ordem de solução de problemas especificada abaixo se o desempenho das populações completas não for satisfatório.  
  
### Uso de memória física  
 Durante uma população de texto completo, é possível que o fdhost.exe ou o sqlservr.exe fique com pouca memória não tenha memória suficiente. Se o log de rastreamento de texto completo mostrar que fdhost.exe está sendo reiniciado com frequência ou que o código de erro 8007008 está sendo retornado, isso indica que um desses processos está sendo executado sem memória. Se fdhost.exe estiver gerando despejos, principalmente em computadores grandes com várias CPUs, talvez ele esteja ficando com memória insuficiente.  
  
> [!NOTE]  
>  Para obter informações sobre os buffers de memória usados por um rastreamento de texto completo, veja [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md).  
  
 As causas possíveis são as seguintes:  
  
-   Se a quantidade de memória física disponível durante uma população completa for zero, o pool de buffers do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] talvez esteja consumindo a maior parte da memória física do sistema.  
  
     O processo do sqlservr.exe tenta obter toda a memória disponível para o pool de buffers, até a memória máxima configurada para o servidor. Se a alocação de **max server memory** for muito grande, condições de memória insuficiente e falha para alocar memória compartilhada poderão ocorrer para o processo do fdhost.exe.  
  
    > [!NOTE]  
    >  Durante uma população de texto completo em um computador com várias CPUs, pode ocorrer a contenção da memória do pool de buffers entre fdhost.exe ou sqlservr.exe. A memória compartilhada insuficiente resultante provoca tentativas em lote, sobrecarga de memória e despejos do processo do fdhost.exe.  
  
     Para resolver esse problema, defina o valor de **memória máxima do servidor** do pool de buffers do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] adequadamente. Para obter mais informações, consulte "Estimando os requisitos de memória da memória compartilhada de saída do processo do host do daemon de filtro (fdhost.exe)", posteriormente neste tópico. A redução do tamanho do lote usado para indexação de texto completo pode ajudar.  
  
-   Um problema de paginação  
  
     O tamanho insuficiente do arquivo de paginação, como em um sistema que tem um arquivo de paginação pequeno com crescimento restrito, também pode fazer com que o fdhost.exe ou o sqlservr.exe fique com memória insuficiente.  
  
     Se os logs de rastreamento não indicarem nenhuma falha relacionada à memória, é provável que o desempenho esteja lento devido a excesso de paginação.  
  
### Estimando os requisitos de memória da memória compartilhada de saída do processo do host do daemon de filtro (fdhost.exe)  
 A quantidade de memória necessária para o processo do fdhost.exe para uma população depende principalmente do número de intervalos de rastreamento de texto completo que ele usa, do tamanho da ISM (memória compartilhada de entrada) e do número de máximo de instâncias da ISM.  
  
 A quantidade de memória consumida (em bytes) pelo host do daemon de filtro pode ser estimada aproximadamente usando a fórmula a seguir:  
  
 *number_of_crawl_ranges* \**ism_size***max_outstanding_isms*\* 2  
  
 Os valores padrão das variáveis na fórmula anterior são os seguintes:  
  
|**Variável**|**Valor padrão**|  
|------------------|-----------------------|  
|*number_of_crawl_ranges*|O número de CPUs|  
|*ism_size*|1 MB para computadores x86<br /><br /> 4 MB, 8 MB ou 16MB para computadores x64, dependendo da memória física total|  
|*max_outstanding_isms*|25 MB para computadores x86<br /><br /> 5 MB para computadores x64|  
  
 A tabela a seguir apresenta diretrizes sobre como estimar as necessidades de memória do fdhost.exe. As fórmulas desta tabela usam os seguintes valores:  
  
-   *F*, que é uma estimativa da memória necessária para fdhost.exe (em MB).  
  
-   *T*, que é o total de memória física disponível no sistema (em MB).  
  
-   *M*, que é a configuração de **memória máxima do servidor** ideal.  
  
> [!IMPORTANT]  
>  Para obter informações essenciais sobre as fórmulas, veja (1), (2) e (3), abaixo.  
  
|Plataforma|Estimando as necessidades de memória de fdhost.exe em MB —*F*^1|Fórmula para calcular a memória máxima do servidor —*M*^2|  
|--------------|-----------------------------------------------------------|-----------------------------------------------------|  
|x86|*F* **=** *Número de intervalos de rastreamento* **\*** 50|*M* **=minimum(** *T* **,** 2000**)–***F***–** 500|  
|x64|*F* **=** *Número de intervalos de rastreamento* **\*** 10 **\*** 8|*M* **=** *T* **–** *F* **–** 500|  
  
 (1) Se houver várias populações completas em andamento, calcule os requisitos de memória de fdhost.exe de cada uma separadamente, como *F1*, *F2* e assim por diante. Em seguida, calcule *M* como *T***–** sigma**(***F***)**.  
  
 (2) 500 MB é uma estimativa da memória exigida por outros processos no sistema. Se o sistema estiver executando trabalho adicional, aumente esse valor de maneira correspondente.  
  
 (3) .*ism_size* é presumido como 8 MB para plataformas x64.  
  
 **Exemplo: Estimando as necessidades de memória do fdhost.exe**  
  
 Este exemplo é para um computador AMD64 com 8 GB de RAM e 4 processadores de núcleo dual. O primeiro cálculo estima a memória necessária para fdhost.exe —*F*. O número de intervalos de rastreamento é `8`.  
  
 `F = 8*10*8=640`  
  
 O próximo cálculo obtém o valor ideal para **memória máxima do servidor**—*M*. *O* total de memória física disponível no sistema em MB – *T* – é `8192`.  
  
 `M = 8192-640-500=7052`  
  
 **Exemplo: Definindo a configuração max server memory**  
  
 Este exemplo usa as instruções [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) e [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] para definir **max server memory** com o valor calculado para *M* no exemplo anterior, `7052`:  
  
```  
USE master;  
GO  
EXEC sp_configure 'max server memory', 7052;  
GO  
RECONFIGURE;  
GO  
```  
  
 **Para definir a opção de configuração da memória máxima do servidor**  
  
-   [Opções Server Memory de configuração do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
### Fatores que podem reduzir o consumo da CPU  
 Esperamos que o desempenho das populações completas não seja o ideal quando a média de consumo da CPU for inferior a cerca de 30%. Esta seção discute alguns fatores que afetam o consumo da CPU.  
  
-   Alta espera por páginas  
  
     Para saber se o tempo de espera de uma página é alto, execute a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```  
    Execute SELECT TOP 10 * FROM sys.dm_os_wait_stats ORDER BY wait_time_ms DESC;  
    ```  
  
     A tabela a seguir descreve os tipos de espera de interesse aqui mencionados.  
  
    |Tipo de espera|Descrição|Solução possível|  
    |---------------|-----------------|-------------------------|  
    |PAGEIO_LATCH_SH (_EX ou _UP)|Isso pode indicar um gargalo de E/S, caso em que normalmente você também observa um comprimento médio da fila de disco alto.|Mover o índice de texto completo para outro grupo de arquivos em outro disco pode ajudar a reduzir o gargalo de E/S.|  
    |PAGELATCH_EX (ou _UP)|Isso pode indicar muita contenção entre os threads que estão tentando para gravar no mesmo arquivo de banco de dados.|Adicionar arquivos ao grupo de arquivos em que reside o índice de texto completo pode ajudar a aliviar essa contenção.|  
  
     Para obter mais informações, veja [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).  
  
-   Ineficiências ao examinar a tabela base  
  
     Uma população completa examina a tabela base para gerar lotes. Esse exame da tabela pode ser ineficiente nos seguintes cenários:  
  
    -   Se a tabela base tem uma porcentagem alta de colunas fora de linha que estão sendo indexadas com texto completo, examinar a tabela base para gerar lotes pode ser o gargalo. Nesse caso, mover os dados menores em linha usando **varchar(max)** ou **nvarchar(max)** pode ser útil.  
  
    -   Se a tabela base estiver muito fragmentada, o exame poderá ser ineficiente. Para obter informações sobre como calcular dados fora de linha e fragmentação de índice, veja [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md) e [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md).  
  
         Para reduzir a fragmentação, você pode reorganizar ou recriar o índice clusterizado. Para obter mais informações, veja [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
##  <a name="filters"></a> Solucionando problemas de desempenho de indexação lento devido a filtros  
 Ao popular um índice de texto completo, o Mecanismo de Texto Completo usa dois tipos de filtros: multithread (vários threads) e single-thread (thread único). Alguns documentos, como os documento do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word, são filtrados com um filtro multithread. Outros documentos, como documentos em PDF (Adobe Acrobat Portable Document Format), são filtrados com um filtro de thread único.  
  
 Por razões de segurança, os filtros são carregados por processos de host do daemon de filtro. Uma instância de servidor usa um processo multi-threaded para todos os filtros multi-threaded e um processo single-threaded para todos os filtros single-threaded. Quando um documento que usa um filtro multithread contém um documento incorporado que usa um filtro de thread único, o Mecanismo de Texto Completo inicia um processo de thread único para o documento incorporado. Por exemplo, ao encontrar um documento do Word que contém um documento em PDF, o Mecanismo de Texto Completo usa o processo multithread para o conteúdo do Word e inicia um processo de thread único para o conteúdo do PDF. Um filtro de thread único pode não funcionar bem neste ambiente e pode desestabilizar o processo de filtragem. Em determinadas circunstâncias em que o processo de incorporação é comum, a desestabilização pode causar o travamento do processo de filtragem. Quando isso ocorrer, o Mecanismo de Texto Completo refaz a rota do documento que falhou (por exemplo, um documento do Word que contém um conteúdo em PDF incorporado) para o processo de filtragem em thread único. Se isso acontecer com frequência, ocorrerá uma degradação de desempenho do processo de indexação de texto completo.  
  
 Para solucionar esse problema, marque o filtro para o documento que contém o conteúdo (neste caso, o Word) como filtro de thread único. É possível alterar o valor do registro de filtro para marcar um determinado filtro como filtro de thread único. Para marcar um filtro como filtro de thread único, você precisará definir o valor de registro **ThreadingModel** para o filtro como **Apartment Threaded**. Para obter informações sobre Single-Threaded Apartments, veja o white paper [Understanding and Using COM Threading Models](http://go.microsoft.com/fwlink/?LinkId=209159) (Compreendendo e usando os modelos de threading COM).  
  
## Consulte também  
 [Opções Server Memory de configuração do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [Opção de configuração de servidor max full-text crawl range](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md)   
 [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md)   
 [Criar e gerenciar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)   
 [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)   
 [Solucionar problemas na indexação de texto completo](../../relational-databases/search/troubleshoot-full-text-indexing.md)  
  
  