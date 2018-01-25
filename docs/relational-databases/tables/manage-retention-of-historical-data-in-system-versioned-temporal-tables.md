---
title: "Gerenciar a retenção de dados históricos em tabelas temporais com controle de versão do sistema | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7925ebef-cdb1-4cfe-b660-a8604b9d2153
caps.latest.revision: "23"
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 41c64af6ffe805d6b0b92ffde0c7057a7cd2abca
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="manage-retention-of-historical-data-in-system-versioned-temporal-tables"></a>Gerenciar a Retenção de Dados Históricos em Tabelas Temporais com Versão do Sistema
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Com tabelas temporais com versão do sistema, a tabela de histórico pode aumentar o tamanho do banco de dados mais do que tabelas regulares, especialmente nas seguintes condições:  
  
-   Você retém dados históricos por um longo período de tempo  
  
-   Você tem uma atualização ou exclusão de modificação de dados pesados  
  
 Uma tabela de histórico grande e crescente pode se tornar um problema, tanto devido a custos de armazenamento puro, como por impor um desempenho imposto sobre consultas temporais. Portanto, o desenvolvimento de uma política de retenção de dados para o gerenciamento de dados na tabela de histórico é um aspecto importante do planejamento e gerenciamento do ciclo de vida de cada tabela temporal.  
  
## <a name="data-retention-management-for-history-table"></a>Gerenciamento da retenção de dados da tabela de histórico  
 O gerenciamento da retenção de dados da tabela temporal começa com a determinação do período de retenção necessário para cada tabela temporal. Sua política de retenção, na maioria dos casos, deve ser considerada parte da lógica de negócios do aplicativo usando as tabelas temporais. Por exemplo, aplicativos na auditoria de dados e cenários de viagem de tempo têm requisitos sólidos em termos de quanto tempo os dados históricos devem estar disponíveis para consulta online.  
  
 Após determinar o período de retenção de dados, a próxima etapa é desenvolver um plano para gerenciar os dados históricos, como e onde você armazena seus dados históricos e como excluir dados históricos anteriores aos requisitos de retenção. As três abordagens a seguir estão disponíveis para gerenciar dados históricos na tabela de histórico temporal:  
  
-   [Stretch Database](https://msdn.microsoft.com/library/mt637341.aspx#using-stretch-database-approach)  
  
-   [Particionamento de Tabela](https://msdn.microsoft.com/library/mt637341.aspx#using-table-partitioning-approach)  
  
-   [Script de Limpeza Personalizada](https://msdn.microsoft.com/library/mt637341.aspx#using-custom-cleanup-script-approach)  

-   [Política de Retenção](https://msdn.microsoft.com/library/mt637341.aspx#using-temporal-history-retention-policy-approach)  

 Com cada uma dessas abordagens, a lógica para a migração ou limpeza de dados históricos baseia-se na coluna que corresponde ao término do período na tabela atual. O final do valor do período para cada linha determina o momento em que a versão de linha se torna "fechada", ou seja, quando ela chega à tabela de histórico. Por exemplo, a condição `SysEndTime < DATEADD (DAYS, -30, SYSUTCDATETIME ())` especifica que dados históricos com mais de um mês precisam ser removidos ou movidos da tabela de histórico.  
  
> **OBSERVAÇÃO:**  os exemplos deste tópico usam este [exemplo de Tabela Temporal](creating-a-system-versioned-temporal-table.md).  
  
## <a name="using-stretch-database-approach"></a>Utilização da abordagem do Stretch Database  
  
> **OBSERVAÇÃO:**  o uso da abordagem do Stretch Database só se aplica ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e não se aplica ao [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md) em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] migra os dados históricos de forma transparente para o Azure. Para mais segurança, é possível criptografar dados em movimento usando o recurso [Sempre Criptografado](https://msdnstage.redmond.corp.microsoft.com/library/mt163865.aspx) do SQL Server. Além disso, você pode usar a [Segurança em nível de linha](../../relational-databases/security/row-level-security.md) e outros recursos de segurança avançados do SQL Server com o Stretch Database e o Temporal para proteger seus dados.  
  
 Ao utilizar a abordagem do Stretch Database, você pode ampliar algumas ou todas as tabelas de histórico temporal para o Azure e, assim, o SQL Server moverá silenciosamente os dados históricos para o Azure. Habilitar a ampliação de uma tabela de histórico não altera a forma como você interage com a tabela temporal em termos de modificação de dados e consultas temporais.  
  
-   **Ampliar toda a tabela de histórico:** configure o Stretch Database para a tabela de histórico inteira se seu cenário principal for a auditoria de dados no ambiente com alterações frequentes dos dados e consultas relativamente raras em dados históricos.  Em outras palavras, use essa abordagem se o desempenho de consultas temporais não for crítico. Nesse caso, o custo-benefício fornecido pelo Azure pode ser atraente.   
    Ao ampliar a tabela de histórico inteira, você pode usar o Assistente de Ampliação ou o Transact-SQL. Exemplos de ambos são exibidos abaixo.  
  
-   **Ampliar uma parte da tabela de histórico:** configure o Stretch Database para apenas uma parte de sua tabela de histórico para melhorar o desempenho se o cenário principal envolver principalmente a consulta de dados históricos recentes e você desejar preservar a opção para consultar dados históricos mais antigos, quando necessário, ao armazenar esses dados remotamente a um custo menor. Com o Transact-SQL, você pode fazer isso especificando uma função de predicado para selecionar as linhas que serão migradas da tabela de histórico, em vez de todas as linhas.  Quando você trabalha com tabelas temporais, geralmente faz sentido mover dados com base na condição de tempo (ou seja, com base na idade da versão de linha na tabela de histórico).    
    Usando uma função de predicado determinística, você pode manter parte do histórico no mesmo banco de dados com os dados atuais, enquanto o restante é migrado para o Azure.    
    Para obter exemplos e limitações, consulte [Selecionar linhas para migração usando uma função de filtro (Stretch Database)](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md). Como as funções não determinísticas não são válidas, se você quiser transferir dados históricos usando o modo de janela deslizante, precisaria alterar regularmente a definição da função de predicado embutido para que a janela de linhas que você mantém localmente fosse constante em termos de idade. A janela deslizante permite mover constantemente dados históricos com mais de um mês para o Azure. Um exemplo dessa abordagem é exibido abaixo.  
  
> **OBSERVAÇÃO:** o Stretch Database migra dados para o Azure. Portanto, você precisa ter uma conta do Azure e uma assinatura para cobrança. Para obter uma conta de avaliação gratuita do Azure, clique em [Avaliação gratuita de um mês](https://azure.microsoft.com/pricing/free-trial/).  
  
 Você pode configurar uma tabela de histórico temporal para o Stretch usando o Assistente de transferência ou o Transact-SQL e pode habilitar para ampliação uma tabela de histórico temporal enquanto o sistema de controle de versão é definido como **ON**. Não é permitido ampliar a tabela atual porque isso não faz sentido.  
  
### <a name="using-the-stretch-wizard-to-stretch-the-entire-history-table"></a>Usando o Assistente de Ampliação para ampliar a tabela de histórico inteira  
 O método mais fácil para iniciantes é usar o Assistente de ampliação para habilitar a ampliação do banco de dados inteiro e escolher a tabela de histórico temporal no assistente de ampliação (este exemplo supõe que você tenha configurado a tabela Department como uma tabela temporal com versão do sistema em um banco de dados vazio). No [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], não é possível clicar com o botão direito do mouse na própria tabela de histórico temporal e clicar em Ampliar.  
  
1.  Clique com o botão direito do mouse em seu banco de dados e aponte para **Tarefas**, aponte para **Stretch**e clique em **Habilitar** para iniciar o assistente.  
  
2.  Na janela **Selecionar tabelas** , marque a caixa de seleção da tabela de histórico temporal e clique em Avançar.  
  
     ![Selecionando a tabela de histórico na página Selecionar tabelas](../../relational-databases/tables/media/stretch-wizard-2-for-temporal.png "Selecionando a tabela de histórico na página Selecionar tabelas")  
  
3.  Na janela **Configurar o Azure** , forneça suas credenciais de logon. Entre no Microsoft Azure ou se inscreva em uma conta. Selecione a assinatura a ser usada e escolha a região do Azure. Em seguida, crie um novo servidor ou escolha um servidor existente. Clique em **Avançar**.  
  
     ![Criar novo servidor do Azure – Assistente do Stretch Database](../../relational-databases/tables/media/stretch-wizard-4.png "Criar novo servidor do Azure – Assistente do Stretch Database")  
  
4.  Na janela **Proteger credenciais** , forneça uma senha para a chave mestra de banco de dados para proteger suas credenciais de banco de dados SQL Server de origem e clique em Avançar.  
  
     ![Página Proteger Credenciais do Assistente do Stretch Database](../../relational-databases/tables/media/stretch-wizard-6.png "Página Proteger Credenciais do Assistente do Stretch Database")  
  
5.  Na janela **Selecionar endereço IP** , forneça o intervalo de endereços IP do SQL Server para permitir que o servidor do Azure se comunique com o SQL Server (se você selecionar um servidor existente para o qual uma regra de firewall já exista, basta clicar em Avançar aqui para usar a regra de firewall existente). Clique em **Avançar** e em **Concluir** para habilitar o Stretch Database e transferir a tabela de histórico temporal.  
  
     ![Página Selecionar endereço IP do Assistente do Stretch Database](../../relational-databases/tables/media/stretch-wizard-7.png "Página Selecionar endereço IP do Assistente do Stretch Database")  
  
6.  Após a conclusão do assistente, verifique se seu banco de dados foi habilitado com êxito para Stretch. Observe os ícones no Pesquisador de Objetos indicando que o banco de dados foi transferido  
  
> **OBSERVAÇÃO:** se a opção Habilitar Banco de Dados para Stretch falhar, examine o log de erros. Um erro comum é a configuração incorreta da regra de firewall.  
  
 Consulte também:  
  
-   [Habilitar o Stretch Database para um banco de dados](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)  
  
-   [Comece executando o Assistente para Habilitar o Banco de Dados para Alongamento](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md)  
  
-   [Habilitar o Stretch Database para uma tabela](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
### <a name="using-transact-sql-to-stretch-the-entire-history-table"></a>Usando o Transact-SQL para alongar a tabela de histórico inteira  
 Você também pode usar o Transact-SQL para habilitar o Stretch no servidor local e para [Habilitar Stretch Database em um banco de dados](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md). Você pode  [usar o Transact-SQL para habilitar o Stretch Database em uma tabela](https://msdn.microsoft.com/library/mt605115.aspx#Anchor_1). Com um banco de dados habilitado anteriormente para Stretch Database, execute o seguinte script Transact-SQL para alongar uma tabela de histórico temporal com controle de versão do sistema existente:  
  
```  
ALTER TABLE <history table name>   
SET (REMOTE_DATA_ARCHIVE = ON (MIGRATION_STATE = OUTBOUND));  
```  
  
### <a name="using-transact-sql-to-stretch-a-portion-of-the-history-table"></a>Usando o Transact-SQL para alongar uma parte da tabela de histórico  
 Para transferir apenas uma parte da tabela de histórico, comece criando uma [função de predicado embutido](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md). Para este exemplo, vamos supor que você tenha configurado a função de predicado embutido pela primeira vez no dia 1 de dezembro de 2015 e deseja alongar para o Azure todas as datas de histórico anteriores ao dia 1 de novembro de 2015. Para fazer isso, comece criando a seguinte função:  
  
```  
CREATE FUNCTION dbo.fn_StretchBySystemEndTime20151101(@systemEndTime datetime2)   
RETURNS TABLE   
WITH SCHEMABINDING    
AS    
RETURN SELECT 1 AS is_eligible   
  WHERE @systemEndTime < CONVERT(datetime2, '2015-11-01T00:00:00', 101) ;  
```  
  
 Em seguida, use o seguinte script para adicionar o predicado de filtro à tabela de histórico e definir o estado de migração como SAÍDA para permitir a migração de dados com base em predicado para a tabela de histórico.  
  
```  
ALTER TABLE <history table name>   
SET (   
        REMOTE_DATA_ARCHIVE = ON   
                (   
                        FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20151101 (SysEndTime)  
                                , MIGRATION_STATE = OUTBOUND   
                )  
        )   
;  
```  
  
 Para manter uma janela deslizante, você precisa fazer com que a função de predicado seja precisa todos os dias (ou seja, alterar a condição de linha de filtragem diariamente por um dia). O script a seguir é o script que você precisará executar em 2 de dezembro de 2015:  
  
```  
BEGIN TRAN  
           /*(1) Create new predicate function definition */  
        CREATE FUNCTION dbo.fn_StretchBySystemEndTime20151102(@systemEndTime datetime2)  
        RETURNS TABLE  
        WITH SCHEMABINDING   
        AS   
        RETURN SELECT 1 AS is_eligible  
               WHERE @systemEndTime < CONVERT(datetime2,'2015-11-02T00:00:00', 101)  
        GO  
  
        /*(2) Set the new function as filter predicate */  
        ALTER TABLE <history table name>  
        SET   
        (  
               REMOTE_DATA_ARCHIVE = ON  
               (  
                       FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20151102(SysEndTime),  
                       MIGRATION_STATE = OUTBOUND  
               )  
        )   
COMMIT ;  
```  
  
 Use o SQL Server Agent ou outro mecanismo de agendamento para garantir uma definição de função de predicado válida o tempo todo.  
  
## <a name="using-table-partitioning-approach"></a>Uso da Abordagem de Particionamento de Tabela  
 O[Particionamento de tabela](../partitions/create-partitioned-tables-and-indexes.md) pode tornar as tabelas grandes mais gerenciáveis e escalonáveis. Usando a abordagem de particionamento de tabela, você pode usar partições de tabela de histórico para implementar a limpeza de dados personalizados ou o arquivamento offline com base em uma condição de tempo. O particionamento de tabela também oferece benefícios de desempenho ao consultar tabelas temporais em um subconjunto de histórico de dados por meio da eliminação da partição.  
  
 Com o particionamento de tabela, você pode implementar uma abordagem de janela deslizante para mover a parte mais antiga dos dados históricos da tabela de histórico e manter constante o tamanho da parte retida em termos de idade, mantendo os dados na tabela de histórico iguais ao período de retenção necessário. A operação de extração de dados da tabela de histórico é suportada enquanto SYSTEM_VERSIONING estiver configurado como ATIVO. Isso significa que você pode limpar uma parte dos dados de histórico sem introduzir uma janela de manutenção ou bloquear suas cargas de trabalho regulares.  
  
> **OBSERVAÇÃO:** para executar a troca de partição, o índice clusterizado na tabela de histórico deve estar alinhado com o esquema de particionamento (ele deve conter SysEndTime). A tabela de histórico padrão criada pelo sistema contém um índice clusterizado que inclui as colunas SysEndTime e SysStartTime, perfeitas para o particionamento, inserindo novos dados históricos e consulta temporal típica. Para obter mais informações, consulte [Temporal Tables](../../relational-databases/tables/temporal-tables.md).  
  
 Uma abordagem de janela deslizante tem dois conjuntos de tarefas que você precisa executar:  
  
-   Uma tarefa de configuração de particionamento  
  
-   Tarefas de manutenção de partição recorrentes  
  
 Para fins ilustrativos, vamos supor que queremos manter dados históricos por 6 meses e que queremos manter todos os meses de dados em uma partição separada. Além disso, vamos supor que ativaremos a versão de sistema em setembro de 2015.  
  
 Uma tarefa de configuração de particionamento cria a configuração de particionamento inicial para a tabela de histórico. Neste exemplo, criaríamos as mesmas partições de número como o tamanho da janela deslizante, em meses, além de uma partição vazia adicional previamente preparada (explicado abaixo). Essa configuração garante que o sistema será capaz de armazenar novos dados corretamente ao iniciarmos a tarefa de manutenção de partição recorrente para a primeira hora e garantias de que nunca dividiremos partições com dados para evitar movimentos de dados. Essa tarefa deve ser executada usando o Transact-SQL com o script de exemplo abaixo.  
  
 A figura a seguir mostra a configuração inicial de particionamento para manter 6 meses de dados.  
  
 ![Partitioning](../../relational-databases/tables/media/partitioning.png "Partitioning")  
  
> **OBSERVAÇÃO:** consulte Considerações sobre desempenho com o particionamento de tabela abaixo para saber sobre as implicações de desempenho do uso de RANGE LEFT versus RANGE RIGHT durante a configuração do particionamento.  
  
 Observe que a primeira e a última partição são "abertas" em limites superiores e inferiores, respectivamente, para garantir que cada nova linha tenha a partição de destino, independentemente do valor na coluna de particionamento.   
Com o passar do tempo, as novas linhas na tabela de histórico serão levadas para partições superiores. Quando a 6ª partição ficar preenchida, teremos atingido o período de retenção definido como destino. Este é o momento de iniciar a tarefa de manutenção de partição recorrente pela primeira vez (ela precisa ser agendada para ser executada periodicamente, uma vez por mês neste exemplo).  
  
 A figura a seguir ilustra as tarefas de manutenção de partição recorrentes (confira as etapas detalhadas abaixo).  
  
 ![Partitioning2](../../relational-databases/tables/media/partitioning2.png "Partitioning2")  
  
 As etapas detalhadas para as tarefas de manutenção de partição recorrentes são:  
  
1.  SWITCH OUT: crie uma tabela temporária e alterne uma partição entre a tabela de histórico e a tabela de preparo usando a instrução [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) com o argumento SWITCH PARTITION (confira o Exemplo C. Mudando de partições entre tabelas).  
  
    ```  
    ALTER TABLE <history table> SWITCH PARTITION 1 TO <staging table>  
    ```  
  
     Após a alternância de partição, você pode optar por arquivar os dados da tabela de preparo e, em seguida, remover ou truncar a tabela de preparo para já ficar preparada para a próxima vez que você precisar realizar essa tarefa de manutenção de partição recorrente.  
  
2.  MERGE RANGE: mescle a partição vazia 1 com a partição 2 usando [ALTER PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md) com MERGE RANGE (veja o exemplo B). Ao remover o limite mais baixo usando essa função, você efetivamente mescla a partição 1 vazia com a partição 2 anterior para formar a nova partição 1. As outras partições também alteraram efetivamente seus números ordinais.  
  
3.  SPLIT RANGE: crie uma nova partição vazia 7 usando o [ALTER PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md) com SPLIT RANGE (veja o exemplo A). Ao adicionar um novo limite superior usando essa função, você cria efetivamente uma partição separada para o mês seguinte.  
  
### <a name="use-transact-sql-to-create-partitions-on-history-table"></a>Use o Transact-SQL para criar partições na tabela de histórico  
 Use o script Transact-SQL na janela de código abaixo para criar a função de partição, o esquema de partição e recriar o índice clusterizado para ser alinhado por partição com o esquema de partição, as partições. Para este exemplo, vamos criar uma abordagem de janela deslizante de seis meses com partições mensais começando em setembro de 2015.  
  
```  
BEGIN TRANSACTION  
  
        /*Create partition function*/  
        CREATE PARTITION FUNCTION [fn_Partition_DepartmentHistory_By_SysEndTime] (datetime2(7))   
                    AS RANGE LEFT FOR VALUES   
                                (N'2015-09-30T23:59:59.999'  
                                , N'2015-10-31T23:59:59.999'  
                                , N'2015-11-30T23:59:59.999'  
                                , N'2015-12-31T23:59:59.999'  
                                , N'2016-01-31T23:59:59.999'  
                                , N'2016-02-29T23:59:59.999')  
  
        /*Create partition scheme*/  
        CREATE PARTITION SCHEME [sch_Partition_DepartmentHistory_By_SysEndTime]   
                        AS PARTITION [fn_Partition_DepartmentHistory_By_SysEndTime]   
                        TO ([PRIMARY], [PRIMARY], [PRIMARY], [PRIMARY], [PRIMARY], [PRIMARY], [PRIMARY])  
  
        /*Re-create index to be partition-aligned with the partitioning schema*/  
        CREATE CLUSTERED INDEX [ix_DepartmentHistory] ON [dbo].[DepartmentHistory]  
        (  
                    [SysEndTime] ASC,  
                    [SysStartTime] ASC  
        )  
            WITH   
                        (PAD_INDEX = OFF  
                        , STATISTICS_NORECOMPUTE = OFF  
                        , SORT_IN_TEMPDB = OFF  
                        , DROP_EXISTING = ON  
                        , ONLINE = OFF  
                        , ALLOW_ROW_LOCKS = ON  
                        , ALLOW_PAGE_LOCKS = ON  
                        , DATA_COMPRESSION = PAGE)  
            ON [sch_Partition_DepartmentHistory_By_SysEndTime] ([SysEndTime])  
  
COMMIT TRANSACTION;  
  
```  
  
### <a name="using-transact-sql-to-maintain-partitions-in-sliding-window-scenario"></a>Usando o Transact-SQL para manter partições no cenário de janela deslizante  
 Use o script Transact-SQL na janela de código abaixo para manter as partições no cenário de janela deslizante. Neste exemplo, iremos alternar a partição para setembro de 2015 usando o MERGE RANGE e, em seguida, adicionar uma nova partição para março de 2016 usando o SPLIT RANGE.  
  
```  
BEGIN TRANSACTION  
  
         /*(1)  Create staging table */  
         CREATE TABLE [dbo].[staging_DepartmentHistory_September_2015]  
        (  
                 [DeptID] [int] NOT NULL  
                 , [DeptName] [varchar](50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL  
                 , [ManagerID] [int] NULL  
                 ,  [ParentDeptID] [int] NULL  
                 ,  [SysStartTime] [datetime2](7) NOT NULL  
                 ,  [SysEndTime] [datetime2](7) NOT NULL  
         ) ON [PRIMARY]  
         WITH  
         (  
              DATA_COMPRESSION = PAGE  
         )  
  
         /*(2) Create index on the same filegroups as the partition that will be switched out*/  
         CREATE CLUSTERED INDEX [ox_staging_DepartmentHistory_September_2015]    
         ON [dbo].[staging_DepartmentHistory_September_2015]  
         (  
                  [SysEndTime] ASC,  
                  [SysStartTime] ASC  
         )  
      WITH   
          (  
               PAD_INDEX = OFF  
               , SORT_IN_TEMPDB = OFF  
               , DROP_EXISTING = OFF  
               , ONLINE = OFF  
               , ALLOW_ROW_LOCKS = ON  
               , ALLOW_PAGE_LOCKS = ON  
          )   
         ON [PRIMARY]  
  
         /*(3) Create constraints matching the partition that will be switched out*/  
         ALTER TABLE [dbo].[staging_DepartmentHistory_September_2015]  WITH CHECK   
               ADD  CONSTRAINT [chk_staging_DepartmentHistory_September_2015_partition_1]   
                    CHECK  ([SysEndTime]<=N'2015-09-30T23:59:59.999')  
         ALTER TABLE [dbo].[staging_DepartmentHistory_September_2015]   
               CHECK CONSTRAINT [chk_staging_DepartmentHistory_September_2015_partition_1]  
  
         /*(4) Switch partition to staging table*/  
         ALTER TABLE [dbo].[DepartmentHistory]   
         SWITCH PARTITION 1 TO [dbo].[staging_DepartmentHistory_September_2015]   
         WITH (WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 MINUTES, ABORT_AFTER_WAIT = NONE))  
  
         /*(5) [Commented out] Optionally archive the data and drop staging table  
         INSERT INTO [ArchiveDB].[dbo].[DepartmentHistory]   
         SELECT * FROM [dbo].[staging_DepartmentHistory_September_2015];  
         DROP TABLE [dbo].[staging_DepartmentHIstory_September_2015];  
         */  
  
         /*(6) merge range to move lower boundary one month ahead*/  
         ALTER PARTITION FUNCTION [fn_Partition_DepartmentHistory_By_SysEndTime]()   
               MERGE RANGE(N'2015-09-30T23:59:59.999')  
  
         /*(7) Create new empty partition for "April and after" by creating new boundary point and specifying NEXT USED file group*/  
         ALTER PARTITION SCHEME [sch_Partition_DepartmentHistory_By_SysEndTime] NEXT USED [PRIMARY]  
         ALTER PARTITION FUNCTION [fn_Partition_DepartmentHistory_By_SysEndTime]() SPLIT RANGE(N'2016-03-31T23:59:59.999')  
  
COMMIT TRANSACTION  
  
```  
  
 Você pode modificar um pouco o script acima e usá-lo no processo de manutenção regular mensal:  
  
1.  Na etapa (1) criar nova tabela de preparo para o mês que deseja remover (outubro seria o próximo em nosso exemplo)  
  
2.  Na etapa (3) criar e verificar a restrição que coincide com o mês dos dados que você deseja remover: `[SysEndTime]<=N'2015-10-31T23:59:59.999'` para a partição de outubro  
  
3.  Na etapa (4) ALTERNAR partição 1 para a tabela de preparo criada recentemente  
  
4.  Na etapa (6) alterar função de partição mesclando o limite inferior: `MERGE RANGE(N'2015-10-31T23:59:59.999'` depois que você moveu os dados de outubro  
  
5.  Na etapa (7) dividir função de partição criando um novo limite superior: `SPLIT RANGE (N'2016-04-30T23:59:59.999'` depois que você moveu os dados de outubro.  
  
 No entanto, a solução ideal seria executar regularmente um script Transact-SQL genérico que fosse capaz de executar a ação apropriada todos os meses sem modificar o script. É possível generalizar o script acima para agir sobre parâmetros fornecidos (limite inferior que precisa ser mesclado e o novo limite que será criado com divisão de partição). Para evitar a criação de uma tabela de preparo a cada mês, você pode criar uma antecipadamente e reutilizá-la alterando a restrição de verificação para corresponder à partição que será alternada. Examine as páginas a seguir para obter ideias sobre [como a janela deslizante pode ser totalmente automatizada](https://msdn.microsoft.com/library/aa964122.aspx) usando um script Transact-SQL.  
  
### <a name="performance-considerations-with-table-partitioning"></a>Considerações sobre desempenho com o particionamento de tabela  
 É importante executar as operações MERGE e SPLIT RANGE para evitar qualquer movimentação de dados já que ela pode sobrecarregar o desempenho de forma significativa. Para obter mais informações, veja [Modificar uma função de partição](../../relational-databases/partitions/modify-a-partition-function.md). Faça isso usando RANGE LEFT em vez de RANGE RIGHT quando usar [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md).  
  
 Vamos primeiro explicar visualmente o significado das opções RANGE LEFT e RANGE RIGHT:  
  
 ![Partitioning3](../../relational-databases/tables/media/partitioning3.png "Partitioning3")  
  
 Quando você define uma função de partição como RANGE LEFT, os valores especificados são os limites superiores das partições. Quando você usa RANGE RIGHT, os valores especificados são os limites inferiores das partições. Quando você usa a operação MERGE RANGE para remover um limite da definição de função da partição, a implementação subjacente também remove a partição que contém o limite. Se essa partição não estiver vazia, os dados serão movidos para a partição que é o resultado da operação MERGE RANGE.  
  
 No cenário de janela deslizante, sempre removemos o limite mais baixo da partição.  
  
-   Caso RANGE LEFT: no caso RANGE LEFT, o limite da partição menor pertence à partição 1, que está vazia (depois de alternar a partição). Portanto, MERGE RANGE não incorrerá em qualquer movimentação de dados.  
  
-   Caso RANGE RIGHT: no caso RANGE RIGHT, o limite da partição menor pertence à partição 2, que não está vazia, pois presumimos que a partição 1 foi esvaziada pela alternância. Nesse caso, MERGE RANGE incorrerá na movimentação de dados (dados da partição 2 serão movidos para a partição 1). Para evitar isso, RANGE RIGHT no cenário de janela deslizante deve ter a partição 1, que sempre está vazia. Isso significa que, se usarmos RANGE RIGHT, devemos criar e manter uma partição adicional em comparação ao caso RANGE LEFT.  
  
 Conclusão: usar RANGE LEFT na partição deslizante é muito mais simples para o gerenciamento de partição e evita a movimentação de dados. No entanto, definir limites de partição com RANGE RIGHT é um pouco mais simples já que você não precisa lidar com problemas de escala de tempo de data e hora.  
  
## <a name="using-custom-cleanup-script-approach"></a>Usando a Abordagem de Script de Limpeza Personalizada  
 Em casos quando o Stretch Database e o particionamento de tabela abordados não são opções viáveis, a terceira abordagem é excluir os dados da tabela de histórico usando o script de limpeza personalizada. Excluir dados da tabela de histórico só é possível quando **SYSTEM_VERSIONING = OFF**. Para evitar a inconsistência de dados, execute a limpeza durante a janela de manutenção (quando as cargas de trabalho que modificam dados não estão ativas) ou dentro de uma transação (bloqueando efetivamente outras cargas de trabalho).  Esta operação requer a permissão **CONTROL** nas tabelas atuais e de histórico.  
  
 Para bloquear minimamente os aplicativos regulares e consultas do usuário, exclua dados em partes menores com um atraso ao executar o script de limpeza dentro de uma transação. Embora, para todos os cenários, não haja um tamanho ideal para cada bloco de dados a ser excluído, a exclusão de mais de 10.000 linhas em uma única transação pode impor um impacto significativo.  
  
 A lógica de limpeza é a mesma para cada tabela temporal e, portanto, pode ser automatizada de forma relativamente fácil por meio de um procedimento armazenado genérico agendado para ser executado periodicamente para cada tabela temporal para a qual você deseja limitar o histórico de dados.  
  
 O diagrama a seguir ilustra como a lógica de limpeza deve ser organizada para uma única tabela reduzir o impacto sobre as cargas de trabalho em execução.  
  
 ![CustomCleanUpScriptDiagram](../../relational-databases/tables/media/customcleanupscriptdiagram.png "CustomCleanUpScriptDiagram")  
  
 Veja algumas diretrizes de alto nível para implementar o processo. Agende a lógica de limpeza para execução diária e itere todas as tabelas temporais que precisam de limpeza de dados. Use o SQL Server Agent ou outra ferramenta para agendar esse processo:  
  
-   Exclua dados históricos em cada tabela temporal, das mais antigas às linhas mais recentes, em várias iterações em pequenas blocos e evite excluir todas as linhas em uma única transação, conforme mostrado na figura anterior.  
  
-   Implemente cada iteração como uma chamada de procedimento armazenado genérico que remove uma parte dos dados da tabela de histórico (confira o exemplo de código abaixo para esse procedimento).  
  
-   Calcule quantas linhas você precisa excluir de uma tabela temporal individual toda vez que você chamar o processo. Com base nisso e no número de iterações, determine dinamicamente os pontos de divisão para cada chamada de procedimento.  
  
-   Planeje um período de atraso entre as iterações para uma única tabela para reduzir o impacto sobre os aplicativos que acessam a tabela temporal.  
  
 Um procedimento armazenado que exclui os dados de uma única tabela temporal pode parecer no seguinte trecho de código (examine esse código cuidadosamente e ajuste-o antes de aplicá-lo ao seu ambiente):  
  
```  
DROP PROCEDURE IF EXISTS sp_CleanupHistoryData;  
GO  
  
CREATE PROCEDURE sp_CleanupHistoryData  
         @temporalTableSchema sysname  
       , @temporalTableName sysname  
       , @cleanupOlderThanDate datetime2  
AS  
    DECLARE @disableVersioningScript nvarchar(max) = '';  
    DECLARE @deleteHistoryDataScript nvarchar(max) = '';  
    DECLARE @enableVersioningScript nvarchar(max) = '';  
  
DECLARE @historyTableName sysname    
DECLARE @historyTableSchema sysname    
DECLARE @periodColumnName sysname    
  
/*Generate script to discover history table name and end of period column for given temporal table name*/  
EXECUTE sp_executesql   
    N'SELECT @hst_tbl_nm = t2.name, @hst_sch_nm = s.name, @period_col_nm = c.name  
        FROM sys.tables t1   
           JOIN sys.tables t2 on t1.history_table_id = t2.object_id  
        JOIN sys.schemas s on t2.schema_id = s.schema_id  
            JOIN sys.periods p on p.object_id = t1.object_id  
           JOIN sys.columns c on p.end_column_id = c.column_id and c.object_id = t1.object_id  
                  WHERE   
                 t1.name = @tblName and s.name = @schName'  
                , N'@tblName sysname  
                , @schName sysname  
                , @hst_tbl_nm sysname OUTPUT  
                , @hst_sch_nm sysname OUTPUT  
                , @period_col_nm sysname OUTPUT'  
                , @tblName = @temporalTableName  
                , @schName = @temporalTableSchema  
                , @hst_tbl_nm = @historyTableName OUTPUT  
                , @hst_sch_nm = @historyTableSchema OUTPUT  
                , @period_col_nm = @periodColumnName OUTPUT   
  
IF @historyTableName IS NULL OR @historyTableSchema IS NULL OR @periodColumnName IS NULL  
    THROW 50010, 'History table cannot be found. Either specified table is not system-versioned temporal or you have provided incorrect argument values.', 1  
  
/*Generate 3 statements that will run inside a transaction: SET SYSTEM_VERSIONING = OFF, DELETE FROM history_table, SET SYSTEM_VERSIONING = ON */  
SET @disableVersioningScript =  @disableVersioningScript + 'ALTER TABLE [' + @temporalTableSchema + '].[' + @temporalTableName + '] SET (SYSTEM_VERSIONING = OFF)'  
SET @deleteHistoryDataScript =  @deleteHistoryDataScript + ' DELETE FROM  [' + @historyTableSchema + '].[' + @historyTableName + ']   
     WHERE ['+ @periodColumnName + '] < ' + '''' + convert(varchar(128), @cleanupOlderThanDate, 126) +  ''''   
SET @enableVersioningScript =  @enableVersioningScript + ' ALTER TABLE [' + @temporalTableSchema + '].[' + @temporalTableName + ']   
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = [' + @historyTableSchema + '].[' + @historyTableName + '], DATA_CONSISTENCY_CHECK = OFF )); '   
  
BEGIN TRAN  
    EXEC (@disableVersioningScript);  
    EXEC (@deleteHistoryDataScript);  
    EXEC (@enableVersioningScript);  
COMMIT;  
```  

## <a name="using-temporal-history-retention-policy-approach"></a>Usando a abordagem de política de retenção de histórico temporal
> **Observação:** “Usando a abordagem de política de retenção de histórico temporal” aplica-se a [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] e ao SQL Server 2017 partir do CTP 1.3.  

A retenção de histórico temporal pode ser configurado no nível de tabela individual, que permite aos usuários criar políticas de vencimento flexíveis. A aplicação de retenção temporal é simples: requer apenas um parâmetro a ser definido durante a criação da tabela ou alteração do esquema.

Depois de definir a política de retenção, o Banco de Dados SQL do Azure começa a verificar regularmente se há linhas de histórico qualificadas para a limpeza automática de dados. A identificação das linhas correspondentes e sua remoção da tabela de histórico ocorrem de forma transparente na tarefa em segundo plano que é agendada e executada pelo sistema. A condição de vencimento para as linhas da tabela de histórico é verificada com base na coluna que representa o final do período SYSTEM_TIME. Se o período de retenção for definido como seis meses, por exemplo, as linhas de tabela qualificadas para limpeza atenderão a seguinte condição:
```
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
```
No exemplo anterior, supomos que a coluna de ValidTo corresponde ao final do período SYSTEM_TIME.
### <a name="how-to-configure-retention-policy"></a>Como configurar a política de retenção?
Antes de configurar a política de retenção para uma tabela temporal, verifique primeiro se a retenção de histórico temporal está habilitada no nível do banco de dados:
```
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
```
O sinalizador de banco de dados **is_temporal_history_retention_enabled** é definido como ON por padrão, mas os usuários podem alterá-lo com a instrução ALTER DATABASE. Ele também é definido automaticamente como OFF após uma operação de restauração pontual. Para habilitar a limpeza da retenção de histórico temporal para seu banco de dados, execute a seguinte instrução:
```
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
```
A política de retenção é configurada durante a criação de uma tabela especificando o valor do parâmetro HISTORY_RETENTION_PERIOD:
```
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
```
Você pode especificar o período de retenção usando unidades de tempo diferentes: DAYS (dias), WEEKS (semanas), MONTHS (meses) e YEARS (anos). Se HISTORY_RETENTION_PERIOD for omitido, a retenção será considerada INFINITE (infinita). Também é possível usar a palavras-chave INFINITE explicitamente.
Em alguns cenários, pode ser útil configurar a retenção após a criação da tabela ou alterar o valor configurado anteriormente. Neste caso, use a instrução ALTER TABLE:
```
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
```
Para examinar o estado atual da política de retenção, use a seguinte consulta que une o sinalizador de habilitação de retenção temporal no nível do banco de dados com períodos de retenção para tabelas individuais:
```
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
```
### <a name="how-sql-database-deletes-aged-rows"></a>Como o Banco de Dados SQL exclui linhas antigas?
O processo de limpeza depende do layout do índice da tabela de histórico. É importante observar que *somente tabelas de histórico com um índice clusterizado (árvore B ou columnstore) podem ter uma política de retenção finita configurada*. Uma tarefa em segundo plano é criada para executar a limpeza de dados antigos para todas as tabelas temporais com período de retenção finito. A lógica de limpeza para o índice clusterizado rowstore (árvore B) exclui as linhas antigas em partes menores (até 10K) minimizando a pressão sobre o log do banco de dados e o subsistema de E/S. Embora a lógica de limpeza utilize o índice de árvore B necessário, a ordem das exclusões para as linhas mais antigas que o período de retenção não pode ser garantido com certeza. Portanto, *não assuma nenhuma dependência na ordem de limpeza em seus aplicativos*.

A tarefa de limpeza para o columnstore clusterizado remove grupos de linha inteiros de uma vez (que normalmente contém 1 milhão de linhas em cada), o que é muito eficiente, especialmente quando os dados históricos são gerados em alta velocidade.

![Retenção de columnstore clusterizado](../../relational-databases/tables/media/cciretention.png "Retenção de columnstore clusterizado")

A excelente compactação de dados e eficiente limpeza da retenção torna o índice de columnstore clusterizado uma opção ideal para cenários em que sua carga de trabalho gera rapidamente uma grande quantidade de dados históricos. Esse padrão é comum para cargas de trabalho intensivas de processamento de transações que usam tabelas temporais para controle de alterações e auditoria, análise de tendências ou ingestão de dados IoT.

Confira [Gerenciar dados históricos em tabelas temporais com a política de retenção](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-temporal-tables-retention-policy) para obter mais detalhes.

## <a name="see-also"></a>Consulte Também  
 [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)   
 [Introdução a Tabelas Temporais com Controle da Versão do Sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Particionamento de Tabelas Temporais](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Considerações e limitações da tabela temporal](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Segurança da tabela temporal](../../relational-databases/tables/temporal-table-security.md)   
 [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
