---
title: Opções de configuração de servidor Server Memory | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Virtual Memory Manager
- max server memory option
- virtual memory [SQL Server]
- VMM
- server memory options [SQL Server]
- servers [SQL Server], memory
- buffer pools [SQL Server]
- min server memory option
- manual memory options [SQL Server]
- memory [SQL Server], servers
ms.assetid: 29ce373e-18f8-46ff-aea6-15bbb10fb9c2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e3d3a6524d0f7e791628ec664bc9b5df17a0e529
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59042185"
---
# <a name="server-memory-server-configuration-options"></a>Opções Server Memory de configuração do servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Use as duas opções de memória de servidor, **memória mínima do servidor** e **memória máxima do servidor**, para reconfigurar a quantidade de memória (em megabytes) que é gerenciada pelo Gerenciador de Memória do SQL Server para um processo do SQL Server usado por uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
A configuração padrão de **min server memory** é 0 e a configuração padrão de **max server memory** é 2.147.483.647 MB (megabytes). Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode alterar seus requisitos de memória dinamicamente com base nos recursos do sistema disponíveis. Para obter mais informações, consulte [Gerenciamento de memória dinâmica](../../relational-databases/memory-management-architecture-guide.md#dynamic-memory-management). 

A quantidade mínima de memória permitida para a **memória máxima do servidor** é de 128 MB.
  
> [!IMPORTANT]  
> Configurar o valor de **max server memory** como muito alto pode fazer com que uma única instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenha que competir por memória com outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hospedadas no mesmo host. No entanto, configurar este valor como muito baixo pode ocasionar uma pressão de memória significativa e problemas de desempenho. Configurar a opção **max server memory** com o valor mínimo pode até mesmo impedir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja iniciado. Se você não puder iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] após alterar essa opção, inicie-o usando a opção de inicialização **_-f_** e redefina a **memória máxima do servidor** para seu valor anterior. Para obter mais informações, consulte [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
    
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar a memória de modo dinâmico. No entanto, você pode definir as opções de memória manualmente e restringir a quantidade de memória que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode acessar. Antes de definir a quantidade de memória para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], determine a configuração de memória apropriada ao subtrair, da memória física total, a memória necessária para o sistema operacional, as alocações de memória não controladas pela configuração max_server_memory e quaisquer outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (e outros usos do sistema, caso o computador não esteja totalmente dedicado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Essa diferença é a quantidade máxima de memória que você pode atribuir à instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atual.  
 
## <a name="setting-the-memory-options-manually"></a>Configurando as opções de memória manualmente  
As opções **min server memory** e **max server memory** do servidor podem ser definidas para abrangerem um intervalo de valores de memória. Esse método é útil para os administradores de banco de dados ou de sistemas configurarem uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em conjunto com os requisitos de memória de outros aplicativos ou de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executadas no mesmo host.

> [!NOTE]
> As opções **memória mínima do servidor** e **memória máxima do servidor** são opções avançadas. Se você estiver usando o procedimento armazenado no sistema **sp_configure** para alterar essas configurações, será possível alterá-las apenas quando **show advanced options** estiver definida como 1. Essas configurações entram em vigor imediatamente sem a reinicialização do servidor.  
  
<a name="min_server_memory"></a> Use **min_server_memory** para garantir uma quantidade mínima de memória disponível para o Gerenciador de Memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não alocará imediatamente a quantidade de memória especificada em **memória mínima do servidor** na inicialização. Porém, depois que o uso de memória atingir esse valor devido à carga do cliente, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não poderá liberar memória livre a menos que o valor de **memória mínima do servidor** seja reduzido. Por exemplo, quando várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puderem existir simultaneamente no mesmo host, defina o parâmetro min_server_memory em vez do max_server_memory com a finalidade de reservar memória para uma instância. Além disso, a configuração de um valor de min_server_memory é essencial em um ambiente virtualizado para garantir que a pressão de memória do host subjacente não tente desalocar a memória do pool de buffers em uma VM (máquina virtual) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convidada além do que for necessário para se obter um desempenho aceitável.
 
> [!NOTE]  
> Não há nenhuma garantia de que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aloque a quantidade de memória especificada em **min server memory**. Se a carga do servidor nunca exigir a alocação da quantidade de memória especificada em **memória mínima do servidor**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será executado com menos memória.  
  
<a name="max_server_memory"></a> Utilize **max_server_memory** para garantir que o sistema operacional não experimente uma pressão de memória prejudicial. Para definir a configuração max server memory, monitore o consumo geral do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para determinar os requisitos de memória. Para ser mais preciso com esses cálculos para uma única instância:
 -  Da memória total do SO, reserve de 1 GB a 4 GB para o sistema operacional em si.
 -  Em seguida, subtraia o equivalente a possíveis alocações de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fora do controle **memória máxima do servidor**, que é composto pelo **_tamanho da pilha <sup>1</sup> \* máx. de threads de trabalho calculado <sup>2</sup> + o parâmetro de inicialização -g <sup>3</sup>_** (ou 256 MB por padrão se *-g* não estiver definido). O que sobrar deve ser a configuração max_server_memory para a instalação de uma instância única.
 
<sup>1</sup> Consulte o [Guia de arquitetura de gerenciamento de memória](../../relational-databases/memory-management-architecture-guide.md#stacksizes) para obter informações sobre os tamanhos de pilha de thread por arquitetura.

<sup>2</sup> Consulte a página da documentação sobre como [Configurar a opção max worker threads de configuração de servidor](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md) para obter informações sobre os threads de trabalho padrão calculados para um determinado número de CPUs de afinidade no host atual.

<sup>3</sup> Consulte a página da documentação em [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md) para obter informações sobre o parâmetro de inicialização *-g*.

## <a name="how-to-configure-memory-options-using-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>Como configurar as opções de memória usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
Use as duas opções de memória de servidor, **min server memory** e **max server memory**, para reconfigurar a quantidade de memória (em megabytes) gerenciada pelo Gerenciador de Memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode alterar seus requisitos de memória dinamicamente com base nos recursos do sistema disponíveis.  
  
### <a name="procedure-for-configuring-a-fixed-amount-of-memory-not-recommended"></a>Procedimento para configurar uma quantidade fixa de memória (não recomendado)  
Para definir uma quantidade fixa de memória:  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Memória** .  
  
3.  Em **Opções de Memória do Servidor**, insira a mesma quantidade desejada para **Memória mínima do servidor** e **Memória máxima do servidor**.  
  
     Use as configurações padrão para permitir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] altere seus requisitos de memória de forma dinâmica com base nos recursos disponíveis do sistema. É recomendável definir uma opção **max server memory**, conforme [detalhado acima](#max_server_memory). 
  
## <a name="lock-pages-in-memory-lpim"></a>LPIM (Bloquear Páginas na Memória) 
Essa política do Windows determina quais contas podem usar um processo para manter dados na memória física, impedindo o sistema de paginar os dados para a memória virtual em disco. O bloqueio de páginas na memória pode manter a resposta do servidor quando ocorre paginação de memória no disco. A opção **Bloquear Páginas na Memória** será definida para ON nas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition e superior quando a conta com privilégios para executar o sqlservr.exe tiver recebido o direito de usuário *LPIM* (Bloquear Páginas na Memória) do Windows.  
  
Para desabilitar a opção **Bloquear Páginas na Memória** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], remova o direito de usuário *Bloquear Páginas na Memória* da conta com privilégios para executar a conta de inicialização do sqlservr.exe (a conta de inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]).  
 
A configuração dessa opção não afeta o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [gerenciamento de memória dinâmica](../../relational-databases/memory-management-architecture-guide.md#dynamic-memory-management), permitindo que você expanda ou reduza mediante a solicitação de outros administradores de memória. Ao usar o direito de usuário *Bloquear Páginas na Memória*, é recomendável definir um limite superior para a opção **max server memory**, conforme [detalhado acima](#max_server_memory).

> [!IMPORTANT]
> Essa opção só deverá ser configurada quando necessário, ou seja, se houver sinais de que o processo sqlservr está sendo paginado. Neste caso, o erro 17890 será reportado no log de erros, que se assemelha ao exemplo abaixo: `A significant part of sql server process memory has been paged out. This may result in a performance degradation. Duration: #### seconds. Working set (KB): ####, committed (KB): ####, memory utilization: ##%.`
> A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o [sinalizador de rastreamento 845](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) não é necessário para que a Standard Edition use páginas bloqueadas. 
  
### <a name="to-enable-lock-pages-in-memory"></a>Habilitar a opção Bloquear Páginas na Memória  
Para habilitar a opção Bloquear Páginas na Memória:  
  
1.  No menu **Iniciar** , clique em **Executar**. Na caixa **Abrir** , digite **gpedit.msc**.  
  
     A caixa de diálogo **Política de Grupo** é aberta.  
  
2.  No console **Política de Grupo** , expanda **Configuração do Computador**e então expanda **Configurações do Windows**.  
  
3.  Expanda **Configurações de Segurança**e então expanda **Políticas Locais**.  
  
4.  Selecione a pasta **Atribuição de direitos de usuários** .  
  
     As políticas serão exibidas no painel de detalhes.  
  
5.  No painel, clique duas vezes em **Bloquear páginas na memória**.  
  
6.  Na caixa de diálogo **Configuração da Política de Segurança Local**, adicione a conta com privilégios para executar o sqlservr.exe (a conta de inicialização [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]).  
  
## <a name="running-multiple-instances-of-includessnoversionincludesssnoversion-mdmd"></a>Executando várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Quando você estiver executando várias instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)], há três métodos que você pode usar para gerenciar a memória:  
  
-   Utilize a opção **max server memory** para controlar o uso de memória, conforme [detalhado acima](#max_server_memory). Defina configurações máximas para cada instância, tomando cuidado para que a permissão total não seja maior que a memória física total de sua máquina. É recomendável que cada instância de memória seja proporcional à sua carga de trabalho ou tamanho de banco de dados esperado. Esse método tem a vantagem de que, quando novos processos ou instância forem iniciados, a memória livre estará disponível para eles imediatamente. A desvantagem é que se você não estiver executando todas as instâncias, nenhuma das instâncias sendo executadas poderá utilizar a memória livre restante.  
  
-   Utilize a opção **min server memory** para controlar o uso de memória, conforme [detalhado acima](#min_server_memory). Defina as configurações mínimas de cada instância, de forma que a soma desses mínimos seja entre 1 a 2 GB menor do que a memória física total de sua máquina. Novamente, você pode definir esses mínimos proporcionalmente à carga esperada para a instância. Esse método tem a vantagem de que, se nem todas as instâncias estiverem sendo executadas ao mesmo tempo, as que estiverem sendo executadas poderão usar a memória livre restante. Esse método também é útil quando há outro processo de uso intensivo da memória no computador, de forma que será assegurado que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenha pelo menos uma quantidade razoável de memória. A desvantagem é que quando uma nova instância (ou qualquer outro processo) for iniciada, pode levar algum tempo para que as instâncias liberem memória, principalmente se for necessário gravar páginas modificadas de volta nos respectivos bancos de dados para fazer isso.  
  
-   Não fazer nada (não recomendado). As primeiras instâncias apresentadas com uma carga de trabalho tenderão a alocar toda a memória. Instâncias inativas ou instâncias iniciadas posteriormente poderão acabar com apenas uma quantidade mínima de memória disponível. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tenta equilibrar o uso de memória em instâncias. No entanto, todas as instâncias responderão aos sinais de Notificação de Memória do Windows para ajustar o tamanho de sua superfície de memória. O Windows não balanceia a memória entre aplicativos com a API de Notificação de Memória. Ele simplesmente fornece um feedback global da disponibilidade da memória no sistema.  
  
 É possível alterar essas configurações sem reinicializar as instâncias, para que você possa testar facilmente para encontrar as melhores configurações para seu padrão de uso.  
  
## <a name="providing-the-maximum-amount-of-memory-to-sql-server"></a>Fornecendo a quantidade máxima de memória para o SQL Server  
A memória pode ser configurada até o limite de espaço do endereço virtual do processo em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Limites de memória para as versões do Windows e do Windows Server](/windows/desktop/Memory/memory-limits-for-windows-releases#physical-memory-limits-windows-server-2016).

## <a name="examples"></a>Exemplos

### <a name="example-a-set-the-max-server-memory-option-to-4-gb"></a>Exemplo A. Defina a opção de memória máxima do servidor como 4 GB.
 O exemplo a seguir define a opção `max server memory` como 4 GB.  Observe que, embora `sp_configure` especifique o nome da opção como `max server memory (MB)`, o exemplo demonstra a omissão do `(MB)`.

```sql
sp_configure 'show advanced options', 1;
GO
RECONFIGURE;
GO
sp_configure 'max server memory', 4096;
GO
RECONFIGURE;
GO
```
Isso produzirá uma instrução semelhante a:

> Opção de configuração “memória máxima do servidor (MB)” alterada de 2147483647 para 4096. Execute a instrução RECONFIGURE para instalar.

### <a name="example-b-determining-current-memory-allocation"></a>Exemplo B. Determinando a Alocação de Memória Atual  
 A instrução a seguir retorna informações sobre a memória alocada atualmente.  

```sql  
SELECT 
  physical_memory_in_use_kb/1024 AS sql_physical_memory_in_use_MB, 
    large_page_allocations_kb/1024 AS sql_large_page_allocations_MB, 
    locked_page_allocations_kb/1024 AS sql_locked_page_allocations_MB,
    virtual_address_space_reserved_kb/1024 AS sql_VAS_reserved_MB, 
    virtual_address_space_committed_kb/1024 AS sql_VAS_committed_MB, 
    virtual_address_space_available_kb/1024 AS sql_VAS_available_MB,
    page_fault_count AS sql_page_fault_count,
    memory_utilization_percentage AS sql_memory_utilization_percentage, 
    process_physical_memory_low AS sql_process_physical_memory_low, 
    process_virtual_memory_low AS sql_process_virtual_memory_low
FROM sys.dm_os_process_memory;  
```  

### <a name="example-c-determining-value-for-max-server-memory-mb"></a>Exemplo C. Determinando o valor para “memória máxima do servidor (MB)”
A consulta a seguir retorna informações sobre o valor configurado atualmente e o valor em uso pelo SQL Server.  Essa consulta retornará resultados independentemente se “mostrar opções avançadas” for verdadeiro.

```sql
SELECT c.value, c.value_in_use
FROM sys.configurations c WHERE c.[name] = 'max server memory (MB)'
```
  
## <a name="see-also"></a>Consulte Também  
 [Guia de arquitetura de gerenciamento de memória](../../relational-databases/memory-management-architecture-guide.md)   
 [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md)   
 [Edições e recursos com suporte do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md#Cross-BoxScaleLimits)   
 [Edições e recursos com suporte do SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md#Cross-BoxScaleLimits)   
 [Edições e recursos compatíveis do SQL Server 2017 no Linux](../../linux/sql-server-linux-editions-and-components-2017.md#Cross-BoxScaleLimits)   
 [Limites de memória para as versões do Windows e do Windows Server](/windows/desktop/Memory/memory-limits-for-windows-releases)
