---
title: Resolver problemas de memória insuficiente | Microsoft Docs
ms.custom: ''
ms.date: 12/21/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f855e931-7502-44bd-8a8b-b8543645c7f4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1b0c54bf494055567e7a8c8fc59fe001ac843cfa
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51671677"
---
# <a name="resolve-out-of-memory-issues"></a>Resolver problemas de memória insuficiente
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[hek_1](../../includes/hek-1-md.md)] usa mais memória e de maneiras diferentes que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. É possível que a quantidade de memória que você instalou e atribuiu para o [!INCLUDE[hek_2](../../includes/hek-2-md.md)] torne-se inadequada para suas necessidades de crescimento. Se for o caso, você pode ficar sem memória. Este tópico aborda como se recuperar de uma situação de OOM. Veja [Monitorar e solucionar problemas de uso da memória](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md) para obter diretrizes que podem ajudá-lo a evitar várias situações de OOM.  
  
## <a name="covered-in-this-topic"></a>Tópicos abordados  
  
|Tópico|Visão geral|  
|-----------|--------------|  
|[Resolver falhas de restauração de banco de dados devido a OOM](#bkmk_resolveRecoveryFailures)|O que fazer se você receber a mensagem de erro “Falha na operação de restauração do banco de dados '*\<databaseName>*' devido à memória insuficiente no pool de recursos '*\<resourcePoolName>*'”.|  
|[Resolver o impacto de pouca memória ou condições de OOM na carga de trabalho](#bkmk_recoverFromOOM)|O que fazer se você desconfiar que os problemas de pouca memória estão comprometendo o desempenho.|  
|[Resolver falhas de alocação de página devido à memória insuficiente quando há memória suficiente disponível](#bkmk_PageAllocFailure)|O que fazer se você receber a mensagem de erro “Desautorizando as alocações de página do banco de dados '*\<databaseName>*' devido à memória insuficiente no pool de recursos '*\<resourcePoolName>*'”. …” quando a memória disponível é suficiente para a operação.|
|[Práticas recomendadas ao usar o OLTP in-memory em um ambiente de VM](#bkmk_VMs)|O que deve ser levado em consideração ao usar o OLTP in-memory em um ambiente virtualizado.|
  
##  <a name="bkmk_resolveRecoveryFailures"></a> Resolver falhas de restauração de banco de dados devido a OOM  
 Quando tenta restaurar um banco de dados, você pode receber a mensagem de erro: “Falha na operação de restauração do banco de dados '*\<databaseName>*' devido à memória insuficiente no pool de recursos '*\<resourcePoolName>*'”. Isso indica que o servidor não tem memória suficiente disponível para restaurar o banco de dados. 
   
O servidor restaurado em um banco de dados deve ter memória suficiente disponível para as tabelas com otimização de memória no backup de banco de dados; caso contrário, o banco de dados não será colocado online e será marcado como suspeito.  
  
Se o servidor tiver memória física suficiente, mas você ainda estiver vendo este erro, é possível que outros processos estejam usando uma quantidade excessiva de memória ou um problema de configuração faz com que não haja memória suficiente disponível para a restauração. Para esta classe de problemas, use as seguintes medidas para disponibilizar mais memória para a operação de restauração: 
  
-   Feche temporariamente os aplicativos em execução.   
    Ao fechar um ou mais aplicativos em execução ou interromper serviços desnecessários no momento, você disponibiliza a memória que eles estavam usando para a operação de restauração. Você poderá reiniciá-los após a restauração bem-sucedida.  
  
-   Aumente o valor de MAX_MEMORY_PERCENT.   
    Se o banco de dados for [associado a um pool de recursos](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md), o que é uma prática recomendada, a memória disponível para a restauração será controlada por MAX_MEMORY_PERCENT. Se o valor for muito baixo, a restauração falhará. Este snippet de código altera MAX_MEMORY_PERCENT para o pool de recursos PoolHk para 70% de memória instalada.  
  
    > [!IMPORTANT]  
    > Se o servidor estiver sendo executado em uma máquina virtual e não for dedicado, defina o valor de MIN_MEMORY_PERCENT para o mesmo valor de MAX_MEMORY_PERCENT.   
    > Confira o tópico [Práticas recomendadas ao usar o OLTP in-memory em um ambiente de VM](#bkmk_VMs) para obter mais informações.  
  
    ```sql  
    -- disable resource governor  
    ALTER RESOURCE GOVERNOR DISABLE  
  
    -- change the value of MAX_MEMORY_PERCENT  
    ALTER RESOURCE POOL PoolHk  
    WITH  
         ( MAX_MEMORY_PERCENT = 70 )  
    GO  
  
    -- reconfigure the Resource Governor  
    --    RECONFIGURE enables resource governor  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
  
    ```  
  
     Para obter informações sobre os valores máximos para MAX_MEMORY_PERCENT, confira a seção do tópico [Percentual de memória disponível para índices e tabelas com otimização de memória](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable).  
  
-   Aumente **max server memory**.  
    Para obter informações sobre como configurar a opção **max server memory**, consulte o tópico [Opções de configuração de servidor Server Memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md).  
  
##  <a name="bkmk_recoverFromOOM"></a> Resolver o impacto de pouca memória ou condições de OOM na carga de trabalho  
 Obviamente, é melhor não ficar com pouca memória ou na situação de OOM (memória insuficiente). Um bom planejamento e monitoramento pode ajudar a evitar situações de OOM. Ainda assim, o melhor planejamento nem sempre prevê o que realmente acontece e você pode acabar com pouca memória ou OOM. Há duas etapas para a recuperação de OOM:  
  
1.  [Abrir uma DAC (Conexão de Administrador Dedicada)](#bkmk_openDAC)  
  
2.  [Realizar a ação corretiva](#bkmk_takeCorrectiveAction)  
  
###  <a name="bkmk_openDAC"></a> Abrir uma DAC (Conexão de Administrador Dedicada)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece uma DAC (conexão de administrador dedicada). A DAC permite que um administrador acesse uma instância em execução do Mecanismo de Banco de Dados do SQL Server para resolver problemas no servidor, mesmo quando o servidor não está respondendo às conexões de outro cliente. O DAC é disponibilizado pelo utilitário `sqlcmd` e [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Para obter orientações sobre como usar o DAC por meio do SSMS ou do `sqlcmd`, consulte [Conexão de diagnóstico para administradores de banco de dados](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md).  
  
###  <a name="bkmk_takeCorrectiveAction"></a> Realizar a ação corretiva  
 Para resolver a sua condição de OOM, você precisa ou liberar memória existente reduzindo o uso ou disponibilizar mais memória para as tabelas de memória.  
  
#### <a name="free-up-existing-memory"></a>Liberar memória existente  
  
##### <a name="delete-non-essential-memory-optimized-table-rows-and-wait-for-garbage-collection"></a>Excluir linhas não essenciais da tabela com otimização de memória e aguardar a coleta de lixo  
 Você pode remover as linhas não essenciais de uma tabela com otimização de memória. O coletor de lixo retorna a memória usada por essas linhas para a memória disponível. O mecanismo de OLTP na memória coleta linhas de lixo de maneira agressiva. No entanto, uma transação demorada poderá evitar a coleta de lixo. Por exemplo, se você tiver uma transação que é executada durante 5 minutos, todas as versões de linha criadas por causa das operações de atualização/exclusão enquanto a transação estava ativa não poderão ser limpas.  
  
##### <a name="move-one-or-more-rows-to-a-disk-based-table"></a>Mover uma ou mais linhas a uma tabela baseada em disco  
 Os seguintes artigos da TechNet fornecem orientação sobre como mover linhas de uma tabela com otimização de memória para uma tabela baseada em disco.  
  
-   [Particionamento de nível de aplicativo](../../relational-databases/in-memory-oltp/application-level-partitioning.md)  
  
-   [Padrão de aplicativo para particionamento de tabelas com otimização de memória](../../relational-databases/in-memory-oltp/application-pattern-for-partitioning-memory-optimized-tables.md)  
  
#### <a name="increase-available-memory"></a>Aumentar a memória disponível  
  
##### <a name="increase-value-of-maxmemorypercent-on-the-resource-pool"></a>Aumentar o valor de MAX_MEMORY_PERCENT no pool de recursos  
 Se você não criou um pool de recursos nomeado para as tabelas de memória, deverá fazer isso e associar seus bancos de dados do [!INCLUDE[hek_2](../../includes/hek-2-md.md)] a ele. Confira o tópico [Associar um banco de dados com tabelas com otimização de memória a um pool de recursos](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md) para obter diretrizes sobre como criar e associar bancos de dados do [!INCLUDE[hek_2](../../includes/hek-2-md.md)] a um pool de recursos.  
  
 Se seu banco de dados do [!INCLUDE[hek_2](../../includes/hek-2-md.md)] estiver associado a um pool de recursos, você poderá aumentar a porcentagem de memória que o pool pode acessar. Confira o subtópico [Alterar MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT em um pool existente](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation) para obter diretrizes sobre como alterar o valor de MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT em um pool de recursos.  
  
 Aumente o valor de MAX_MEMORY_PERCENT.   
Este snippet de código altera MAX_MEMORY_PERCENT para o pool de recursos PoolHk para 70% de memória instalada.  
  
> [!IMPORTANT]  
>  Se o servidor estiver sendo executado em uma máquina virtual e não for dedicado, defina o valor de MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT como o mesmo.   
> Confira o tópico [Práticas recomendadas ao usar o OLTP in-memory em um ambiente de VM](#bkmk_VMs) para obter mais informações.  
  
```sql  
-- disable resource governor  
ALTER RESOURCE GOVERNOR DISABLE  
  
-- change the value of MAX_MEMORY_PERCENT  
ALTER RESOURCE POOL PoolHk  
WITH  
     ( MAX_MEMORY_PERCENT = 70 )  
GO  
  
-- reconfigure the Resource Governor to enabled it
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
```  
  
 Para obter informações sobre os valores máximos para MAX_MEMORY_PERCENT, confira a seção do tópico [Percentual de memória disponível para índices e tabelas com otimização de memória](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable).  
  
##### <a name="install-additional-memory"></a>Instalar a memória adicional  
 Por fim, a melhor solução, se possível, é instalar mais memória física. Se você fizer isso, lembre-se de que provavelmente também poderá aumentar o valor de MAX_MEMORY_PERCENT (confira o subtópico [Alterar MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT em um pool existente](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation)), já que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] talvez não precise de mais memória, permitindo assim que você disponibilize a maior parte da memória recém-instalada, se não toda ela, ao pool de recursos.  
  
> [!IMPORTANT]  
>  Se o servidor estiver sendo executado em uma máquina virtual e não for dedicado, defina o valor de MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT como o mesmo.   
> Confira o tópico [Práticas recomendadas ao usar o OLTP in-memory em um ambiente de VM](#bkmk_VMs) para obter mais informações.  
  
##  <a name="bkmk_PageAllocFailure"></a> Resolver falhas de alocação de página devido à memória insuficiente quando há memória suficiente disponível  
 Se você receber a mensagem de erro `Disallowing page allocations for database '*\<databaseName>*' due to insufficient memory in the resource pool '*\<resourcePoolName>*'. See 'https://go.microsoft.com/fwlink/?LinkId=330673' for more information.` no log de erros quando a memória física disponível for suficiente para alocar a página, talvez isso ocorra porque um Administrador de Recursos está desabilitado. Quando o Administrador de Recursos é desabilitado, MEMORYBROKER_FOR_RESERVE induz artificial à pressão de memória artificial.  
  
 Para resolver isso, é necessário habilitar o Administrador de Recursos.  
  
 Veja [Habilitar Administrador de Recursos](../../relational-databases/resource-governor/enable-resource-governor.md) para obter informações sobre limites e restrições, bem como diretrizes sobre como habilitar o Administrador de Recursos usando o Pesquisador de Objetos, as propriedades do Administrador de Recursos ou o Transact-SQL.  
 
## <a name="bkmk_VMs"></a> Práticas recomendadas ao usar o OLTP in-memory em um ambiente de VM
A virtualização do servidor pode ajudá-lo a diminuir os custos operacionais e de capital com a TI, e atingir uma maior eficiência de TI com processos de provisionamento de aplicativo, manutenção, disponibilidade e backup/recuperação aprimorados. Com os avanços tecnológicos recentes, as cargas de trabalho de banco de dados complexas podem mais ser prontamente consolidadas usando a virtualização. Este tópico abrange as práticas recomendadas para usar o OLTP in-memory do SQL Server em um ambiente virtualizado.

### <a name="memory-pre-allocation"></a>Pré-alocação de memória
Para a memória em um ambiente virtualizado, o melhor desempenho e o suporte aprimorado são considerações essenciais. Você deve ser capaz de alocar memória rapidamente para máquinas virtuais dependendo de seus requisitos (cargas de pico e fora de pico) e garantir que a memória não seja desperdiçada. O recurso de Memória Dinâmica do Hyper-V aumenta a agilidade sobre como a memória é alocada e gerenciada entre as máquinas virtuais executadas em um host.

Algumas práticas recomendadas para virtualizar e gerenciar o SQL Server precisam ser modificadas ao virtualizar um banco de dados que tenha tabelas com otimização de memória. Sem tabelas com otimização de memória, duas das práticas recomendadas são:
-  Se você usar a opção min server memory, será melhor atribuir somente a quantidade de memória necessária para que uma parcela suficiente de memória permaneça em outros processos (impedindo a paginação).
-  Não defina o valor de pré-alocação de memória muito alto. Caso contrário, outros processos podem não obter memória suficiente no momento em que a exigirem e isso pode levar à paginação de memória.

Se você seguir as práticas acima para um banco de dados com tabelas otimizadas pela memória, uma tentativa de restaurar e recuperar um banco de dados poderá resultar no banco de dados ficando em um estado de "Recuperação Pendente", mesmo se você tiver memória suficiente para recuperá-lo. A razão para isso é que, ao iniciar, o OLTP in-memory traz os dados para a memória de maneira mais agressiva do que a alocação de memória dinâmica faz ao alocar a memória no banco de dados.

### <a name="resolution"></a>Resolução
Para solucionar isso, pré-aloque memória suficiente para o banco de dados a ser recuperado ou reinicie o banco de dados, não um valor mínimo que depende da memória dinâmica para fornecer a memória adicional quando for necessário.
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciando memória para OLTP na memória](https://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)   
 [Monitorar e solucionar problemas de uso da memória](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)   
 [Associar um banco de dados com tabelas com otimização de memória a um pool de recursos](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [Guia de arquitetura de gerenciamento de memória](../../relational-databases/memory-management-architecture-guide.md)  
 [Opções Server Memory de configuração do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md) 
  
