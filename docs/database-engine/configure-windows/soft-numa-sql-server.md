---
title: Soft-NUMA (SQL Server) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 11/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- NUMA
- soft-NUMA
helpviewer_keywords:
- NUMA
- non-uniform memory access
- soft-NUMA
ms.assetid: 1af22188-e08b-4c80-a27e-4ae6ed9ff969
caps.latest.revision: 53
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2f57a1d59210a002ebd03b04be4158e514e725cd
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="soft-numa-sql-server"></a>soft-NUMA (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Processadores modernos têm vários núcleos múltiplos por soquete. Cada soquete é representado, em geral, como um único nó NUMA. O mecanismo de banco de dados do SQL Server particiona diversas estruturas internas e particiona threads de serviço para cada nó NUMA.  Com processadores contendo 10 ou mais núcleos por soquete, o uso de software NUMA para dividir nós NUMA de hardware geralmente aumenta a escalabilidade e o desempenho. Antes do SQL Server 2014 SP2, o NUMA baseado em software (soft-NUMA) solicitou que você editasse o Registro para adicionar uma máscara de afinidade de configuração de nó e foi configurada por computador em vez de por cada instância.  Com o SQL Server 2014 SP2 e o SQL Server 2016, o soft-NUMA é configurado automaticamente no nível da instância de banco de dados quando o serviço SQL Server é iniciado.  
  
> [!NOTE]  
>  O soft-NUMA não dá suporte para processadores incluídos a quente.  
  
## <a name="automatic-soft-numa"></a>Soft-NUMA automático  
 Com o SQL Server 2016, sempre que o servidor do mecanismo de banco de dados detecta mais de 8 núcleos físicos para cada nó ou soquete NUMA na inicialização, são criados nós soft-NUMA automaticamente por padrão. Núcleos de processador Hyper-threaded não são diferenciados na contagem de núcleos físicos em um nó.  Quando o número de núcleos físicos detectados é maior que 8 por soquete, o serviço de mecanismo de banco de dados criará nós soft-NUMA idealmente contendo 8 núcleos, mas que poderão ter de 5 a 9 núcleos lógicos por nó. O tamanho do nó de hardware pode limitar-se a uma máscara de afinidade de CPU. Consulte   
            [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md). O número de nós NUMA nunca excederá o número máximo de nós para o qual há suporte.  
  
 Você pode desabilitar ou reabilitar o soft-NUMA usando a instrução [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) com o argumento SET SOFTNUMA. Alterar o valor dessa configuração requer a efetivação da reinicialização do mecanismo de banco de dados.  
  
 A figura a seguir mostra o tipo de informações sobre soft-NUMA que serão exibidas no log de erros do SQL Server quando o SQL Server detectar nós NUMA de hardware com mais de 8 núcleos físicos em cada nó ou soquete.  


``2016-11-14 13:39:43.17 Server      SQL Server detected 2 sockets with 12 cores per socket and 24 logical processors per socket, 48 total logical processors; using 48 logical processors based on SQL Server licensing. This is an informational message; no user action is required.``  
  **``2016-11-14 13:39:43.35 Server      Automatic soft-NUMA was enabled because SQL Server has detected hardware NUMA nodes with greater than 8 physical cores.``**  
  ``2016-11-14 13:39:43.63 Server      Node configuration: node 0: CPU mask: 0x0000000000555555:0 Active CPU mask: 0x0000000000555555:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.``  
  ``2016-11-14 13:39:43.63 Server      Node configuration: node 1: CPU mask: 0x0000000000aaaaaa:0 Active CPU mask: 0x0000000000aaaaaa:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.``  
  ``2016-11-14 13:39:43.63 Server      Node configuration: node 2: CPU mask: 0x0000555555000000:0 Active CPU mask: 0x0000555555000000:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.``  
  ``2016-11-14 13:39:43.63 Server      Node configuration: node 3: CPU mask: 0x0000aaaaaa000000:0 Active CPU mask: 0x0000aaaaaa000000:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.``

  
## <a name="manual-soft-numa"></a>Soft-NUMA manual  
 Para configurar manualmente o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usar o soft-NUMA, desabilitando soft_NUMA automático e editando o Registro para adicionar uma máscara de afinidade de configuração de nó. Ao usar esse método, a máscara do soft-NUMA pode ser declarada como uma entrada de registro binária, DWORD (hexadecimal ou decimal) ou QWORD (hexadecimal ou decimal). Para configurar mais que as primeiras 32 CPUs usam o valor do registro QWORD ou BINARY. (Os valores QWORD não podem ser usados antes de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].) Depois de modificar o Registro, você deve reiniciar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para a configuração do soft-NUMA entrar em vigor.  
  
> [!TIP]
> As CPUs são numeradas a partir de 0.  

> [!WARNING]
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 Considere o exemplo a seguir. Um computador com oito CPUs não tem NUMA de hardware. Três nós soft-NUMA são configurados.   
            A instância A [!INCLUDE[ssDE](../../includes/ssde-md.md)] é configurada para usar as CPUs 0 a 3. Uma segunda instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] está instalada e configurada para usar as CPUs 4 a 7. O exemplo pode ser visualmente representado como:  
  
 `CPUs          0  1  2  3  4  5  6  7`  
  
 `Soft-NUMA   <-N0--><-N1-><----N2---->`  
  
 `SQL Server  <instance A ><instance B>`  
  
 A instância A, que tem E/S significativa, agora tem dois threads de E/S e um thread de gravador lento, enquanto a instância B, que executa operações de processamento intenso, tem apenas um thread de E/S e um thread de gravador lento. Diferentes quantidades de memória podem ser atribuídas às instâncias, mas, ao contrário do NUMA de hardware, ambas recebem memória do mesmo bloco de memória do sistema operacional, e não há afinidade entre memória e processador.  
  
 O thread de gravador lento está vinculado à exibição do sistema operacional SQL dos nós físicos de memória NUMA. Por isso, aquilo que o hardware apresentar como os nós físicos NUMA equivalerá ao número de threads de gravador lento criados. Para obter mais informações, consulte   
            [How It Works: Soft NUMA, I/O Completion Thread, Lazy Writer Workers and Memory Nodes](http://blogs.msdn.com/b/psssql/archive/2010/04/02/how-it-works-soft-numa-i-o-completion-thread-lazy-writer-workers-and-memory-nodes.aspx)(Como funcionam o soft NUMA, o thread de término de E/S, os trabalhadores de gravador lento e os nós de memória).  
  
> [!NOTE]
> As chaves do Registro **Soft-NUMA** não são copiadas quando você atualiza uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="set-the-cpu-affinity-mask"></a>Defina a máscara de afinidade de CPU  
 Execute a instrução a seguir na instância A para configurá-la para usar as CPUs 0, 1, 2 e 3, definindo a máscara de afinidade da CPU:  
  
```  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=0 TO 3;  
```  
  
 Execute a instrução a seguir na instância B para configurá-la para usar as CPUs 4, 5, 6 e 7, definindo a máscara de afinidade da CPU:  
  
```  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=4 TO 7;  
```  
  
### <a name="map-soft-numa-nodes-to-cpus"></a>Mapear nós NUMA de software para CPUs  
 Usando o programa Editor do Registro (regedit.exe), adicione as duas chaves de Registro seguintes para mapear o nó 0 do NUMA de software para as CPUs 0 e 1, o nó 1 do NUMA de software para as CPUs 2 e 3 e o nó 2 do NUMA de software para as CPUs 4, 5, 6 e 7.  
  
> [!TIP]
> Para especificar as CPUs 60 a 63, use um valor QWORD de F000000000000000 ou um valor BINARY de 1111000000000000000000000000000000000000000000000000000000000000.  
  
 No exemplo a seguir, suponha que você tem um servidor DL580 G9, com 18 núcleos por soquete (em 4 soquetes) e cada soquete está em seu próprio grupo K. Uma configuração de soft-numa que você poderia criar seria algo semelhante ao mostrado a seguir. (6 núcleos por nó, 3 nós por grupo, 4 grupos).  
  
|Exemplo para um servidor [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] com vários Grupos K|Tipo|Nome do valor|Dados do valor|  
|-----------------------------------------------------------------------------------------------------------------|----------|----------------|----------------|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node0|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node0|DWORD|Agrupar|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node1|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node1|DWORD|Agrupar|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node2|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node2|DWORD|Agrupar|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node3|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node3|DWORD|Agrupar|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node4|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node4|DWORD|Agrupar|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node5|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node5|DWORD|Agrupar|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node6|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node6|DWORD|Agrupar|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node7|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node7|DWORD|Agrupar|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node8|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node8|DWORD|Agrupar|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node9|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node9|DWORD|Agrupar|3|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node10|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node10|DWORD|Agrupar|3|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node11|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node11|DWORD|Agrupar|3|  
  
## <a name="metadata"></a>Metadados  
 Você pode usar os DMVs a seguir para exibir o estado atual e a configuração do soft_NUMA.  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md): exibe o valor atual (0 ou 1) para SOFTNUMA  
  
-   [sys.dm_os_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-nodes-transact-sql.md): a coluna de node_state_desc para cada nó NUMA mostrará se o nó foi ou não criado pelo soft-NUMA.  
  
-   [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md): as colunas softnuma e softnuma_desc mostrarão os valores de configuração.  
  
> [!NOTE]
> Embora seja possível exibir o valor de execução para o soft-NUMA automático usando [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md), não é possível alterar seu valor usando **sp_configure**. É necessário usar a declaração [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) com o argumento SET SOFTNUMA.  
  
## <a name="see-also"></a>Consulte também  
 [Mapear portas TCP/IP para nós NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/map-tcp-ip-ports-to-numa-nodes-sql-server.md)   
 [Opção máscara de afinidade de configuração de servidor](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)  
  
  


