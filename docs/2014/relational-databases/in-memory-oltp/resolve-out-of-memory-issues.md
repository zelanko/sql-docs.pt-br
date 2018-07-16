---
title: Resolver problemas de memória insuficiente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f855e931-7502-44bd-8a8b-b8543645c7f4
caps.latest.revision: 15
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 2e866c2899ff4172e969cba97e4b10f1ce0fac3a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37253978"
---
# <a name="resolve-out-of-memory-issues"></a>Resolver problemas de memória insuficiente
  [!INCLUDE[hek_1](../../includes/hek-1-md.md)] usa mais memória e de maneiras diferentes que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. É possível que a quantidade de memória que você instalou e atribuiu para o [!INCLUDE[hek_2](../../includes/hek-2-md.md)] torne-se inadequada para suas necessidades de crescimento. Se for o caso, você pode ficar sem memória. Este tópico aborda como se recuperar de uma situação de OOM. Veja [Monitorar e solucionar problemas de uso da memória](monitor-and-troubleshoot-memory-usage.md) para obter diretrizes que podem ajudá-lo a evitar várias situações de OOM.  
  
## <a name="covered-in-this-topic"></a>Tópicos abordados  
  
|Tópico|Visão geral|  
|-----------|--------------|  
|[Resolver falhas de restauração de banco de dados devido a OOM](resolve-out-of-memory-issues.md#bkmk_resolverecoveryfailures)|O que fazer se você receber a mensagem de erro “Falha na operação de restauração do banco de dados '*\<databaseName>*' devido à memória insuficiente no pool de recursos '*\<resourcePoolName>*'”.|  
|[Resolver o impacto de pouca memória ou condições de OOM na carga de trabalho](resolve-out-of-memory-issues.md#bkmk_recoverfromoom)|O que fazer se você desconfiar que os problemas de pouca memória estão comprometendo o desempenho.|  
|[Resolver falhas de alocação de página devido à memória insuficiente quando há memória suficiente disponível](resolve-out-of-memory-issues.md#bkmk_pageallocfailure)|O que fazer se você receber a mensagem de erro “Desautorizando as alocações de página do banco de dados '*\<databaseName>*' devido à memória insuficiente no pool de recursos '*\<resourcePoolName>*'”. …” quando a memória disponível é suficiente para a operação.|  
  
##  <a name="bkmk_resolveRecoveryFailures"></a> Resolver falhas de restauração de banco de dados devido a OOM  
 Quando tenta restaurar um banco de dados, você pode receber a mensagem de erro: “Falha na operação de restauração do banco de dados '*\<databaseName>*' devido à memória insuficiente no pool de recursos '*\<resourcePoolName>*'”. Antes de restaurar com êxito o banco de dados, você deve resolver o problema de memória insuficiente disponibilizando mais memória.  
  
 Para resolver a falha de recuperação devido a OOM, aumente a memória disponível usando qualquer ou todos esses meios para aumentar temporariamente a memória disponível para a operação de recuperação.  
  
-   Feche temporariamente os aplicativos em execução.   
    Ao fechar um ou mais aplicativos em execução, como Visual Studio, Internet Explorer, OneNote e outros, você disponibiliza a memória que eles estavam usando para a operação de restauração. Você poderá reiniciá-los após a restauração bem-sucedida.  
  
-   Aumente o valor de MAX_MEMORY_PERCENT.   
    Este trecho de código altera MAX_MEMORY_PERCENT para o pool de recursos PoolHk para 70% de memória instalada.  
  
    > [!IMPORTANT]  
    >  Se o servidor estiver sendo executado em uma máquina virtual e não for dedicado, defina o valor de MIN_MEMORY_PERCENT para o mesmo valor de MAX_MEMORY_PERCENT.   
    > Confira o tópico [Práticas recomendadas: Usando OLTP in-memory em um ambiente de máquina virtual](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md) para obter mais informações.  
  
    ```tsql  
  
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
  
     Para obter informações sobre os valores máximos para MAX_MEMORY_PERCENT, confira a seção do tópico [Percentual de memória disponível para índices e tabelas com otimização de memória](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable).  
  
-   Reconfigurar **memória máxima do servidor**.  
    Para obter informações sobre como configurar **max server memory** , veja o tópico [Otimizando o desempenho do servidor usando opções de configuração de memória](http://technet.microsoft.com/library/ms177455\(v=SQL.105\).aspx).  
  
##  <a name="bkmk_recoverFromOOM"></a> Resolver o impacto de pouca memória ou condições de OOM na carga de trabalho  
 Obviamente, é melhor não ficar com pouca memória ou na situação de OOM (memória insuficiente). Um bom planejamento e monitoramento pode ajudar a evitar situações de OOM. Ainda assim, o melhor planejamento nem sempre prevê o que realmente acontece e você pode acabar com pouca memória ou OOM. Há duas etapas para a recuperação de OOM:  
  
1.  [Abrir uma DAC (Conexão de Administrador Dedicada)](resolve-out-of-memory-issues.md#bkmk_opendac)  
  
2.  [Realizar a ação corretiva](resolve-out-of-memory-issues.md#bkmk_takecorrectiveaction)  
  
###  <a name="bkmk_openDAC"></a> Abrir uma DAC (Conexão de Administrador Dedicada)  
 O Microsoft SQL Server fornece uma DAC (conexão de administrador dedicada). A DAC permite que um administrador acesse uma instância em execução do Mecanismo de Banco de Dados do SQL Server para resolver problemas no servidor, mesmo quando o servidor não está respondendo às conexões de outro cliente. A DAC está disponível com o utilitário do `sqlcmd` e o SQL Server Management Studio (SSMS).  
  
 Para obter orientação sobre como usar o `sqlcmd` e o DAC, veja [Usando uma conexão de administrador dedicada](http://msdn.microsoft.com/library/ms189595\(v=sql.100\).aspx/css). Para obter orientação sobre como usar o DAC por meio do SSMS, veja [Como usar a conexão de administrador dedicada com o SQL Server Management Studio](http://msdn.microsoft.com/library/ms178068.aspx).  
  
###  <a name="bkmk_takeCorrectiveAction"></a> Realizar a ação corretiva  
 Para resolver a sua condição de OOM, você precisa ou liberar memória existente reduzindo o uso ou disponibilizar mais memória para as tabelas de memória.  
  
#### <a name="free-up-existing-memory"></a>Liberar memória existente  
  
##### <a name="delete-non-essential-memory-optimized-table-rows-and-wait-for-garbage-collection"></a>Excluir linhas não essenciais da tabela com otimização de memória e aguardar a coleta de lixo  
 Você pode remover as linhas não essenciais de uma tabela com otimização de memória. O coletor de lixo retorna a memória usada por essas linhas para a memória disponível. para obter informações sobre a ferramenta de configuração e recursos adicionais. O mecanismo de OLTP na memória coleta linhas de lixo de maneira agressiva. No entanto, uma transação demorada poderá evitar a coleta de lixo. Por exemplo, se você tiver uma transação que é executada durante 5 minutos, todas as versões de linha criadas por causa das operações de atualização/exclusão enquanto a transação estava ativa não poderão ser limpas.  
  
##### <a name="move-one-or-more-rows-to-a-disk-based-table"></a>Mover uma ou mais linhas a uma tabela baseada em disco  
 Os seguintes artigos da TechNet fornecem orientação sobre como mover linhas de uma tabela com otimização de memória para uma tabela baseada em disco.  
  
-   [Particionamento de nível de aplicativo](http://technet.microsoft.com/library/dn296452\(v=sql.120\).aspx)  
  
-   [Padrão de aplicativo para particionamento de tabelas com otimização de memória](http://technet.microsoft.com/library/dn133171\(v=sql.120\).aspx)  
  
#### <a name="increase-available-memory"></a>Aumentar a memória disponível  
  
##### <a name="increase-value-of-maxmemorypercent-on-the-resource-pool"></a>Aumentar o valor de MAX_MEMORY_PERCENT no pool de recursos  
 Se você não criou um pool de recursos nomeado para as tabelas de memória, deverá fazer isso e associar seus bancos de dados do [!INCLUDE[hek_2](../../includes/hek-2-md.md)] a ele. Confira o tópico [Associar um banco de dados com tabelas com otimização de memória a um pool de recursos](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md) para obter diretrizes sobre como criar e associar bancos de dados do [!INCLUDE[hek_2](../../includes/hek-2-md.md)] a um pool de recursos.  
  
 Se seu banco de dados do [!INCLUDE[hek_2](../../includes/hek-2-md.md)] estiver associado a um pool de recursos, você poderá aumentar a porcentagem de memória que o pool pode acessar. Confira o subtópico [Alterar MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT em um pool existente](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation) para obter diretrizes sobre como alterar o valor de MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT em um pool de recursos.  
  
 Aumente o valor de MAX_MEMORY_PERCENT.   
Este trecho de código altera MAX_MEMORY_PERCENT para o pool de recursos PoolHk para 70% de memória instalada.  
  
> [!IMPORTANT]  
>  Se o servidor estiver sendo executado em uma máquina virtual e não for dedicado, defina o valor de MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT como o mesmo.   
> Confira o tópico [Práticas recomendadas: Usando OLTP in-memory em um ambiente de máquina virtual](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md) para obter mais informações.  
  
```tsql  
  
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
  
 Para obter informações sobre os valores máximos para MAX_MEMORY_PERCENT, confira a seção do tópico [Percentual de memória disponível para índices e tabelas com otimização de memória](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable).  
  
##### <a name="install-additional-memory"></a>Instalar a memória adicional  
 Por fim, a melhor solução, se possível, é instalar mais memória física. Se você fizer isso, lembre-se de que provavelmente também poderá aumentar o valor de MAX_MEMORY_PERCENT (confira o subtópico [Alterar MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT em um pool existente](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation)), já que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] talvez não precise de mais memória, permitindo assim que você disponibilize a maior parte da memória recém-instalada, se não toda ela, ao pool de recursos.  
  
> [!IMPORTANT]  
>  Se o servidor estiver sendo executado em uma máquina virtual e não for dedicado, defina o valor de MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT como o mesmo.   
> Confira o tópico [Práticas recomendadas: Usando OLTP in-memory em um ambiente de máquina virtual](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md) para obter mais informações.  
  
##  <a name="bkmk_PageAllocFailure"></a> Resolver falhas de alocação de página devido à memória insuficiente quando há memória suficiente disponível  
 Se você receber a mensagem de erro “Desautorizando as alocações de página do banco de dados '*\<databaseName>*' devido à memória insuficiente no pool de recursos '*\<resourcePoolName*'”. Consulte 'http://go.microsoft.com/fwlink/?LinkId=330673' para obter mais informações. " No log de erros quando a memória física disponível for suficiente para alocar a página, talvez isso ocorra devido a um Administrador de Recursos desabilitado. Quando o Administrador de Recursos é desabilitado, MEMORYBROKER_FOR_RESERVE induz artificial à pressão de memória artificial.  
  
 Para resolver isso, é necessário habilitar o Administrador de Recursos.  
  
 Veja [Habilitar Administrador de Recursos](http://technet.microsoft.com/library/bb895149.aspx) para obter informações sobre limites e restrições, bem como diretrizes sobre como habilitar o Administrador de Recursos usando o Pesquisador de Objetos, as propriedades do Administrador de Recursos ou o Transact-SQL.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando memória para OLTP na memória](../../database-engine/managing-memory-for-in-memory-oltp.md)   
 [Monitorar e solucionar problemas de uso da memória](monitor-and-troubleshoot-memory-usage.md)   
 [Associar um banco de dados com tabelas com otimização de memória a um pool de recursos](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [Práticas recomendadas: Usando OLTP in-memory em um ambiente de máquina virtual](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)  
  
  
