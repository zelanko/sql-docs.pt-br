---
title: Opções de configuração do Server Memory | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: d4f7302da7be80038478c887a01bb32037503fc0
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028690"
---
# <a name="server-memory-configuration-options"></a>Opções de configuração do Server Memory
  Use as duas opções de memória de servidor, **memória mínima do servidor** e **memória máxima do servidor**, para reconfigurar a quantidade de memória (em megabytes) que é gerenciada pelo Gerenciador de Memória do SQL Server para um processo do SQL Server usado por uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A configuração padrão de **memória mínima do servidor** é 0 e a configuração padrão de **memória máxima do servidor** é 2147483647 MB. Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode alterar seus requisitos de memória dinamicamente com base nos recursos do sistema disponíveis.  
  
> [!NOTE]  
> Configurar a **memória máxima do servidor** com o valor mínimo pode reduzir drasticamente o desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e até mesmo impedir sua inicialização. Se você não puder iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] após alterar essa opção, inicie-o usando a opção de inicialização **-f** e redefina **memória máxima do servidor** para seu valor anterior. Para obter mais informações, consulte [Opções de inicialização do serviço Mecanismo de Banco de Dados](database-engine-service-startup-options.md).  
  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está usando memória dinamicamente, ele consulta o sistema periodicamente para determinar a quantidade de memória livre. Manter essa memória livre impede a paginação do SO (sistema operacional). Se menos memória estiver livre, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] liberará memória para o SO. Se houver mais memória livre, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá alocar mais memória. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] adiciona memória apenas quando sua carga de trabalho exige mais. Um servidor em repouso não aumenta o tamanho de seu espaço de endereço virtual.  
  
 Veja o exemplo B para uma consulta que retorna a memória usada atualmente. A**memória máxima do servidor** controla a alocação de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , incluindo o pool de buffers, a memória de compilação, todos os caches, as concessões de memória qe, a memória de gerenciador de bloqueio e a memória do clr (essencialmente qualquer administrador de memória encontrado em **sys.dm_os_memory_clerks**). Memória para as pilhas de thread, heaps de memória, provedores de servidor vinculados diferentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e toda a memória alocada por um DLL não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não são controlados pela memória máxima do servidor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa a API de notificação de memória **QueryMemoryResourceNotification** para determinar quando o Gerenciador de Memória do SQL Server pode alocar e liberar memória.  
  
 E recomendável permitir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] use memória dinamicamente, porém, você pode definir as opções de memória manualmente e restringir a quantidade de memória que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode acessar. Antes de definir a quantidade de memória para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], determine a configuração de memória apropriada subtraindo, da memória física total, a memória necessária para o SO e quaisquer outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (e outros usos do sistema, caso o computador não esteja totalmente dedicado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Essa diferença é a quantidade máxima de memória que você pode atribuir ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
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
 
<sup>1</sup> Consulte o [Guia de arquitetura de gerenciamento de memória](https://docs.microsoft.com/sql/relational-databases/memory-management-architecture-guide#stacksizes) para obter informações sobre os tamanhos de pilha de thread por arquitetura.

<sup>2</sup> Consulte a página da documentação sobre como [Configurar a opção max worker threads de configuração de servidor](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md) para obter informações sobre os threads de trabalho padrão calculados para um determinado número de CPUs de afinidade no host atual.

<sup>3</sup> Consulte a página da documentação em [Opções de inicialização do serviço Mecanismo de Banco de Dados](https://docs.microsoft.com/sql/database-engine/configure-windows/database-engine-service-startup-options?view=sql-server-2014) para obter informações sobre o parâmetro de inicialização *-g*. Aplicável somente para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 32 bits ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] até [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]).

|Tipo de SO|Valores mínimos de memória permitidos para a **memória máxima do servidor**|  
|-------------|----------------------------------------------------------------|  
|32 bits|64 MB|  
|64 bits|128 MB| 

## <a name="how-to-configure-memory-options-using-sql-server-management-studio"></a>Como configurar opções de memória no SQL Server Management Studio  
 Use as duas opções de memória de servidor, **memória mínima do servidor** e **memória máxima do servidor**, para reconfigurar a quantidade de memória (em megabytes) gerenciada pelo Gerenciador de Memória do SQL Server para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode alterar seus requisitos de memória dinamicamente com base nos recursos do sistema disponíveis.  
  
### <a name="procedure-for-configuring-a-fixed-amount-of-memory"></a>Procedimento para configurar uma quantidade fixa de memória  
 **Para definir uma quantidade fixa de memória:**  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Memória** .  
  
3.  Em **Opções de Memória do Servidor**, insira a quantidade desejada para **Memória mínima do servidor** e **Memória máxima do servidor**.  
  
     Use as configurações padrão para permitir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] altere seus requisitos de memória de forma dinâmica com base nos recursos disponíveis do sistema. A configuração padrão de **memória mínima do servidor** é 0 e a configuração padrão de **memória máxima do servidor** é 2147483647 megabytes (MB).  
  
## <a name="maximize-data-throughput-for-network-applications"></a>Maximizar a taxa de transferência de dados para aplicativos de rede  
 Para otimizar o uso de memória do sistema para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], limite a quantidade de memória usada pelo sistema para o cache de arquivo. Para limitar o cache do sistema de arquivos, verifique se a opção **Maximizar taxa de transferência de dados para compartilhamento de arquivos** não está selecionada. É possível especificar o menor cache do sistema de arquivos com a seleção de **Minimizar a memória usada** ou **Equilíbrio**.  
  
#### <a name="to-check-the-current-setting-on-your-operating-system"></a>Para verificar a configuração atual de seu sistema operacional  
  
1.  Clique em **Iniciar**, clique em **Painel de Controle**, clique duas vezes em **Conexões de Rede**e duas vezes em **Conexão de Área Local**.  
  
2.  Na guia **Geral** clique em **Propriedades**, selecione **Redes Microsoft de Compartilhamento de Arquivos e Impressoras**e clique em **Propriedades**.  
  
3.  Se **Maximizar transferência de dados para aplicativos de rede** estiver selecionada, escolha qualquer outra opção, clique em **OK**e feche o restante das caixas de diálogo.  
  
## <a name="lock-pages-in-memory"></a>Bloquear páginas na memória  
 Essa política do Windows determina quais contas podem usar um processo para manter dados na memória física, impedindo o sistema de paginar os dados para a memória virtual em disco. O bloqueio de páginas na memória pode manter a resposta do servidor quando ocorre paginação de memória no disco. A opção SQL Server **bloquear páginas na memória** é definida como on nas instâncias de 32 bits e 64 bits da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard Edition e superior quando a conta com privilégios para executar o sqlservr. exe tiver recebido o direito de usuário "LPIM (páginas bloqueadas na memória)" do Windows. Em versões anteriores do SQL Server, a definição da opção Bloquear Páginas para uma instância de 32 bits do SQL Server requer que a conta com privilégios para executar o sqlservr.exe tenha o direito de usuário LPIM e a opção de configuração 'awe_enabled' seja definida como ON.  
  
 Para desabilitar a opção **bloquear páginas na memória** para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o, remova o direito de usuário "páginas bloqueadas na memória" para a conta de inicialização SQL Server.  
  
### <a name="to-disable-lock-pages-in-memory"></a>Para desabilitar Bloquear Páginas na Memória  
 **Para desabilitar a opção bloquear páginas na memória:**  
  
1.  No menu **Iniciar** , clique em **Executar**. Na caixa **abrir** , digite `gpedit.msc`.  
  
     A caixa de diálogo **Política de Grupo** é aberta.  
  
2.  No console **Política de Grupo** , expanda **Configuração do Computador**e então expanda **Configurações do Windows**.  
  
3.  Expanda **Configurações de Segurança**e então expanda **Políticas Locais**.  
  
4.  Selecione a pasta **Atribuição de direitos de usuários** .  
  
     As políticas serão exibidas no painel de detalhes.  
  
5.  No painel, clique duas vezes em **Bloquear páginas na memória**.  
  
6.  Na caixa de diálogo **Configuração da Política de Segurança Local** , selecione a conta com privilégios para executar o sqlservr.exe e clique em **Remover**.  
  
## <a name="virtual-memory-manager"></a>Gerenciador de Memória Virtual  
 Os sistemas operacionais de 32 bits fornecem acesso a 4 GB de espaço de endereço virtual. Os 2 GB de memória virtual são privativos por processo e estão disponíveis para uso do aplicativo. 2 GB são reservados para uso do sistema operacional. Todas as edições do sistema operacional incluem um comutador que pode fornecer aos aplicativos acesso a até 3 GB de espaço de endereço virtual, com o limite de 1 GB para o sistema operacional. Para obter mais informações sobre como usar a configuração de comutador de memória, consulte a documentação do Windows sobre como ajustar 4 gigabytes (4 GT). Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 32 bits está em execução em um sistema operacional de 64 bits seu espaço de endereço virtual de usuário disponível é de 4 GB completos.  
  
 As regiões confirmadas de espaço de endereço são mapeadas para a memória física disponível pelo VMM (Gerenciador de Memória Virtual) do Windows.  
  
 Para obter mais informações sobre a quantidade de memória física com suporte de diferentes sistemas operacionais, consulte a documentação do Windows "Limites de memória para versões do Windows".  
  
 Os sistemas de memória virtual permitem exceder o uso da memória física, de modo que a taxa entre memória física e virtual pode exceder 1:1. Como resultado, programas maiores podem ser executados em computadores com várias configurações de memória física. No entanto, usar significativamente mais memória virtual do que a média combinada de conjuntos de trabalho de todos os processos pode provocar desempenho inadequado.  
  
 As opções **memória mínima do servidor** e **memória máxima do servidor** são opções avançadas. Se você estiver usando o procedimento armazenado no sistema **sp_configure** para alterar essas configurações, será possível alterá-las apenas quando **show advanced options** estiver definida como 1. Essas configurações entram em vigor imediatamente sem a reinicialização do servidor.  
  
## <a name="running-multiple-instances-of-sql-server"></a>Executando várias instâncias do SQL Server  
 Quando você estiver executando várias instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)], há três métodos que você pode usar para gerenciar a memória:  
  
-   Use **max server memory** para controlar o uso de memória. Defina configurações máximas para cada instância, tomando cuidado para que a permissão total não seja maior que a memória física total de sua máquina. É recomendável que cada instância de memória seja proporcional à sua carga de trabalho ou tamanho de banco de dados esperado. Esse método tem a vantagem de que, quando novos processos ou instância forem iniciados, a memória livre estará disponível para eles imediatamente. A desvantagem é que se você não estiver executando todas as instâncias, nenhuma das instâncias sendo executadas poderá utilizar a memória livre restante.  
  
-   Use **min server memory** para controlar o uso de memória. Defina as configurações mínimas de cada instância, de forma que a soma desses mínimos seja entre 1 a 2 GB menor do que a memória física total de sua máquina. Novamente, você pode definir esses mínimos proporcionalmente à carga esperada para a instância. Esse método tem a vantagem de que, se nem todas as instâncias estiverem sendo executadas ao mesmo tempo, as que estiverem sendo executadas poderão usar a memória livre restante. Esse método também é útil quando há outro processo de uso intensivo da memória no computador, de forma que será assegurado que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenha pelo menos uma quantidade razoável de memória. A desvantagem é que quando uma nova instância (ou qualquer outro processo) for iniciada, pode levar algum tempo para que as instâncias liberem memória, principalmente se for necessário gravar páginas modificadas de volta nos respectivos bancos de dados para fazer isso.  
  
-   Não fazer nada (não recomendado). As primeiras instâncias apresentadas com uma carga de trabalho tenderão a alocar toda a memória. Instâncias inativas ou instâncias iniciadas posteriormente poderão acabar com apenas uma quantidade mínima de memória disponível. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tenta equilibrar o uso de memória em instâncias. No entanto, todas as instâncias responderão aos sinais de Notificação de Memória do Windows para ajustar o tamanho de sua superfície de memória. O Windows não balanceia a memória entre aplicativos com a API de Notificação de Memória. Ele simplesmente fornece um feedback global da disponibilidade da memória no sistema.  
  
 É possível alterar essas configurações sem reinicializar as instâncias, para que você possa testar facilmente para encontrar as melhores configurações para seu padrão de uso.  
  
## <a name="providing-the-maximum-amount-of-memory-to-sql-server"></a>Fornecendo a quantidade máxima de memória para o SQL Server  
  
||32 bits|64 bits|  
|-|-------------|-------------|  
|Memória convencional|Limite máximo do espaço de endereço virtual do processo em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:<br /><br /> 2 GB<br /><br /> 3 GB com parâmetro de inicialização **/3GB** *<br /><br /> 4 GB em WOW64\*\*|Limite máximo do espaço de endereço virtual do processo em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:<br /><br /> 8 TB na arquitetura x64|  
  
 * **/3gb** é um parâmetro de inicialização do sistema operacional. Para obter mais informações, visite a [Biblioteca MSDN](https://go.microsoft.com/fwlink/?LinkID=10257&clcid=0x409).  
  
 \* * O WOW64 (Windows no Windows 64) é um modo em que o 32 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -bit é executado em um sistema operacional de 64 bits. Para obter mais informações, visite a [Biblioteca MSDN](https://go.microsoft.com/fwlink/?LinkID=10257&clcid=0x409).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="example-a"></a>Exemplo A  
 O exemplo a seguir define a opção `max server memory` como 4 GB:  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'max server memory', 4096;  
GO  
RECONFIGURE;  
GO  
```  
  
### <a name="example-b-determining-current-memory-allocation"></a>Exemplo B. Determinando a Alocação de Memória Atual  
 A instrução a seguir retorna informações sobre a memória alocada atualmente.  
  
```  
SELECT  
(physical_memory_in_use_kb/1024) AS Memory_usedby_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,  
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
