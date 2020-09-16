---
title: Soft-NUMA (SQL Server) | Microsoft Docs
description: Saiba mais sobre o soft-NUMA no SQL Server 2014 SP2 e versões mais recentes. Veja como usar o soft-NUMA automático e como configurar manualmente o SQL Server para usar o soft-NUMA.
ms.custom: ''
ms.date: 02/13/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- NUMA
- soft-NUMA
helpviewer_keywords:
- NUMA
- non-uniform memory access
- soft-NUMA
ms.assetid: 1af22188-e08b-4c80-a27e-4ae6ed9ff969
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e2674f1453242e6f9b580ff41524254a10896f76
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538018"
---
# <a name="soft-numa-sql-server"></a>soft-NUMA (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Os processadores modernos têm vários núcleos por soquete. Cada soquete é representado, em geral, como um único nó NUMA. O mecanismo de banco de dados do SQL Server particiona diversas estruturas internas e particiona threads de serviço para cada nó NUMA.  Com processadores contendo 10 ou mais núcleos por soquete, o uso de software NUMA para dividir nós NUMA de hardware geralmente aumenta a escalabilidade e o desempenho. Antes do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2, o soft-NUMA (NUMA baseado em software) exigia a edição do Registro para adicionar uma máscara de afinidade de configuração de nó e era configurado no nível do host e não por instância. Desde o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 e o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o soft-NUMA passou a ser configurado automaticamente no nível da instância do banco de dados quando o serviço [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] é iniciado.  
  
> [!NOTE]  
> O soft-NUMA não dá suporte para processadores incluídos a quente.  
  
## <a name="automatic-soft-numa"></a>Soft-NUMA automático  
Com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], sempre que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] detectar mais de oito núcleos por nó NUMA ou soquete na inicialização, os nós soft-NUMA serão criados automaticamente por padrão. Núcleos de processador Hyper-threaded não são diferenciados na contagem de núcleos físicos em um nó.  Quando o número detectado de núcleos físicos for mais de oito por soquete, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] criará nós soft-NUMA contendo o ideal de 8 núcleos, podendo reduzir para cinco ou aumentar para nove núcleos lógicos por nó. O tamanho do nó de hardware pode limitar-se a uma máscara de afinidade de CPU. O número de nós NUMA nunca excede o número máximo de nós NUMA permitidos.  
  
Você pode desabilitar ou reabilitar o soft-NUMA usando a instrução [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) com o argumento `SET SOFTNUMA`. Alterar o valor dessa configuração requer a efetivação da reinicialização do mecanismo de banco de dados.  
  
A figura a seguir mostra o tipo de informações sobre o soft-NUMA que aparece no log de erros do SQL Server, quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detecta nós NUMA com mais de oito núcleos físicos para cada nó ou soquete.  


```
2016-11-14 13:39:43.17 Server      SQL Server detected 2 sockets with 12 cores per socket and 24 logical processors per socket, 48 total logical processors; using 48 logical processors based on SQL Server licensing. This is an informational message; no user action is required.     
2016-11-14 13:39:43.35 Server      Automatic soft-NUMA was enabled because SQL Server has detected hardware NUMA nodes with greater than 8 physical cores.     
2016-11-14 13:39:43.63 Server      Node configuration: node 0: CPU mask: 0x0000000000555555:0 Active CPU mask: 0x0000000000555555:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.    
2016-11-14 13:39:43.63 Server      Node configuration: node 1: CPU mask: 0x0000000000aaaaaa:0 Active CPU mask: 0x0000000000aaaaaa:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.    
2016-11-14 13:39:43.63 Server      Node configuration: node 2: CPU mask: 0x0000555555000000:0 Active CPU mask: 0x0000555555000000:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.     
2016-11-14 13:39:43.63 Server      Node configuration: node 3: CPU mask: 0x0000aaaaaa000000:0 Active CPU mask: 0x0000aaaaaa000000:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.   
```   

> [!NOTE]
> Do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 em diante, use o sinalizador de rastreamento 8079 para permitir que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] use Soft-NUMA automático. Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], esse comportamento é controlado pelo mecanismo e o sinalizador de rastreamento 8079 não tem nenhum efeito. Para obter mais informações, veja [DBCC TRACEON – sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).

## <a name="manual-soft-numa"></a>Soft-NUMA manual  
Para configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manualmente para usar o soft-NUMA, desabilite o soft-NUMA automático e edite o Registro para adicionar uma máscara de afinidade de configuração de nó. Ao usar esse método, a máscara do soft-NUMA pode ser declarada como uma entrada de registro binária, DWORD (hexadecimal ou decimal) ou QWORD (hexadecimal ou decimal). Para configurar mais que as primeiras 32 CPUs, use os valores do Registro QWORD ou BINARY (os valores QWORD não podem ser usados antes do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]). Depois de modificar o Registro, você precisará reiniciar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para que a configuração do soft-NUMA entre em vigor.  
  
> [!TIP]
> As CPUs são numeradas a partir de 0.  

> [!WARNING]
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
Considere o exemplo de um computador com oito CPUs, que não tem NUMA de hardware. Três nós soft-NUMA são configurados.   
A instância A [!INCLUDE[ssDE](../../includes/ssde-md.md)] é configurada para usar as CPUs 0 a 3. Uma segunda instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] está instalada e configurada para usar as CPUs 4 a 7. O exemplo pode ser visualmente representado como:  
  
 `CPUs          0  1  2  3  4  5  6  7`  
  
 `Soft-NUMA   <-N0--><-N1-><----N2---->`  
  
 `SQL Server  <instance A ><instance B>`  
  
 A instância A, que apresenta E/S significativa, agora tem dois threads de E/S e um thread de gravador lento. A instância B, que executa operações de processamento intenso, tem apenas um thread de E/S e um thread de gravador lento. Diferentes quantidades de memória podem ser atribuídas às instâncias, mas ao contrário do NUMA de hardware, ambas recebem memória do mesmo bloco de memória do sistema operacional e não há nenhuma afinidade do processador com a memória.  
  
 O thread de gravador lento é vinculado à exibição do SQLOS dos nós de memória NUMA físicos. Por isso, aquilo que o hardware apresentar como os nós NUMA físicos equivalerá ao número de threads de gravador lento criados. Para obter mais informações, confira [Como funciona: Como funcionam o soft NUMA, o thread de término de E/S, os trabalhadores de gravador lento e os nós de memória](https://techcommunity.microsoft.com/t5/sql-server-support/how-it-works-soft-numa-i-o-completion-thread-lazy-writer-workers/ba-p/316044).  
  
> [!NOTE]
> As chaves do Registro **Soft-NUMA** não são copiadas quando você atualiza uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="set-the-cpu-affinity-mask"></a>Defina a máscara de afinidade de CPU  
 Execute a instrução a seguir na instância A para configurá-la para usar as CPUs 0, 1, 2 e 3, definindo a máscara de afinidade da CPU:  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=0 TO 3;  
```  
  
Execute a instrução a seguir na instância B para configurá-la para usar as CPUs 4, 5, 6 e 7, definindo a máscara de afinidade da CPU:  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=4 TO 7;  
```  
  
### <a name="map-soft-numa-nodes-to-cpus"></a>Mapear nós NUMA de software para CPUs  
 Usando o programa Editor do Registro (regedit.exe), adicione as duas chaves do Registro seguintes para mapear o nó soft-NUMA 0 às CPUs 0 e 1, o nó soft-NUMA 1 para as CPUs 2 e 3 e o nó soft-NUMA 2 para as CPUs 4, 5, 6 e 7.  
  
> [!TIP]
> Para especificar as CPUs 60 a 63, use um valor QWORD de F000000000000000 ou um valor BINARY de 1111000000000000000000000000000000000000000000000000000000000000.  
  
 No exemplo a seguir, suponha que você tenha um servidor DL580 G9, com 18 núcleos por soquete (em 4 soquetes) e cada soquete esteja em seu próprio grupo K. Uma configuração de soft-NUMA que você poderia criar seria algo semelhante a isto: seis núcleos por nó, três nós por grupo, quatro grupos.  
  
|Exemplo para um servidor [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] com vários Grupos K|Type|Nome do valor|Dados do valor|  
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
 Você pode usar as DMVs a seguir para exibir o estado e a configuração atuais do soft-NUMA.  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md): exibe o valor atual (0 ou 1) para SOFTNUMA  
  
-   [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md): As colunas *softnuma_configuration* e *softnuma_configuration_desc* exibem os valores de configuração atuais.  
  
> [!NOTE]
> Embora seja possível exibir o valor de execução para o soft-NUMA automático usando [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md), não é possível alterar seu valor usando **sp_configure**. Você deve usar a instrução [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) com o argumento `SET SOFTNUMA`.  
  
## <a name="see-also"></a>Consulte Também  
[Mapear portas TCP/IP para nós NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/map-tcp-ip-ports-to-numa-nodes-sql-server.md)    
[Opção affinity mask de configuração de servidor](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)    
[ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)     
[sys.dm_os_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-nodes-transact-sql.md)   
  
