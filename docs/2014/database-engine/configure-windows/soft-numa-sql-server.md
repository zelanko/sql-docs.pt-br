---
title: Configurar o SQL Server para usar o Soft-NUMA (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- NUMA
- non-uniform memory access
ms.assetid: 1af22188-e08b-4c80-a27e-4ae6ed9ff969
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6ad0e30c0db83daf7e0cae4f7353d1f0a96a96d9
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59953822"
---
# <a name="configure-sql-server-to-use-soft-numa-sql-server"></a>Configurar o SQL Server para usar o NUMA de software (SQL Server)
Processadores modernos têm vários núcleos múltiplos por soquete. Cada soquete é representado, em geral, como um único nó NUMA. O mecanismo de banco de dados do SQL Server particiona diversas estruturas internas e particiona threads de serviço para cada nó NUMA. Com processadores contendo 10 ou mais núcleos por soquete, o uso do software NUMA (soft-NUMA) para dividir nós de hardware geralmente aumenta a escalabilidade e desempenho.   

> [!NOTE]
> O soft-NUMA não dá suporte para processadores incluídos a quente.
  
## <a name="automatic-soft-numa"></a>Soft-NUMA automático
Nós soft-NUMA começando com o SQL Server 2014 Service Pack 2, sempre que o servidor do mecanismo de banco de dados detecta mais de 8 processadores físicos na inicialização, são criados automaticamente se o sinalizador de rastreamento 8079 é habilitado como um parâmetro de inicialização. Núcleos de processador Hyper-threaded não são considerados na contagem de processadores físicos. Quando o número de processadores físicos detectados é maior que 8 por soquete, o serviço de mecanismo de banco de dados criará nós soft-NUMA idealmente contenham 8 núcleos, mas podem descer até 5 ou até 9 processadores lógicos por nó. O tamanho do nó de hardware pode limitar-se a uma máscara de afinidade de CPU. O número de nós NUMA nunca excederá o número máximo de nós para o qual há suporte.

Sem o sinalizador de rastreamento, o soft-NUMA é desabilitada por padrão. Você pode habilitar o soft-NUMA usando o sinalizador de rastreamento 8079. Alterar o valor dessa configuração requer a efetivação da reinicialização do mecanismo de banco de dados.

A figura a seguir mostra o tipo de informações sobre soft-NUMA que serão vistos no log de erros do SQL Server quando o SQL Server detectar nós de hardware com mais de 8 processadores lógicos e se o sinalizador de rastreamento 8079 é habilitado.

![Soft-NUMA](./media/soft-numa-sql-server/soft-numa.PNG)

> [!NOTE]
> Começando com o SQL Server 2016, esse comportamento é controlado pelo mecanismo e rastreamento 8079 o sinalizador não tem nenhum efeito.

## <a name="manual-soft-numa"></a>Soft-NUMA manual
  
Para configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usar o soft-NUMA manualmente, você deve editar o registro para adicionar uma máscara de afinidade de configuração de nó. A máscara do NUMA de software pode ser declarada como uma entrada de registro binária, DWORD (hexadecimal ou decimal) ou QWORD (hexadecimal ou decimal). Para configurar mais que as primeiras 32 CPUs usam o valor do registro QWORD ou BINARY. (Os valores QWORD não podem ser usados antes de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].) Você deve reiniciar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para configurar o soft-NUMA.  
  
> [!TIP]  
>  As CPUs são numeradas a partir de 0.  
  
 [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 Considere o exemplo a seguir. Um computador com oito CPUs não tem NUMA de hardware. Três nós soft-NUMA são configurados. A instância A [!INCLUDE[ssDE](../../includes/ssde-md.md)] é configurada para usar as CPUs 0 a 3. Uma segunda instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] está instalada e configurada para usar as CPUs 4 a 7. O exemplo pode ser visualmente representado como:  
  
 `CPUs          0  1  2  3  4  5  6  7`  
  
 `Soft-NUMA   <-N0--><-N1-><----N2---->`  
  
 `SQL Server  <instance A ><instance B>`  
  
 A instância A, que tem E/S significativa, agora tem dois threads de E/S e um thread de gravador lento, enquanto a instância B, que executa operações de processamento intenso, tem apenas um thread de E/S e um thread de gravador lento. Diferentes quantidades de memória podem ser atribuídas às instâncias, mas, ao contrário do NUMA de hardware, ambas recebem memória do mesmo bloco de memória do sistema operacional, e não há afinidade entre memória e processador.  
  
 O thread de gravador lento está vinculado à exibição do sistema operacional SQL dos nós físicos de memória NUMA. Por isso, aquilo que o hardware apresentar como os nós físicos NUMA equivalerá ao número de threads de gravador lento criados. Para obter mais informações, confira [Como funciona: Soft-NUMA, o Thread de conclusão de e/s, trabalhadores de gravador lento e nós de memória](https://blogs.msdn.com/b/psssql/archive/2010/04/02/how-it-works-soft-numa-i-o-completion-thread-lazy-writer-workers-and-memory-nodes.aspx).  
  
> [!NOTE]  
>  As chaves do Registro **Soft-NUMA** não são copiadas quando você atualiza uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="set-the-cpu-affinity-mask"></a>Defina a máscara de afinidade de CPU  
  
1.  Execute a instrução a seguir na instância A para configurá-la para usar as CPUs 0, 1, 2 e 3, definindo a máscara de afinidade da CPU:  
  
    ```  
    ALTER SERVER CONFIGURATION   
    SET PROCESS AFFINITY CPU=0 TO 3;  
    ```  
  
2.  Execute a instrução a seguir na instância B para configurá-la para usar as CPUs 4, 5, 6 e 7, definindo a máscara de afinidade da CPU:  
  
    ```  
    ALTER SERVER CONFIGURATION   
    SET PROCESS AFFINITY CPU=4 TO 7;  
    ```  
  
### <a name="map-soft-numa-nodes-to-cpus"></a>Mapear nós NUMA de software para CPUs  
  
-   Usando o programa Editor do Registro (regedit.exe), adicione as duas chaves de Registro seguintes para mapear o nó 0 do NUMA de software para as CPUs 0 e 1, o nó 1 do NUMA de software para as CPUs 2 e 3 e o nó 2 do NUMA de software para as CPUs 4, 5, 6 e 7.  
  
     No exemplo a seguir, suponha que você tem um servidor DL580 G9, com 18 núcleos por soquete (em 4 soquetes) e cada soquete está em seu próprio grupo K. Uma configuração de soft-numa que você poderia criar seria algo semelhante ao mostrado a seguir. (6 núcleos por nó, 3 nós por grupo, 4 grupos).  
  
    |Exemplo para um servidor [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] com vários Grupos K|Tipo|Nome do valor|Dados do valor|  
    |------------------------------------------------------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node3|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node3|DWORD|Grupo|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node4|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node4|DWORD|Grupo|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node5|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node5|DWORD|Grupo|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node6|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node6|DWORD|Grupo|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node7|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node7|DWORD|Grupo|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node8|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node8|DWORD|Grupo|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node9|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node9|DWORD|Grupo|3|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node10|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node10|DWORD|Grupo|3|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node11|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node11|DWORD|Grupo|3|  
  
     Exemplos adicionais:  
  
    |[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Tipo|Nome do valor|Dados do valor|  
    |---------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|Grupo|0|  
  
    > [!TIP]  
    >  Para especificar as CPUs 60 a 63, use um valor QWORD de F000000000000000 ou um valor BINARY de 1111000000000000000000000000000000000000000000000000000000000000.  
  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|Tipo|Nome do valor|Dados do valor|  
    |---------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node0|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node1|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node2|DWORD|Grupo|0|  
  
    |SQL Server 2008 R2|Tipo|Nome do valor|Dados do valor|  
    |------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|Grupo|0|  
  
    |SQL Server 2008|Tipo|Nome do valor|Dados do valor|  
    |---------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
  
    |SQL Server 2005|Tipo|Nome do valor|Dados do valor|  
    |---------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
  
## <a name="see-also"></a>Consulte também  
 [Mapear portas TCP/IP para nós NUMA &#40;SQL Server&#41;](map-tcp-ip-ports-to-numa-nodes-sql-server.md)   
 [Opção máscara de afinidade de configuração de servidor](affinity-mask-server-configuration-option.md)   
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)  
  
  
