---
title: Contadores de desempenho (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 05d7d5ab-a96c-4f82-94b1-48a657d7c580
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aa9d5a5352afd10617358a032824d275b14b6c5e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66079707"
---
# <a name="performance-counters-ssas"></a>Contadores de desempenho (SSAS)
  Usando o Monitor de Desempenho, você pode monitorar o desempenho de uma instância do Microsoft SQL Server Analysis Services (SSAS) usando contadores de desempenho.  
  
 O Monitor de Desempenho é um snap-in do Controle de Gerenciamento [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MMC) que controla o uso de recursos. Você pode iniciar este snap-in de MMC digitando **PerfMon** no prompt de comando ou, no Painel de Controle, clicando em **Ferramentas Administrativas**e, em seguida, **Monitor de Desempenho**. O Monitor de Desempenho permite o monitoramento de atividade e desempenho do servidor e dos processos usando objetos e contadores predefinidos, bem como o monitoramento de eventos usando contadores definidos pelo usuário. O Monitor de Desempenho coleta as contagens em vez de dados sobre os eventos, por exemplo, uso de memória, número de transações ativas ou atividade de CPU. Você também pode definir limites em contadores específicos para gerar alertas que notificam operadores.  
  
 O Monitor de Desempenho pode monitorar instâncias remotas e locais do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Usando o Monitor de Desempenho](https://technet.microsoft.com/library/cc749115.aspx).  
  
 Para ver a descrição de qualquer contador que pode ser usado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], em Monitor de Desempenho, abra a caixa de diálogo **Adicionar Contadores** , selecione um objeto de desempenho e clique em **Mostrar Descrição**. Os contadores mais importantes são: uso de CPU, uso de memória e taxa de E/S do disco. É recomendável iniciar com esses importantes contadores e passar para contadores mais detalhados quando você tiver uma ideia melhor do que mais pode ser aprimorado pelo monitoramento. Para obter mais informações sobre quais contadores devem ser incluídos, consulte o [Guia de Operações do SQL Server 2008 R2](https://go.microsoft.com/fwlink/?LinkID=225539).  
  
 Os contadores são agrupados para facilitar a localização dos contadores relacionados.  
  
## <a name="counters-by-groups"></a>Contadores por grupos  
  
|Agrupar|Descrição|  
|-----------|-----------------|  
|[Cache](#bkmk_Cache)|Estatísticas relacionadas ao cache de agregação do Analysis Services.|  
|[Conexão](#bkmk_Connection)|Estatísticas relacionadas às conexões do Microsoft Analysis Services|  
|[Previsão de Mineração de Dados](#bkmk_DataMiningPrediction)|Estatísticas relacionadas ao processamento de modelos de mineração de dados.|  
|[Processamento do Modelo de Mineração de Dados](#bkmk_DataMiningModelProcessing)|Estatísticas relacionadas à criação de previsões de modelos de mineração de dados.|  
|[Locks](#bkmk_Locks)|Estatísticas relativas a bloqueios do servidor interno do Microsoft Analysis Services.|  
|[MDX](#bkmk_MDX)|Estatísticas relacionadas a cálculos MDX do Microsoft Analysis Services.|  
|[Memória](#bkmk_Memory)|Estatísticas relacionadas à memória do servidor interno do Microsoft Analysis Services.|  
|[Cache pró-ativo](#bkmk_ProactiveCaching)|Estatísticas relacionadas ao cache pró-ativo do Microsoft Analysis Services.|  
|[Processamento de agregações](#bkmk_ProcAggregations)|Estatísticas relacionadas ao processamento de agregações em arquivos de dados MOLAP.|  
|[Processamento de índices](#bkmk_ProcIndexes)|Estatísticas relacionadas ao processamento de índices para arquivos de dados MOLAP.|  
|[Processando](#bkmk_Processing)|Estatísticas relacionadas ao processamento de dados.|  
|[Consulta do mecanismo de armazenamento](#bkmk_StorageEngineQuery)|Estatísticas relacionadas a consultas do mecanismo de armazenamento do Microsoft Analysis Services.|  
|[Threads](#bkmk_Threads)|Estatísticas relacionadas a threads do Microsoft Analysis Services.|  
  
###  <a name="cache"></a><a name="bkmk_Cache"></a>Armazenar  
 Estatísticas relacionadas ao cache de agregação do Analysis Services.  
  
|Contador|Descrição|  
|-------------|-----------------|  
|KB Atual|Memória atual usada pelo cache de agregação, em KB.|  
|KB adicionado/s|Taxa de memória acrescentada ao cache, KB/segundo.|  
|Entradas atuais|Número atual de entradas de cache.|  
|Inserções/s|Taxa de inserções no cache.  A taxa é rastreada por partição por cubo por banco de dados.|  
|Remoções/s|Taxa de remoções do cache  Isto ocorre por partição por cubo por banco de dados  As remoções costumam ocorrer devido à limpeza do plano de fundo.|  
|Total de inserções|Inserções no cache.  A taxa é rastreada por partição por cubo por banco de dados.|  
|Total de remoções|Remoções do cache.  As remoções são rastreadas por partição por cubo por banco de dados.  As remoções costumam ocorrer devido à limpeza do plano de fundo.|  
|Acertos diretos/s|Taxa de acertos diretos do cache. Um acerto de cache indica que consultas foram respondidas de uma entrada de cache existente.|  
|Erros/s|Taxa de erros do cache.|  
|Pesquisas/s|Taxa de pesquisas de cache.|  
|Total de acertos diretos|Contagem total de acertos diretos de cache.  Um acerto direto de cache indica que consultas foram respondidas a partir de entradas de cache existentes.|  
|Total de erros|Contagem total de erros de cache.|  
|Total de pesquisas|Número total de pesquisas no cache.|  
|Taxa de acertos diretos|Taxa de acertos diretos do cache para pesquisas de cache, pelo período entre valores de contador.|  
|Total de acertos do cache do iterator filtrado|Número total de acertos do cache que retornaram um iterador indexado nos resultados filtrados.|  
|Número total de erros de cache do iterador filtrado|Número total de acertos de cache que não conseguiram criar um iterador indexado nos resultados filtrados e precisaram criar um novo cache com os resultados filtrados.|  
  
###  <a name="connection"></a><a name="bkmk_Connection"></a>Conexão  
 Estatísticas relacionadas às conexões do Microsoft Analysis Services  
  
|Contador|Descrição|  
|-------------|-----------------|  
|Conexões atuais|Número atual de conexões de cliente estabelecidas.|  
|Solicitações/s|Taxa de solicitações de conexão.  Estas são chegadas.|  
|Total de solicitações|Solicitações de conexão totais.  Estas são chegadas.|  
|Êxitos/s|Taxa de conclusões de conexão bem-sucedidas.|  
|Total de êxitos|Total de conexões com êxito.|  
|Falhas/s|Taxa de falhas de conexão.|  
|Total de falhas|Total de falhas em tentativas de conexão.|  
|Sessões atuais do usuário|Número atual de sessões de usuário estabelecidas.|  
  
###  <a name="data-mining-model-processing"></a><a name="bkmk_DataMiningModelProcessing"></a>Processamento de modelo de mineração de dados  
 Estatísticas relativas ao processamento do modelo de Mineração de Dados do Microsoft Analysis Services.  
  
|Contador|Descrição|  
|-------------|-----------------|  
|Casos/s|Taxa de processamento dos casos.|  
|Processamento atual de modelos|Número atual de modelos sendo processados.|  
  
###  <a name="data-mining-prediction"></a><a name="bkmk_DataMiningPrediction"></a>Previsão de mineração de dados  
 Estatística relativa à previsão de Mineração de Dados do Microsoft Analysis Services.  
  
|Contador|Descrição|  
|-------------|-----------------|  
|Consultas simultâneas do DM|Número atual de consultas de mineração de dados sendo trabalhadas ativamente.|  
|Previsões/s|Número de previsões geradas em consultas de mineração de dados|  
|Linhas/s|Número de linhas tratadas durante uma consulta de previsão de mineração de dados.|  
|Consultas/s|Número de consultas de mineração de dados que foram tratadas.|  
|Total de consultas|Total de consultas de mineração de dados recebidas pelo servidor.|  
|Linhas de total|Total de linhas retornadas por consultas de mineração de dados.|  
|Total de previsões|Total de consultas de previsão de mineração de dados recebidas pelo servidor.|  
  
###  <a name="locks"></a><a name="bkmk_Locks"></a>Bloquea  
 Estatísticas relativas a bloqueios do servidor interno do Microsoft Analysis Services.  
  
|Contador|Descrição|  
|-------------|-----------------|  
|Esperas de trava atuais|Número atual de threads aguardando uma trava.  Estas solicitações de trava que podem ter concessões imediatas e se encontram em estado de espera.|  
|Esperas de trava/s|Taxa de solicitações de trava que não podem ser concedidas imediatamente e precisaram aguardar antes de serem concedidas.|  
|Bloqueios atuais|Número atual de objetos bloqueados.|  
|Esperas de bloqueio atuais|Número atual de clientes aguardando um bloqueio.|  
|Solicitações de bloqueio/s|Número de solicitações de bloqueio por segundo.|  
|Concessões de bloqueio/s|Número de concessões de bloqueio por segundo.|  
|Esperas de bloqueio/s|Número de esperas de bloqueio por segundo.  Há solicitações de bloqueio que podem receber concessões de bloqueio imediato e foram colocadas em estado de espera.|  
|Negações de bloqueio/s|Taxa de negações de bloqueio.|  
|Solicitações de desbloqueio/s|Número de solicitações de desbloqueio por segundo.|  
|Total de deadlocks detectados|Número total de deadlocks detectados.|  
  
###  <a name="mdx"></a><a name="bkmk_MDX"></a>LINGUAGEM  
 Estatísticas relacionadas a cálculos MDX do Microsoft Analysis Services.  
  
|Contador|Descrição|  
|-------------|-----------------|  
|Número de coberturas de cálculo|Número total de nós de avaliação criados por planos de execução MDX, incluindo ativo e em cache.|  
|Número atual de nós de avaliação|Número atual (aproximado) de nós de avaliação criados por planos de execução MDX, incluindo ativo e em cache.|  
|Número de nós de avaliação do Mecanismo de Armazenamento|Número total de nós de avaliação do Mecanismo de Armazenamento criados por planos de execução MDX|  
|Número de nós de avaliação célula a célula|Número total de nós de avaliação célula a célula criados por planos de execução MDX|  
|Número de nós de avaliação em modo em massa|Número total de nós de avaliação em modo em massa criados por planos de execução MDX|  
|Número de nós de avaliação cobertos por uma única célula|Número total de nós de avaliação criados por planos de execução MDX que são cobertos por uma única célula.|  
|Número de nós de avaliação com cálculos na mesma granularidade|Número total de nós de avaliação criados por planos de execução MDX para os quais os cálculos estão na mesma granularidade que o nó de avaliação.|  
|Número atual de nós de avaliação armazenados em cache|Número atual (aproximado) de nós de avaliação armazenados em cache criados por planos de execução MDX.|  
|Número de nós de avaliação do Mecanismo de Armazenamento armazenados em cache|Número total de nós de avaliação do Mecanismo de Armazenamento armazenado em cache criados por planos de execução MDX|  
|Número de nós de avaliação do modo em massa armazenados em massa|Número total de nós de avaliação do modo em massa armazenados em cache criados por planos de execução MDX|  
|Número de 'outros' nós de avaliação armazenados em cache|Número total de nós de avaliação armazenados em cache criados por planos de execução MDX que não são do Mecanismo de Armazenamento nem do modo em massa.|  
|Número de remoções de nós de avaliação|Número total de remoções de cache de nós de avaliação devido a colisões.|  
|Número de acertos de índice de hash no cache de nós de avaliação|Número total de acertos no cache de nós de avaliação que foram satisfeitos pelo índice de hash.|  
|Número de acertos célula a célula no cache de nós de avaliação|Número total de acertos célula a célula no cache de nós de avaliação.|  
|Número de erros célula a célula no cache de nós de avaliação|Número total de erros célula a célula no cache de nós de avaliação.|  
|Número de acertos de subcubo no cache de nós de avaliação|Número total de acertos de subcubo no cache de nós de avaliação.|  
|Número de erros de subcubo no cache de nós de avaliação|Número total de erros de subcubo no cache de nós de avaliação.|  
|Total de subcubos Sonar|Número total de subcubos que o otimizador de consulta gerou.|  
|Total de células calculadas|Número total de propriedades de células calculadas.|  
|Total de recomputações|Número total de células recomputadas devido ao erro.|  
|Total de inserções de cache simples|Número total de valores de célula inseridos em cache de cálculo simples.|  
|Total de cache de cálculo registrado|Número total de caches de cálculo registrados.|  
|Total de NÃO VAZIOS|Número total de horas de uso de um algoritmo NÃO VAZIO.|  
|Total de NÃO VAZIOS não otimizados|Número total de vezes em que um algoritmo NÃO VAZIO foi usado.|  
|Total de NÃO VAZIO para membros calculados|Número total de vezes em que um algoritmo NÃO VAZIO executou um loop em membros calculados.|  
|Total de Autoexist|Número total de vezes em que Autoexist foi executado.|  
|Total de EXISTENTE|Número total de vezes em que uma operação definida EXISTENTE foi executada.|  
  
###  <a name="memory"></a><a name="bkmk_Memory"></a>Memória  
 Estatísticas relacionadas à memória do servidor interno do Microsoft Analysis Services.  
  
|Contador|Descrição|  
|-------------|-----------------|  
|KB Alocado do Pool da Página 64|Memória emprestada do sistema, em KB.  Esta memória é oferecida a outras partes do servidor.|  
|KB à Parte do Pool da Página 64|Memória atual em lista à parte de 64 KB, em KB.  (Páginas de memória prontas para serem usadas.)|  
|KB Alocado do Pool da Página 8|Memória emprestada do pool de página de 64KB, em KB.  Esta memória é oferecida a outras partes do servidor.|  
|KB à Parte do Pool da Página 8|Memória atual em lista à parte de 8KB, em KB.  (Páginas de memória prontas para serem usadas.)|  
|KB Alocado do Pool da Página 1|Memória emprestada do pool de página de 64KB, em KB.  Esta memória é oferecida a outras partes do servidor.|  
|KB à Parte do Pool da Página 1|Memória atual em lista à parte de 8KB, em KB.  (Páginas de memória prontas para serem usadas.)|  
|Preço atual do limpador|Preço atual da memória, $/byte/tempo, normalizado em 1000.|  
|Saldo de Limpeza/s|Taxa de operações de saldo+redução.|  
|Redução da limpeza de Memória em KB/s|Taxa de redução, em KB/s.|  
|KB de Memória Reduzível|Quantidade de memória, em KB, sujeita a eliminação pela limpeza de segundo plano.|  
|KB da Memória da Limpeza Não Reduzível|Quantidade de memória, em KB, não sujeita a eliminação pela limpeza de segundo plano.|  
|KB de Memória de Limpeza|Quantidade de memória, em KB, conhecida pela limpeza de segundo plano.  (Memória da limpeza reduzível + Memória de limpeza não reduzível.)|  
|KB de uso de memória|Uso de memória do processo do servidor, como usado no cálculo de preço de memória do limpador.  Igual ao contador Processo\PrivateBytes mais o tamanho dos dados mapeados em memória, ignorando qualquer memória mapeada ou alocada pelo mecanismo de análise de memória xVelocity (VertiPaq), além do limite de memória do mecanismo xVelocity.|  
|KB de Limite de Memória Baixo|Limite de memória inferior, do arquivo de configuração.|  
|KB de Limite de Memória Alto|Limite de memória superior, do arquivo de configuração.|  
|AggCacheKB|Memória atual alocada para cache de agregação, em KB.|  
|Cota de KB|Cota de memória atual, em KB.  A cota de memória também é conhecida como uma reserva de memória ou concessão de memória.|  
|Cota bloqueada|Número atual de solicitações de cota bloqueadas até que outras cotas de memória sejam liberadas.|  
|KB de repositório de arquivo|Memória atual alocada para repositório de arquivo (cache de arquivo), em KB.|  
|Falhas da Página de Repositório de Arquivo/s|Taxa de falhas da página de repositório de arquivo.|  
|Leituras de Repositório de Arquivo/s|Leitura de páginas de repositório de arquivo/s.|  
|Leituras de KB de Repositório de Arquivo/s|Leitura de KB de repositório de arquivo/s.|  
|Gravações de Repositório de Arquivo/s|Páginas de repositórios de arquivos gravadas/s. As gravações são assíncronas.|  
|Gravação de KB de Repositório de Arquivo/s|Repositórios de arquivos KB gravados/s. As gravações são assíncronas.|  
|Erros de ES do Repositório de Arquivo/s|Taxa de erros de ES do repositório de arquivo.|  
|Erros de ES do Repositório de Arquivo|Total de erros de ES do repositório de arquivo.|  
|Páginas de Relógio do Repositório de Arquivo Examinadas/s|Taxa de limpeza de plano de fundo que examina páginas para consideração de remoção.|  
|Páginas do Relógio do Repositório de Arquivo ComRef/s|Taxa de limpeza de plano de fundo que examina páginas com uma contagem de referência atual (estão em uso no momento).|  
|Páginas de Relógio do Repositório de Arquivo Válidas/s|Taxa de limpeza de plano de fundo que examina páginas que são candidatas válidas à remoção.|  
|Memória Fixada do Repositório de Arquivo em KB|Memória fixada do repositório de arquivo atual, em KB.|  
|Arquivo de Propriedade de Dimensão Contido na Memória em KB|O tamanho atual do arquivo de propriedade de dimensão contido na memória, em KB.|  
|Arquivo de Propriedade de Dimensão Contido na Memória em KB/s|Taxa de gravações no arquivo de propriedade de dimensão contido na memória, em KB.|  
|Arquivo de Propriedade de Dimensão Contido na Memória Potencial em KB|O tamanho potencial do arquivo de propriedade de dimensão contido na memória, em KB.|  
|Arquivos de Propriedade de Dimensão|Número de arquivos de propriedade de dimensão.|  
|Arquivo de Índice (Hash) de Dimensão Contido na Memória em KB|Tamanho do arquivo de índice (hash) de dimensão contido na memória, em KB.|  
|Arquivo de Índice (Hash) de Dimensão Contido na Memória em KB/s|Taxa de gravações no arquivo de índice (hash) de dimensão contido na memória, em KB.|  
|Arquivo de Índice (Hash) de Dimensão Contido na Memória Potencial em KB|Tamanho potencial do arquivo de índice (hash) de dimensão contido na memória, em KB.|  
|Arquivos de índice (hash) de dimensão|Número de arquivos de índice (hash) de dimensão.|  
|Arquivo da Cadeia de Caracteres de Dimensão Contido na Memória em KB|O tamanho atual do arquivo da cadeia de caracteres de dimensão contido na memória, em KB.|  
|Arquivo da Cadeia de Caracteres de Dimensão Contido na Memória em KB/s|Taxa de gravações no arquivo da cadeia de caracteres de dimensão contido na memória, em KB.|  
|Arquivo da Cadeia de Caracteres de Dimensão Contido na Memória Potencial em KB|O tamanho potencial do arquivo da cadeia de caracteres de dimensão contido na memória, em KB.|  
|Arquivos da cadeia de caracteres de dimensão|Número de arquivos da cadeia de caracteres de dimensão.|  
|Arquivo de Mapa Contido na Memória em KB|Tamanho atual do arquivo de mapa contido na memória, em KB.|  
|Arquivo de Mapa Contido na Memória em KB/s|Taxa de gravações no arquivo de mapa contido na memória, em KB.|  
|Arquivo de Mapa Contido na Memória Potencial em KB|Tamanho potencial do arquivo de mapa contido na memória, em KB.|  
|Arquivos de Mapa|Número de arquivos de mapa.|  
|Arquivo de Mapa de Agregação Contido na Memória em KB|Tamanho atual do arquivo de mapa de agregação contido na memória, em KB.|  
|Arquivo de Mapa de Agregação Contido na Memória em KB/s|Taxa de gravações no arquivo de mapa de agregação contido na memória, em KB.|  
|Arquivo de Mapa de Agregação Contido na Memória Potencial em KB|Tamanho do arquivo de mapa de agregação contido na memória potencial, em KB.|  
|Arquivos de mapa de agregação|Número de arquivos de mapa de agregação.|  
|Arquivo de Dados de Fato Contido na Memória em KB|Tamanho do arquivo de dados atual de fato contido na memória, em KB.|  
|Arquivo de Dados de Fato Contido na Memória em KB/s|Taxas de gravações no arquivo de dados de fato contido na memória, em KB.|  
|Arquivo de Dados de Fato Contido na Memória Potencial em KB|Tamanho do arquivo de dados de fato contido na memória potencial, em KB.|  
|Arquivos de Dados de Fato|Número de arquivos de dados de fato.|  
|Arquivo de Cadeia de Caracteres de Fato Contido na Memória em KB|Tamanho do arquivo de cadeia de caracteres atual de fato contido na memória, em KB.|  
|Arquivo de Cadeia de Caracteres de Fato Contido na Memória em KB/s|Taxa de gravações no arquivo da cadeia de caracteres de fato contido na memória, em KB.|  
|Arquivo de Cadeia de Caracteres de Fato Contido na Memória Potencial em KB|Tamanho do arquivo de cadeia de caracteres de fato contido na memória potencial, em KB.|  
|Arquivos de Cadeia de Caracteres de Fato|Número de arquivos de cadeia de caracteres de fato.|  
|Arquivo de Agregação de Fato Contido na Memória em KB|Tamanho atual do arquivo de agregação de fato contido na memória, em KB.|  
|Arquivo de Agregação de Fato Contido na Memória em KB/s|Taxa de gravações no arquivo de agregação de fato contido na memória, em KB.|  
|Arquivo de Agregação de Fato Contido na Memória Potencial em KB|Tamanho do arquivo de agregação de fato contido na memória potencial, em KB.|  
|Arquivos de Agregação de Fato|Número de arquivos de agregação de fato.|  
|Outro Arquivo Contido na Memória em KB|Tamanho do outro arquivo contido na memória atual, em KB.|  
|Outro Arquivo Contido na Memória em KB/s|Taxa de gravações em outro arquivo contido na memória, em KB.|  
|Outro Arquivo Contido na Memória Potencial em KB|Tamanho do outro arquivo contido na memória potencial, em KB.|  
|Outros arquivos|Número de outros arquivos.|  
|KB Pagináveis para VertiPaq|Quilobytes de memória paginável em uso para dados na memória.|  
|KB Não Pagináveis para VertiPaq|Quilobytes de memória bloqueada no conjunto de trabalho para uso pelo mecanismo na memória.|  
|KB Mapeado pela Memória de VertiPaq|Quilobytes de memória paginável em uso para dados na memória.|  
|KB de limite de memória física|Limite de memória física, do arquivo de configuração.|  
|KB de limite de memória de VertiPaq|Limite na memória, do arquivo de configuração.|  
  
###  <a name="proactive-caching"></a><a name="bkmk_ProactiveCaching"></a>Cache pró-ativo  
 Estatísticas relacionadas ao cache pró-ativo do Microsoft Analysis Services.  
  
|Contador|Descrição|  
|-------------|-----------------|  
|Notificações/s|Taxa de notificações de banco de dados relacional.|  
|Cancelamentos de processamento/s|Taxa de cancelamentos de processamento causada por notificações.|  
|Início de Cache Pró-ativo/s|Taxa de início do cache pró-ativo.|  
|Conclusão de Cache Pró-ativo/s|Taxa de conclusão do cache pró-ativo.|  
  
###  <a name="processing-aggregations"></a><a name="bkmk_ProcAggregations"></a>Processando agregações  
 Estatísticas relacionadas ao processamento de agregações do Microsoft Analysis Services em arquivos de dados MOLAP.  
  
|Contador|Descrição|  
|-------------|-----------------|  
|Partições atuais|Número atual de partições sendo processadas.|  
|Total de partições|Número total de partições processadas (com êxito ou não).|  
|Linhas do tamanho da memória|Tamanho de agregações atuais na memória.  Esta contagem é uma estimativa.|  
|Bytes do tamanho da memória|Tamanho de agregações atuais na memória.  Esta contagem é uma estimativa.|  
|Linhas mescladas/s|Taxa de linhas mescladas ou inseridas em uma agregação.|  
|Linhas criadas/s|Taxa de linhas de agregação criadas.|  
|Linhas de arquivo temp. gravadas/s|Taxa de linhas gravadas em arquivo temporário.  Arquivos temporários são gravados quando agregações excedem os limites de memória.|  
|Bytes do arquivo temp. gravados/s|Taxa de bytes gravados em arquivo temporário.  Arquivos temporários são gravados quando agregações excedem os limites de memória.|  
  
###  <a name="processing-indexes"></a><a name="bkmk_ProcIndexes"></a>Processando índices  
 Estatísticas relacionadas ao processamento de índices do Microsoft Analysis Services para arquivos de dados MOLAP.  
  
|Contador|Descrição|  
|-------------|-----------------|  
|Partições atuais|Número atual de partições sendo processadas.|  
|Total de partições|Número total de partições processadas (com êxito ou não).|  
|Linhas/s|Taxa de linhas de arquivos MOLAP usados para criar índices.|  
|Linhas de total|Total de linhas de arquivos MOLAP usados para criar índices.|  
  
###  <a name="processing"></a><a name="bkmk_Processing"></a>Processamento  
 Estatísticas relacionadas ao processamento de dados do Microsoft Analysis Services.  
  
|Contador|Descrição|  
|-------------|-----------------|  
|Linhas lidas/s|Taxa de linhas lidas de todos os bancos de dados relacionais.|  
|Total de linhas lidas|Contagem de linhas lidas de todos os bancos de dados relacionais.|  
|Linhas convertidas/s|Taxa de linhas convertidas durante o processamento.|  
|Total de linhas convertidas|Contagem de linhas convertidas durante o processamento.|  
|Linhas gravadas/s|Taxa de linhas gravadas durante o processamento.|  
|Total de linhas gravadas|Contagem de linhas gravadas durante o processamento.|  
  
###  <a name="storage-engine-query"></a><a name="bkmk_StorageEngineQuery"></a>Consulta do mecanismo de armazenamento  
 Estatísticas relacionadas a consultas do mecanismo de armazenamento do Microsoft Analysis Services.  
  
|Contador|Descrição|  
|-------------|-----------------|  
|Consultas de grupo de medidas atuais|Número atual de consultas de grupo de medidas que estão em operação ativa.|  
|Consultas do grupo de medidas/s|Taxa de consultas do grupo de medidas|  
|Total de consultas do grupo de medidas|Número total de consultas a grupo de medidas.|  
|Consultas de dimensão atuais|Número atual de consultas de dimensão em operação ativa.|  
|Consultas de dimensão/s|Taxa de consultas de dimensão|  
|Total de consultas de dimensão.|Número total de consultas de dimensão.|  
|Consultas respondidas/s|Taxa de consultas respondidas.|  
|Total de consultas respondidas|Número total de consultas respondidas.|  
|Bytes enviados/s|Taxa de bytes enviados pelo servidor a clientes, em resposta a consultas.|  
|Total de bytes enviados|Total de bytes enviados pelo servidor a clientes, em resposta a consultas.|  
|Linhas enviadas/s|Taxa de linhas enviadas pelo servidor a clientes.|  
|Total de linhas enviadas|Total de linhas enviadas pelo servidor a clientes.|  
|Consultas direto do cache/s|Taxa de consultas respondidas diretamente do cache.|  
|Consultas filtradas do cache/s|Taxa de consultas respondidas por filtragem da entrada de cache existente.|  
|Consultas de arquivo/s|Taxa de consultas respondidas de arquivos.|  
|Total de consultas direto do cache|Número total de consultas derivadas diretamente do cache.  Observe que isso ocorre por partição.|  
|Total de consultas filtradas do cache|Total de consultas respondidas por filtragem de entradas de cache existente.|  
|Total de consultas de arquivo|Número total de consultas respondidas de arquivos.|  
|Leituras de mapa/s|Número de operações de leitura lógicas usando o arquivo de Mapa.|  
|Bytes de mapa/s|Bytes lidos do arquivo de Mapa.|  
|Leituras de dados/s|Número de operações de leitura lógicas usando o arquivo de Dados.|  
|Bytes de dados/s|Bytes lidos do arquivo de Dados.|  
|Tempo médio/consulta|Tempo médio por consulta, em milissegundos.  Tempo de resposta baseado em consultas respondidas desde a última medida de contador.|  
|Viagens de ida e volta da rede/s|Taxa de viagens de ida e volta da rede.  Isto inclui toda a comunicação cliente/servidor.|  
|Total de viagens de ida e volta da rede|Total de viagens de ida e volta da rede.  Isto inclui toda a comunicação cliente/servidor.|  
|Pesquisas de cache simples/s|Taxa de pesquisas de cache simples.  Isto inclui caches simples de escopo global, sessão e consulta.|  
|Acertos de cache simples/s|Taxa de acertos de cache simples.  Isto inclui caches simples de escopo global, sessão e consulta.|  
|Pesquisas de cache de cálculo/s|Taxa de pesquisas de cache de cálculo.  Isto inclui caches de cálculo de escopo global, sessão e consulta.|  
|Acertos de cache de cálculo/s|Taxa de acertos de cache de cálculo.  Isto inclui caches de cálculo de escopo global, sessão e consulta.|  
|Pesquisas de cache persistente/s|Taxa de pesquisas de cache persistente.  Caches persistentes são criados pela instrução CACHE de script MDX.|  
|Acertos de cache persistente/s|Taxa de acertos de cache persistente.  Caches persistentes são criados pela instrução CACHE de script MDX.|  
|Pesquisas de cache de dimensão/s|Taxa de pesquisas de cache de dimensão.|  
|Acertos de cache de dimensão/s|Taxa de acertos de cache de dimensão.|  
|Pesquisas de cache de grupo de medidas/s|Taxa de pesquisas de cache de grupo de medidas.|  
|Acertos de cache de grupo de medidas/s|Taxa de acertos de cache de grupo de medidas.|  
|Pesquisas de agregação/s|Taxa de pesquisas de agregação.|  
|Acertos de agregação/s|Taxa de acertos de agregação.|  
  
###  <a name="threads"></a><a name="bkmk_Threads"></a>Threads  
 Estatísticas relacionadas a threads do Microsoft Analysis Services.  
  
|Contador|Descrição|  
|-------------|-----------------|  
|Threads ociosos de análise resumida|Número de threads ociosos no pool de threads de análise resumida.|  
|Threads ocupados de análise resumida|Número de threads ocupados no pool de threads de análise resumida.|  
|Tamanho da fila de trabalhos de análise resumida|Número de trabalhos na fila do pool de threads de análise resumida.|  
|Taxa de trabalhos da análise resumida|Taxa de trabalhos através do pool de threads da análise resumida.|  
|Threads ociosos de análise longa|Número de threads ociosos no pool de threads de análise longa.|  
|Threads ocupados de análise longa|Número de threads ocupados no pool de threads de análise longa.|  
|Tamanho da fila de trabalhos de análise longa|Número de trabalhos na fila do pool de threads de análise longa.|  
|Taxa de trabalhos da análise longa|Taxa de trabalhos através do pool de threads da análise longa.|  
|Threads ociosos do pool de consultas|Número de threads ociosos no pool de threads de consulta.|  
|Threads ocupados do pool de consulta|Número de threads ocupados no pool de threads de consulta.|  
|Tamanho da fila de trabalhos do pool consultas|Número de trabalhos na fila do pool de threads de consulta.|  
|Taxa de trabalho do pool de consulta|Taxa de trabalhos através do pool de threads de consulta.|  
|Threads de trabalho não E/S ociosos do pool de processamento|Número de threads ociosos no pool de threads de processamento dedicado a trabalhos não E/S.|  
|Threads de trabalho não E/S ocupados do pool de processamento|Número de threads que executam trabalhos não E/S no pool de threads de processamento.|  
|Comprimento da fila de trabalhos do pool de processamento|Número de trabalhos não de E/S na fila do pool de threads de processamento.|  
|Taxa de processamento de trabalho do pool|Taxa de trabalhos não E/S através do pool de thread de processamento.|  
|Threads de trabalho de E/S ociosos do pool de processamento|Número de threads ociosos para trabalhos de E/S no pool de threads de processamento.|  
|Threads de trabalho de E/S ocupados do pool de processamento|Número de threads que executam trabalhos de E/S no pool de threads de processamento.|  
|Comprimento da fila de trabalho de E/S do pool de processamento|Número de trabalhos de E/S na fila do pool de threads de processamento.|  
|Taxa de conclusão de trabalho de E/S do pool de processamento|Taxa de trabalhos de E/S através do pool de thread de processamento.|  
  
  
