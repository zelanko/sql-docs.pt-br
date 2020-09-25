---
title: Associar um banco de dados com tabelas com otimização de memória a um pool de recursos
description: Saiba como criar um pool de recursos separado para gerenciar o consumo de memória de um banco de dados do SQL Server com tabelas com otimização de memória.
ms.custom: seo-dt-2019
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f222b1d5-d2fa-4269-8294-4575a0e78636
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ff3d2de93c28d106cf24cd72b72c5d2e3346d287
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91111004"
---
# <a name="bind-a-database-with-memory-optimized-tables-to-a-resource-pool"></a>Associar um banco de dados com tabelas com otimização de memória a um pool de recursos
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Um pool de recursos representa um subconjunto de recursos físicos que podem ser controlados. Por padrão, os bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão associados a e consomem recursos do pool de recursos padrão. Para proteger o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de ter todos os recursos consumidos por uma ou mais tabelas com otimização de memória, e evitar que outros usuários da memória consumam a memória necessária para as tabelas com otimização de memória, você deve criar um pool de recursos separado para gerenciar o consumo de memória para o banco de dados com tabelas com otimização de memória.  
  
 Um banco de dados pode estar associado em apenas um pool de recursos. No entanto, você pode associar vários bancos de dados ao mesmo pool. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite associar um banco de dados sem tabelas com otimização de memória a um pool de recursos, mas isso não tem efeito. Talvez você queira associar um banco de dados a um pool de recursos denominado se, no futuro, talvez você quiser criar tabelas com otimização de memória no banco de dados.  
  
 Antes de associar um banco de dados a um pool de recursos, o banco de dados e o pool de recursos devem existir. A associação entra em vigor da próxima vez que o banco de dados é colocado online. Veja [Estados de banco de dados](../../relational-databases/databases/database-states.md) para obter mais informações.  
  
 Para obter informações sobre pools de recursos, veja [Pool de recursos do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md).  
  
## <a name="steps-to-bind-a-database-to-a-resource-pool"></a>Etapas para associar um banco de dados a um pool de recursos  
  
1.  [Criar o banco de dados e o pool de recursos](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_CreatePool)  
  
    1.  [Criar o banco de dados](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_CreateDatabase)  
  
    2.  [Determine o valor mínimo de MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_DeterminePercent)  
  
    3.  [Criar um pool de recursos e configurar a memória](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_CreateResourcePool)  
  
2.  [Associar o banco de dados ao pool](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_DefineBinding)  
  
3.  [Confirmar a associação](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ConfirmBinding)  
  
4.  [Tornar a associação efetiva](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_MakeBindingEffective)  
  
 Outros conteúdos neste tópico  
  
-   [Alterar MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT em um pool existente](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation)  
  
-   [Porcentagem de memória disponível para tabelas com otimização de memória e índices](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)  
  
##  <a name="create-the-database-and-resource-pool"></a><a name="bkmk_CreatePool"></a> Criar o banco de dados e o pool de recursos  
 Você pode criar o banco de dados e o pool de recursos em qualquer ordem. O que importa é que ambos existam antes de associar o banco de dados ao pool de recursos.  
  
###  <a name="create-the-database"></a><a name="bkmk_CreateDatabase"></a> Criar o banco de dados  
 O [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir cria um banco de dados chamado IMOLTP_DB que conterá uma ou mais tabelas com otimização de memória. O caminho \<driveAndPath> precisa existir antes da execução desse comando.  
  
```sql  
CREATE DATABASE IMOLTP_DB  
GO  
ALTER DATABASE IMOLTP_DB ADD FILEGROUP IMOLTP_DB_fg CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE IMOLTP_DB ADD FILE( NAME = 'IMOLTP_DB_fg' , FILENAME = 'c:\data\IMOLTP_DB_fg') TO FILEGROUP IMOLTP_DB_fg;  
GO  
```  
  
###  <a name="determine-the-minimum-value-for-min_memory_percent-and-max_memory_percent"></a><a name="bkmk_DeterminePercent"></a> Determine o valor mínimo de MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT  
 Depois que você determinar as necessidades de memória para tabelas com otimização de memória, será necessário determinar o percentual de memória disponível necessário e definir os percentuais de memória com esse valor ou um valor mais alto.  
  
 **Exemplo:**    
Para este exemplo, vamos pressupor que, com base nos cálculos, você determinou que suas tabelas com otimização de memória e índices precisam de 16 GB de memória. Digamos que você tenha 32 GB de memória confirmada para uso.  
  
 À primeira vista pode parecer que você precisa definir MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT como 50 (16 são de 50% de 32).  No entanto, isso não daria memória suficiente às tabelas com otimização de memória otimizada. Examinando a tabela abaixo ([Percentual de memória disponível de índices e tabelas com otimização de memória](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)), vemos que, se houver 32 GB de memória confirmada, somente 80% dessa quantidade estará disponível para índices e tabelas com otimização de memória.  Consequentemente, calculamos percentuais mínimo e máximo com base na memória disponível, não na memória confirmada.  
  
 `memoryNeedeed = 16`   
 `memoryCommitted = 32`   
 `availablePercent = 0.8`   
 `memoryAvailable = memoryCommitted * availablePercent`   
 `percentNeeded = memoryNeeded / memoryAvailable`  
  
 Em números reais:   
`percentNeeded = 16 / (32 * 0.8) = 16 / 25.6 = 0.625`  
  
 Dessa forma, você precisa de pelo menos 62,5% da memória disponível para cumprir o requisito de 16 GB de tabelas com otimização de memória e índices.  Como os valores de MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT devem ser inteiros, vamos configurá-los como pelo menos 63%.  
  
###  <a name="create-a-resource-pool-and-configure-memory"></a><a name="bkmk_CreateResourcePool"></a> Criar um pool de recursos e configurar a memória  
 Ao configurar a memória para tabelas com otimização de memória, o planejamento de capacidade deve ser feito com base em MIN_MEMORY_PERCENT, não MAX_MEMORY_PERCENT.  Veja [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md) para obter informações sobre MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT. Isso fornece uma disponibilidade de memória mais previsível para tabelas com otimização de memória porque o MIN_MEMORY_PERCENT causa uma pressão de memória em outros pools de recursos para garantir que seja cumprida. Para garantir que essa memória esteja disponível e para ajudar a evitar condições de memória insuficiente, os valores de MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT devem ser iguais. Veja [Percentual de memória disponível de índices e tabelas com otimização de memória](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable) abaixo para obter o percentual de memória disponível para tabelas com otimização de memória com base na quantidade de memória confirmada.  
  
 Confira [Melhores práticas: usar OLTP in-memory em um ambiente de VM](https://msdn.microsoft.com/library/27ec7eb3-3a24-41db-aa65-2f206514c6f9) para obter mais informações ao trabalhar em um ambiente de VM.  
  
 O código [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir cria um pool de recursos chamado Pool_IMOLTP com metade da memória disponível para esse uso.  Depois que o pool é criado, o Administrador de Recursos é reconfigurado para incluir Pool_IMOLTP.  
  
```sql  
-- set MIN_MEMORY_PERCENT and MAX_MEMORY_PERCENT to the same value  
CREATE RESOURCE POOL Pool_IMOLTP   
  WITH   
    ( MIN_MEMORY_PERCENT = 63,   
    MAX_MEMORY_PERCENT = 63 );  
GO  
  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
##  <a name="bind-the-database-to-the-pool"></a><a name="bkmk_DefineBinding"></a> Associar o banco de dados ao pool  
 Use a função do sistema `sp_xtp_bind_db_resource_pool` para associar o banco de dados ao pool de recursos. A função usa dois parâmetros: o nome do banco de dados e o nome do pool de recursos.  
  
 O [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir define uma associação do banco de dados IMOLTP_DB ao pool de recursos Pool_IMOLTP. A associação não entra em vigor até que você coloque o banco de dados online.  
  
```sql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
 A função de sistema sp_xtp_bind_db_resourece_pool usa dois parâmetros de cadeia de caracteres: nome_do_banco_de_dados e nome_do_pool.  
  
##  <a name="confirm-the-binding"></a><a name="bkmk_ConfirmBinding"></a> Confirmar a associação  
 Confirme a associação, observando a ID do pool de recursos para IMOLTP_DB. Não deve ser NULL.  
  
```sql  
SELECT d.database_id, d.name, d.resource_pool_id  
FROM sys.databases d  
GO  
```  
  
##  <a name="make-the-binding-effective"></a><a name="bkmk_MakeBindingEffective"></a> Tornar a associação efetiva  
 Você deve colocar o banco de dados offline e depois online de novo depois de associá-lo ao pool de recursos para que a associação entre em vigor. Se seu banco de dados tiver sido associado a um pool diferente anteriormente, isso removerá a memória alocada do pool de recursos anterior, e as alocações de memória para sua tabela com otimização de memória e os índices agora virão do pool de recursos recém-associado ao banco de dados.  
  
```sql  
USE master  
GO  
  
ALTER DATABASE IMOLTP_DB SET OFFLINE  
GO  
ALTER DATABASE IMOLTP_DB SET ONLINE  
GO  
  
USE IMOLTP_DB  
GO  
```  
  
 Agora o banco de dados está associado ao pool de recursos.  
  
##  <a name="change-min_memory_percent-and-max_memory_percent-on-an-existing-pool"></a><a name="bkmk_ChangeAllocation"></a> Alterar MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT em um pool existente  
 Se você adicionar mais memória ao servidor ou se a quantidade de memória das suas tabelas com otimização de memória for alterada, talvez seja necessário alterar o valor de MIN_MEMORY_PERCENT e de MAX_MEMORY_PERCENT. As etapas a seguir mostram como alterar o valor de MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT em um pool de recursos. Consulte a seção abaixo, para obter orientação sobre quais valores usar para MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT.  Confira o tópico [Melhores práticas: usar OLTP in-memory em um ambiente de VM](https://msdn.microsoft.com/library/27ec7eb3-3a24-41db-aa65-2f206514c6f9) para obter mais informações.  
  
1.  Use `ALTER RESOURCE POOL` para alterar o valor de MIN_MEMORY_PERCENT e MAX_MEMORY_PERCENT.  
  
2.  Use `ALTER RESURCE GOVERNOR` para reconfigurar o Administrador de Recursos com os novos valores.  
  
 **Código de exemplo**  
  
```sql  
ALTER RESOURCE POOL Pool_IMOLTP  
WITH  
     ( MIN_MEMORY_PERCENT = 70,  
       MAX_MEMORY_PERCENT = 70 )   
GO  
  
-- reconfigure the Resource Governor  
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
```  
  
##  <a name="percent-of-memory-available-for-memory-optimized-tables-and-indexes"></a><a name="bkmk_PercentAvailable"></a> Porcentagem de memória disponível para tabelas com otimização de memória e índices  
 Se você mapear um banco de dados com tabelas com otimização de memória e uma carga de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o mesmo pool de recursos, o Administrador de Recursos definirá um limite interno para o [!INCLUDE[hek_2](../../includes/hek-2-md.md)] usar de modo que os usuários do pool não tenham conflitos sobre o uso do pool. Em linhas gerais, o limite para o uso do [!INCLUDE[hek_2](../../includes/hek-2-md.md)] é de aproximadamente 80% do pool. A tabela a seguir mostra os limites reais para vários tamanhos de memória.  
  
 Quando você cria um pool de recursos dedicado para o banco de dados [!INCLUDE[hek_2](../../includes/hek-2-md.md)] , precisa estimar a quantidade de memória física necessária para as tabelas na memória, após considerar versões de linhas e o crescimento de dados. Após estimar a memória necessária, você cria um pool de recursos com uma porcentagem da memória de destino de confirmação para a Instância SQL, conforme refletido pela coluna ‘committed_target_kb’ no DMV [`sys.dm_os_sys_info`](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md). Por exemplo, você pode criar um pool de recursos P1 com 40% da memória total disponível para a instância. Além desses 40%, o mecanismo de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] obtém uma porcentagem menor para armazenar dados de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] .  Isso é feito para garantir que [!INCLUDE[hek_2](../../includes/hek-2-md.md)] não consuma toda a memória desse pool.  Esse valor de porcentagem menor depende da Memória confirmada de destino. A tabela a seguir descreve a memória disponível para o banco de dados de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] em um pool de recursos (nomeado ou padrão), antes que um erro de OOM seja gerado.  
  
|Memória confirmada de destino|Porcentagem disponível para tabelas na memória|  
|-----------------------------|---------------------------------------------|  
|<= 8 GB|70%|  
|<= 16 GB|75%|  
|<= 32 GB|80%|  
|\<= 96 GB|85%|  
|>96 GB|90%|  
  
 Por exemplo, se a 'memória confirmada de destino' for 100 GB e você calcular que as tabelas com otimização de memória e os índices precisam de 60 GB de memória, poderá criar um pool de recursos com MAX_MEMORY_PERCENT = 67 (60 GB necessários / 0,90 = 66,667 GB – arredondar para 67 GB, 67 GB / 100 GB instalados = 67%) para garantir que seus objetos [!INCLUDE[hek_2](../../includes/hek-2-md.md)] tenham os 60 GB necessários.  
  
 Quando um banco de dados for associado a um pool de recursos nomeado, use a consulta a seguir para ver as alocações de memória em diferentes pools de recursos.  
  
```sql  
SELECT pool_id  
     , Name  
     , min_memory_percent  
     , max_memory_percent  
     , max_memory_kb/1024 AS max_memory_mb  
     , used_memory_kb/1024 AS used_memory_mb   
     , target_memory_kb/1024 AS target_memory_mb  
   FROM sys.dm_resource_governor_resource_pools  
```  
  
 Esta saída de exemplo mostra que a memória usada por objetos com otimização de memória é de 1356 MB no pool de recursos, PoolIMOLTP, com um limite superior de 2307 MB. Esse limite superior controla a memória total que pode ser usada pelo usuário e os objetos com otimização de memória do sistema que são mapeados para esse pool.  
  
 **Saída de exemplo**   
Esta saída é do banco de dados e das tabelas criadas anteriormente.  
  
```  
pool_id     Name        min_memory_percent max_memory_percent max_memory_mb used_memory_mb target_memory_mb  
----------- ----------- ------------------ ------------------ ------------- -------------- ----------------   
1           internal    0                  100                3845          125            3845  
2           default     0                  100                3845          32             3845  
259         PoolIMOLTP 0                  100                3845          1356           2307  
```  
  
 Para obter mais informações, confira [sys.dm_resource_governor_resource_pools (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md).  
  
 Se você não associa o banco de dados a um pool de recursos nomeado, ele é associado ao pool ‘padrão‘. Como o pool de recursos padrão é usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a maioria das demais alocações, você não poderá monitorar a memória consumida por tabelas com otimização de memória usando o DMV sys.dm_resource_governor_resource_pools de forma precisa para o banco de dados de interesse.  
  
## <a name="see-also"></a>Consulte Também  
 [sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql.md)   
 [sys.sp_xtp_unbind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md)   
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Pool de recursos do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Criar um pool de recursos](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [Alterar configurações do pool de recursos](../../relational-databases/resource-governor/change-resource-pool-settings.md)   
 [Excluir um pool de recursos](../../relational-databases/resource-governor/delete-a-resource-pool.md)  
  
  
