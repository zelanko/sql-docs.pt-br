---
title: "Guia de arquitetura de gerenciamento de memória | Microsoft Docs"
ms.custom: 
ms.date: 10/21/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- guide, memory management architecture
- memory management architecture guide
ms.assetid: 7b0d0988-a3d8-4c25-a276-c1bdba80d6d5
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d00e5c97e6c27f3fe40b2066b5e194b8011f6b1e
ms.lasthandoff: 04/11/2017

---
# <a name="memory-management-architecture-guide"></a>guia de arquitetura de gerenciamento de memória
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

## <a name="memory-architecture"></a>Arquitetura de memória

O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] adquire e libera memória dinamicamente conforme necessário. Normalmente, um administrador não precisa especificar a quantidade de memória que deve ser alocada ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], embora essa opção exista e seja necessária em alguns ambientes.

Uma das principais metas de design de todo o software de banco de dados é minimizar a E/S de disco devido às leituras e gravações de disco estarem entre as operações que consomem muitos recursos. O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cria um pool de buffers na memória para manter a leitura de páginas do banco de dados. Grande parte do código do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é dedicada a minimizar o número de leituras e gravações físicas entre o disco e o pool de buffers. O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tenta alcançar um equilíbrio entre as duas metas:

* Evitar que o pool de buffers fique tão grande que o sistema inteiro fique com pouca memória.
* Minimizar a E/S física aos arquivos de banco de dados maximizando o tamanho do pool de buffers.


> [!NOTE]
> Em um sistema amplamente carregado, algumas consultas grandes que exigem muita memória para serem executadas não conseguem obter a quantidade mínima de memória solicitada e recebem um erro de tempo limite enquanto esperam recursos de memória. Para resolver isso, aumente a [Opção query wait](../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md). Para uma consulta paralela, considere a redução da [Opção de grau máximo de paralelismo](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).
 
> [!NOTE]
> Em um sistema amplamente carregado sob pressão de memória, as consultas com junção de mesclagem, classificação e bitmap no plano de consulta podem cancelar o bitmap quando as consultas não adquirem a memória mínima necessária para o bitmap. Isso pode afetar o desempenho da consulta e, se o processo de classificação não conseguir se ajustar na memória, poderá aumentar o uso de tabelas de trabalho no banco de dados tempdb, aumentando o tempdb. Para resolver esse problema, adicione memória física ou ajuste as consultas para usar um plano de consulta diferente e mais rápido.
 
### <a name="providing-the-maximum-amount-of-memory-to-includessnoversionincludesssnoversion-mdmd"></a>Fornecendo a quantidade máxima de memória para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

Ao usar o AWE e o privilégio Páginas Bloqueadas na Memória, você pode fornecer as quantidades de memória a seguir para o Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . (A tabela a seguir inclui uma coluna para versões de 32 bits que não estão mais disponíveis.)

| |32 bits <sup>1</sup> |64 bits
|-------|-------|-------| 
|Memória convencional |Todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Até o limite de espaço de endereço virtual do processo: <br>- 2 GB<br>- 3 GB com parâmetro de inicialização de /3gb <sup>2</sup> <br>- 4 GB no WOW64 <sup>3</sup> |Todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Até o limite de espaço de endereço virtual do processo: <br>- 7 TB com arquitetura IA64 (IA64 não tem suporte no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] e posterior)<br>- Máximo do sistema operacional com a arquitetura x64 <sup>4</sup>
|Mecanismo AWE (Permite ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ir além do limite de espaço de endereço virtual do processo na plataforma de 32 bits.) |Edições Standard, Enterprise e Developer do[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] : o pool de buffers é capaz de acessar até 64 GB de memória.|Não aplicável <sup>5</sup> |
|Páginas bloqueadas no privilégio do sistema operacional da memória (Permite bloqueio de memória física, evitando a paginação do sistema operacional da memória bloqueada). <sup>6</sup> |Edições Standard, Enterprise e Developer do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]: necessárias para o processo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usar o mecanismo AWE. A memória alocada pelo mecanismo AWE não pode passar pelo page out. <br> A concessão desse privilégio sem a ativação de AWE não tem nenhum efeito no servidor. |Edições Enterprise e Developer do[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] : recomendadas, para evitar a paginação do sistema operacional. Pode fornecer um benefício de desempenho dependendo da carga de trabalho. A quantidade de memória acessível é semelhante a da memória convencional. |

<sup>1</sup> Versões de 32 bits não estão disponíveis a partir do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
<sup>2</sup> /3gb é um parâmetro de inicialização do sistema operacional. Para saber mais, visite a Biblioteca MSDN.  
<sup>3</sup> WOW64 (Windows on Windows 64) é um modo em que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de 32 bits é executado em um sistema operacional de 64 bits.  
<sup>4</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard Edition supports up to 128 GB. O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition oferece suporte a, no máximo, o limite do sistema operacional.  
<sup>5</sup> Observe que a opção sp_configure awe enabled estava presente no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]de 64 bits, mas é ignorada.    
<sup>6</sup> Se as páginas bloqueadas no privilégio de memória (LPIM) forem concedidas (em 32 bits para suporte AWE ou em 64 bits por si só), também é recomendável a definição da memória máxima do servidor.

> [!NOTE]
> Versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] podiam ser executadas em um sistema operacional de 32 bits. O acesso a mais de quatro gigabytes de memória em um sistema operacional de 32 bits exige o AWE (Address Windowing Extensions) para gerenciar a memória. Isso não é necessário quando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está em execução em sistemas operacionais de 64 bits. Para saber mais sobre o AWE, veja [Espaço de endereço de processo](https://msdn.microsoft.com/library/ms189334) e [Gerenciando memória para bancos de dados grandes](https://msdn.microsoft.com/library/ms191481) na documentação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2008.   


## <a name="dynamic-memory-management"></a>Gerenciamento de memória dinâmica

O comportamento de gerenciamento de memória padrão do Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] da Microsoft é adquirir a quantidade de memória necessária sem provocar escassez de memória no sistema. O Mecanismo de Banco de Dados faz isto usando as APIs de Notificação de memória no Microsoft Windows.

O espaço de endereço virtual do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode ser dividido em duas regiões distintas: espaço ocupado pelo pool de buffers e o restante. Se o mecanismo de AWE for habilitado, o pool de buffers poderá residir na memória mapeada AWE, fornecendo espaço adicional para páginas de banco de dados. 

O pool de buffers serve como fonte de alocação de memória primária do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Os componentes externos que residem no processo do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , como objetos COM, e que não reconhecem os recursos de gerenciamento de memória do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , usam a memória fora do espaço de endereço virtual ocupado pelo pool de buffers.

Quando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é iniciado, ele computa o tamanho do espaço de endereço virtual do pool de buffers baseado em vários parâmetros, como quantidade de memória física no sistema, número de threads de servidor e vários parâmetros de inicialização. O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] reserva a quantidade computada do seu espaço de endereço virtual de processo do pool de buffers, mas adquire (confirma) somente a quantidade exigida da memória física para a carga atual.

A instância continua adquirindo memória conforme necessário para atender a carga de trabalho. Como mais usuários conectam e executam consultas, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] adquire a memória física adicional por demanda. Uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] continua adquirindo memória física até alcançar o destino de alocação max server memory ou o Windows indicar que não há excesso de memória livre; ela libera memória quando tem mais que a configuração de min server memory e o Windows indicar que há uma escassez de memória livre.

Conforme são iniciados outros aplicativos em um computador que está executando uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], eles consomem memória e a quantidade de memória física livre reduz o destino do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . A instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ajusta seu consumo de memória. Se outro aplicativo for interrompido e, com isso, houver mais memória disponível, a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] aumentará o tamanho de sua alocação de memória. O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode liberar e adquirir vários megabytes de memória por segundo, permitindo o ajuste rápido às mudanças na alocação de memória.


## <a name="effects-of-min-and-max-server-memory"></a>Efeitos de memória mínima e máxima do servidor

As opções de configuração min server memory e max server memory estabelecem limites superiores e inferiores à quantidade de memória usada pelo pool de buffers do Mecanismo de Banco de Dados do Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . O pool de buffers não adquire imediatamente a quantidade de memória especificada na min server memory. O pool de buffers é iniciado apenas com a memória exigida para inicialização. Conforme a carga de trabalho do Mecanismo de Banco de Dados aumenta, ele continua adquirindo a memória exigida para oferecer suporte à carga de trabalho. O pool de buffers não libera a memória adquirida até atingir a quantidade especificada na min server memory. Quando a min server memory é atingida, o pool de buffers usa o algoritmo padrão para adquirir e liberar memória, conforme necessário. A única diferença é que o pool de buffers nunca cancela sua alocação de memória abaixo do nível especificado na min server memory, e nunca adquire mais memória que o nível especificado na max server memory.

> [!NOTE]
> Como um processo, o[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] adquire mais memória do que a especificada pela opção max server memory. Os componentes internos e externos podem alocar memória fora do pool de buffers, o que consome memória adicional, mas a memória alocada ao pool de buffers normalmente representa a parte maior da memória consumida pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].


A quantidade de memória adquirida pelo Mecanismo de Banco de Dados é completamente dependente da carga de trabalho colocada na instância. Uma instância [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que não está processando muitas solicitações nunca consegue atingir a min server memory.

Se o mesmo valor for especificado para a min server memory e a max server memory, quando a memória alocada ao Mecanismo de Banco de Dados atingir o valor, o Mecanismo de Banco de Dados interromperá a liberação e a aquisição dinamicamente para o pool de buffers.

Se uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] estiver sendo executada em um computador em que outros aplicativos são interrompidos ou iniciados com frequência, a alocação e a desalocação de memória pela instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] poderão reduzir as inicializações dos outros aplicativos. Além disso, se o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] for um dos vários aplicativos de servidor em execução em um único computador, os administradores de sistema poderão precisar controlar a quantidade de memória alocada ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Nesses casos, você pode usar as opções min server memory e max server memory para controlar a quantidade de memória que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode usar. Para saber mais, veja [Opções de configuração de memória do servidor](../database-engine/configure-windows/server-memory-server-configuration-options.md).

As opções min server memory e max server memory são especificadas em megabytes.

## <a name="memory-used-by-includessnoversionincludesssnoversion-mdmd-objects-specifications"></a>Memória usada por especificações de objetos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

A lista a seguir descreve a quantidade aproximada de memória usada por diferentes objetos no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Os valores listados são estimativas e podem variar dependendo do ambiente e como os objetos são criados.

* Bloqueio: 64 bytes + 32 bytes por proprietário   
* Conexão do usuário: aproximadamente (3* *network_packet_size + 94 kb)    

O tamanho do pacote de rede é o tamanho dos pacotes TDS (tabular data scheme) que são usados para comunicação entre aplicativos e o Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . O tamanho de pacote padrão é 4 KB e é controlado pela opção de configuração tamanho do pacote de rede.

Quando o MARS (conjunto de resultados ativos múltiplos) estiver habilitado, a conexão do usuário será de aproximadamente (3 + 3 * num_logical_connections) * network_packet_size + 94 KB

## <a name="buffer-management"></a>Gerenciamento de buffer

A principal finalidade de um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é armazenar e recuperar dados, de modo que a intensa E/S de disco é uma característica importante do Mecanismo de Banco de Dados. Como as operações de E/S de disco podem consumir muitos recursos e levar um tempo relativamente longo para terminar, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se concentra em tornar a E/S altamente eficiente. O gerenciamento de buffer é um componente fundamental para alcançar essa eficiência. O componente de gerenciamento de buffer consiste em dois mecanismos: o gerenciador de buffer para acessar e atualizar páginas de banco de dados e o cache do buffer (também chamado de pool de buffers), para reduzir a E/S do arquivo de banco de dados. 

### <a name="how-buffer-management-works"></a>Como funciona o gerenciamento de buffer

Um buffer é uma página de 8 KB da memória, mesmo tamanho de uma página de dados ou de índice. Portanto, o cache do buffer é dividido em páginas de 8 KB. O gerenciador de buffer gerencia as funções lendo páginas de dados ou de índice dos arquivos do disco de banco de dados no cache do buffer e gravando páginas modificadas de volta no disco. Uma página permanece no cache do buffer até que o gerenciador de buffer precise da área de buffer para ler mais dados. Os dados serão gravados no disco apenas se forem modificados. Os dados podem ser modificados no cache do buffer várias vezes antes de serem gravados no disco. Para saber mais, veja [Lendo Páginas](../relational-databases/reading-pages.md) e [Gravando Páginas](../relational-databases/writing-pages.md).

Quando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é iniciado, ele computa o tamanho do espaço de endereço virtual do cache de buffers com base em vários parâmetros, como quantidade de memória física no sistema, número máximo de threads de servidor configurado e vários parâmetros de inicialização. O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] reserva essa quantidade computada de seu espaço de endereço virtual de processo (chamado de memória cache) do cache de buffers, mas adquire (confirma) somente a quantidade exigida da memória física para a carga atual. Você pode consultar as colunas **bpool_commit_target** e **bpool_committed columns** na exibição do catálogo [sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) para retornar o número de páginas reservado como destino de memória e o número de páginas atualmente confirmado no cache do buffer, respectivamente.

O intervalo entre a inicialização do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e o momento em que o cache do buffer obtém seu destino de memória é chamado de ramp-up. Nesse momento, as solicitações de leitura preenchem os buffers conforme necessário. Por exemplo, uma solicitação de leitura de página única preenche apenas uma página de buffer. Isso significa que o ramp-up depende do número e do tipo de solicitações do cliente. O ramp-up é expedido transformando as solicitações de leitura de página única em solicitações de oito páginas alinhadas. Isso permite ao ramp-up terminar de forma muito mais rápida, especialmente em máquinas com muita memória.

Como o gerenciador de buffer usa a maior parte da memória no processo do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , ele coopera com o gerenciador de memória para permitir que outros componentes usem seus buffers. O gerenciador de buffer interage principalmente com os seguintes componentes:

* Gerenciador de recurso para controlar o uso de memória global e, em plataformas de 32 bits, controlar o uso de espaço de endereço.  
* Gerenciador de banco de dados e SQLOS ( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Operating System) para operações de E/S de arquivo de nível baixo.  
* Gerenciador de log para log write-ahead.  

### <a name="supported-features"></a>Recursos com suporte

O gerenciador de buffer oferece suporte aos seguintes recursos:

* O gerenciador de buffer reconhece NUMA (acesso não uniforme à memória por software). São distribuídas páginas de cache do buffer em nós NUMA de hardware, que permitem a um thread acessar uma página de buffer alocada no nó NUMA local em vez de memória externa. 
* O gerenciador de buffer oferece suporte à Inclusão de Memória a Quente, que permite aos usuários adicionar memória física sem reiniciar o servidor. 
* O gerenciador de buffer oferece suporte a páginas grandes em plataformas de 64 bits. O tamanho da página é específico para a versão do Windows. 
* O gerenciador de buffer fornece diagnósticos adicionais que são expostos por meio de exibições de gerenciamento dinâmico. Você pode usar essas exibições para monitorar uma variedade de recursos de sistema operacional específicos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Por exemplo, é possível usar a exibição sys.dm_os_buffer_descriptors para monitorar as páginas no cache do buffer.   

### <a name="disk-io"></a>E/S de disco
O gerenciador de buffer apenas faz leituras e gravações no banco de dados. Outras operações de arquivo e banco de dados, como abrir, fechar, estender e reduzir são executadas pelos componentes do gerenciador de banco de dados e de arquivos. 

As operações de E/S de disco pelo gerenciador de buffer têm as seguintes características:

* Todas as E/S são executadas de forma assíncrona, o que permite ao thread de chamada continuar o processamento enquanto a operação de E/S acontece em segundo plano.
* Todas as E/S são emitidas nos threads de chamada, a menos que a opção affinity I/O esteja em uso. A opção affinity I/O mask associa a E/S de disco do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a um subconjunto especificado de CPUs. Em ambientes OLTP (online transactional processing) avançados de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , esta extensão pode aumentar o desempenho de threads [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que emitem E/S.
* Várias E/Ss de página são realizadas com E/S de dispersar e reunir, que permite transferir dados para dentro ou para fora de áreas não contíguas de memória. Isso significa que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode preencher ou liberar o cache do buffer rapidamente enquanto evita várias solicitações de E/S físicas. 

#### <a name="long-io-requests"></a>Solicitações de E/S demoradas  
O gerenciador de buffer fornece informações sobre qualquer solicitação de E/S pendente durante pelo menos 15 segundos. Isso ajuda o administrador de sistema a distinguir entre problemas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e problemas do subsistema de E/S. A mensagem de erro 833 é informada e exibida no log de erros do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como segue:

`` 
SQL Server has encountered %d occurrence(s) of I/O requests taking longer than %d seconds to complete on file [%ls] in database [%ls] (%d). The OS file handle is 0x%p. The offset of the latest long I/O is: %#016I64x.
`` 

Uma E/S demorada pode ser uma leitura ou uma gravação. Isso não está indicado atualmente na mensagem. Mensagens de E/S demoradas são avisos, não erros. Elas não indicam problemas com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. As mensagens são informadas para ajudar o administrador de sistema a encontrar mais depressa a causa de tempos de resposta insatisfatórios do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e distinguir problemas que estão fora do controle do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Como tal, eles não exigem nenhuma ação, mas o administrador do sistema deve investigar por que a solicitação de E/S demorou tanto e se o tempo é justificável.

#### <a name="causes-of-long-io-requests"></a>Causas de solicitações de E/S demoradas  
Uma mensagem de E/S demorada pode indicar que uma E/S está bloqueada permanentemente e nunca será concluída (conhecida como E/S perdida) ou, então, que apenas não foi concluída ainda. Não é possível distinguir qual é o cenário com base na mensagem, embora uma E/S perdida geralmente conduza a um tempo limite de trava.

E/S demorada geralmente indica uma carga de trabalho do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] muito intensa para o subsistema de disco. Um subsistema de disco inadequado pode ser indicado quando:

* Várias mensagens de E/S demorada são exibidas no log de erros durante uma carga de trabalho pesada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .
* Contadores de desempenho mostram latências de disco demoradas, filas de disco demoradas ou nenhum tempo ocioso de disco.  

E/Ss demoradas também podem ser causadas por um componente no caminho de E/S (por exemplo, driver, controlador ou firmware) que continuamente adia o atendimento de uma solicitação de E/S antiga a favor do atendimento mais próximo à posição atual da cabeça de disco. A técnica comum de processamento de solicitações com prioridade baseada no atendimento mais próximo à posição atual da cabeça de leitura/gravação é conhecida como "busca de menor caminho". Isso pode ser difícil de confirmar com a ferramenta do Windows System Monitor (PERFMON.EXE) porque a maioria das E/Ss está sendo atendida prontamente. As solicitações de E/S demoradas podem ser agravadas por cargas de trabalho que executam grandes quantidades de E/S sequenciais, como backup e restauração, exames de tabela, classificação, criação de índices, carregamentos em massa e anulação de arquivos de saída.

E/Ss demoradas e isoladas que não aparecem relacionadas a quaisquer condições anteriores podem ser causadas por um problema de hardware ou driver. O log de eventos do sistema pode conter um evento relacionado que ajuda a diagnosticar o problema.

#### <a name="error-detection"></a>Detecção de erro  
As páginas de banco de dados podem usar um dentre dois mecanismos opcionais que ajudam a garantir a integridade da página do momento em que é gravada no disco até ser lida novamente: proteção de página interrompida e proteção de soma de verificação. Esses mecanismos permitem um método independente para verificar a exatidão não apenas do armazenamento de dados, mas de componentes de hardware, como controladores, drivers, cabos e até mesmo o sistema operacional. A proteção é adicionada à página um pouco antes da gravação no disco e verificada depois da leitura do disco.

#### <a name="torn-page-protection"></a>Proteção de página interrompida  
A proteção de página interrompida , apresentada no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000, é principalmente um modo de detectar páginas corrompidas devido a falhas de energia. Por exemplo, uma falha de energia inesperada pode deixar apenas parte de uma página gravada no disco. Quando a proteção de página interrompida é usada, uma assinatura de 2 bits é colocada no final de cada setor de 512 bytes na página (depois de ter copiado os dois bits originais no cabeçalho da página). A assinatura alterna entre 01 e 10 binário com toda gravação, de modo que seja sempre possível informar quando apenas uma parte dos setores realizou essa operação no disco: se um bit estiver com estado inválido quando a página for lida posteriormente, a página foi gravada incorretamente e uma página interrompida é detectada. A detecção de página interrompida usa recursos mínimos; porém, não detecta todos os erros provocados por falhas de hardware de disco.

#### <a name="checksum-protection"></a>Proteção de soma de verificação  
A proteção de soma de verificação, apresentada no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2005, fornece verificação de integridade de dados mais resistente. Uma soma de verificação é calculada para os dados de cada página gravada e armazenada no cabeçalho da página. Sempre que uma página com uma soma de verificação armazenada é lida no disco, o Mecanismo de Banco de Dados recalcula a soma de verificação dos dados na página e gera o erro 824 se a nova soma de verificação for diferente da soma de verificação armazenada. A proteção de soma de verificação pode capturar mais erros que a proteção de página interrompida porque é afetada por todo byte da página, porém, é um recurso moderadamente intensivo. Quando a soma de verificação for habilitada, os erros causados por falta de energia e falha de hardware ou firmware poderão ser detectados sempre que o gerenciador de buffer ler uma página do disco.

O tipo de proteção de página usado é um atributo do banco de dados que contém a página. A proteção de soma de verificação é a proteção padrão para bancos de dados criados no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2005 e posterior. O mecanismo de proteção de página é especificado no momento de criação do banco de dados e pode ser alterado usando ALTER DATABASE. Você pode determinar a configuração de proteção da página atual, consultando a coluna page_verify_option na exibição do catálogo [sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md) ou na propriedade IsTornPageDetectionEnabled da função [DATABASEPROPERTYEX](../t-sql/functions/databasepropertyex-transact-sql.md) . Se a configuração de proteção de página for alterada, a configuração nova não afetará imediatamente o banco de dados inteiro. Em vez disso, as páginas adotarão o nível de proteção atual do banco de dados sempre que eles forem gravados posteriormente. Isso significa que o banco de dados pode ser composto de páginas com tipos diferentes de proteção. 

## <a name="understanding-non-uniform-memory-access"></a>Compreendendo o Non-uniform Memory Access

O Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] reconhece o NUMA (Non-uniform Memory Access) e tem um bom desempenho em hardware de NUMA sem configuração especial. Devido ao aumento da velocidade de clock e do número de processadores, fica muito difícil reduzir a latência de memória exigida para usar este poder de processamento adicional. Para evitar isto, fornecedores de hardware fornecem caches de L3 grandes, mas esta é apenas uma solução limitada. A arquitetura NUMA oferece uma solução escalonável para esse problema. O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] foi projetado para tirar proveito de computadores baseados em NUMA sem exigir nenhuma mudança de aplicativo. Para saber mais, veja [Como configurar o SQL Server para usar o Soft-NUMA](../database-engine/configure-windows/soft-numa-sql-server.md).

## <a name="see-also"></a>Consulte também
[Lendo Páginas](../relational-databases/reading-pages.md)   
 [Gravando Páginas](../relational-databases/writing-pages.md)


