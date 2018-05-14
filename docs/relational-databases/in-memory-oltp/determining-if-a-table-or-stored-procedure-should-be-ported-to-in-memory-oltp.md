---
title: Determinando se uma tabela ou um procedimento armazenado deve ser movido para o OLTP in-memory | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Analyze, Migrate, Report
- AMR
ms.assetid: c1ef96f1-290d-4952-8369-2f49f27afee2
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ffc32787570449c192f7a24b56b03cfa7e2bbdd7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp"></a>Determinando se uma tabela ou um procedimento armazenado deve ser movido para o OLTP na memória
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  O relatório de Análise de Desempenho da Transação no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o ajuda a avaliar se o OLTP in-memory melhorará o desempenho de seu aplicativo de banco de dados. Também indica quanto trabalho você deve fazer para habilitar o OLTP na memória no seu aplicativo. Depois de identificar uma tabela baseada em disco a ser transportada para o OLTP in-memory, você poderá usar o [Orientador de Otimização da Memória](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md)para ajudar na migração da tabela. De maneira semelhante, o [Native Compilation Advisor](../../relational-databases/in-memory-oltp/native-compilation-advisor.md) o ajudará a transportar um procedimento armazenado para um procedimento armazenado compilado nativamente. Para obter informações sobre as metodologias de migração, consulte [In-Memory OLTP – Common Workload Patterns and Migration Considerations](https://msdn.microsoft.com/library/dn673538.aspx)(OLTP in-memory – Padrões comuns de carga de trabalho e considerações de migração).  
  
 O relatório de Análise de desempenho da transação é executado diretamente no banco de dados de produção, ou em um banco de dados de teste com uma carga de trabalho ativa semelhante à carga de trabalho de produção.  
  
 Os consultores de migração e relatório ajudam você a realizar as seguintes tarefas:  
  
-   Analisar sua carga de trabalho para determinar os pontos de acesso onde o OLTP in-memory pode ajudar a melhorar o desempenho. O relatório de Análise de desempenho da transação recomenda as tabelas e os procedimentos armazenados que serão mais beneficiados com a conversão em OLTP in-memory.  
  
-   Ajudar você a planejar e executar a migração para o OLTP na memória. O caminho de migração de uma tabela com base em disco para uma tabela com otimização de memória pode ser demorado. O Orientador de Otimização da Memória o ajuda a identificar as incompatibilidades na tabela que você deve remover antes de movê-la para o OLTP na memória. O Orientador de Otimização em Memória também ajuda a entender o impacto que a migração de uma tabela para uma tabela com otimização de memória terá no seu aplicativo.  
  
     Você poderá verificar se seu aplicativo pode se beneficiar do OLTP na memória, quando desejar planejar a migração para o OLTP na memória e sempre que trabalhar para migrar alguma de suas tabelas e os procedimentos armazenados para o OLTP na memória.  
  
    > [!IMPORTANT]  
    >  O desempenho de um sistema de banco de dados depende de vários fatores e nem todos podem ser observados e medidos pelo coletor de desempenho da transação. Portanto, o relatório de análise de desempenho da transação não garante que os ganhos de desempenho reais corresponderão a essas previsões, caso elas sejam feitas.  
  
 O relatório de Análise de Desempenho da Transação e os consultores de migração são instalados como parte do SSMS (SQL Server Management Studio) quando você seleciona **Ferramentas de Gerenciamento – Básico** ou **Ferramentas de Gerenciamento – Avançado** ao instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ou quando você [baixa o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).    
  
## <a name="transaction-performance-analysis-reports"></a>Relatórios de Análise de desempenho da transação  
 Você pode gerar relatórios de análise de desempenho da transação no **Pesquisador de Objetos** clicando com o botão direito no banco de dados, selecionando **Relatórios**, **Relatórios Padrão**e **Visão Geral da Análise de Desempenho da Transação**. O banco de dados deve ter uma carga de trabalho ativa, ou uma execução recente de uma carga de trabalho, para gerar um relatório de análise significativo.  
  
### <a name="tables"></a>Tabelas
  
 Os detalhes relatados para uma tabela consistem em três seções:  
  
-   Seção Estatísticas de Verificação  
  
     Esta seção inclui uma única tabela que mostra as estatísticas que foram coletadas sobre verificações na tabela do banco de dados. As colunas são:  
  
    -   Percentual de total de acessos. O percentual de verificações e pesquisas nesta tabela em relação à atividade do banco de dados inteiro. Quanto mais alto for esse percentual, mais intensa será a utilização da tabela em comparação com outras tabelas no banco de dados.  
  
    -   Estatísticas de Pesquisa/Estatísticas de Verificação do Intervalo. Essa coluna registra o número de pesquisas de ponto e de verificações de intervalo (verificações de índice e de tabela) realizadas na tabela durante a criação de perfil. A média por transação é uma estimativa.  
    
-   Seção de Estatísticas de Contenção  
  
     Esta seção inclui uma tabela que mostra a contenção na tabela do banco de dados. Para saber mais sobre travas e bloqueios do banco de dados, confira Arquitetura de bloqueio. As colunas são apresentadas assim:  
  
    -   Porcentagem do total de esperas. O percentual de esperas de travas e bloqueios nessa tabela de banco de dados em comparação com a atividade do banco de dados. Quanto mais alto for esse percentual, mais intensa será a utilização da tabela em comparação com outras tabelas no banco de dados.  
  
    -   Estatísticas de Trava. Essas colunas registram o número de esperas de travas para consultas que envolvem essa tabela. Para saber mais sobre travas, confira Travamento. Quanto mais alto for esse número, mais contenção de trava haverá na tabela.  
  
    -   Estatísticas de Bloqueio. Esse grupo de colunas registra o número de aquisições de bloqueio de página e esperas para consultas para essa tabela. Para saber mais sobre bloqueios, confira Entendendo o bloqueio no SQL Server. Quanto mais esperas, maior a contenção de bloqueio na tabela.  
  
-   Seção Dificuldades de Migração  
  
     Esta seção inclui uma tabela que mostra a dificuldade de converter essa tabela de banco de dados em uma tabela com otimização de memória. Uma classificação de dificuldade mais alta indica mais dificuldade para converter a tabela. Para ver detalhes da conversão dessa tabela de banco de dados, use o Orientador de otimização da memória.  
  
As estatísticas de verificação e contenção no relatório de detalhes da tabela são coletadas e agregadas de sys.dm_db_index_operational_stats (Transact-SQL).  

### <a name="stored-procedures"></a>Procedimentos armazenados

 Um procedimento armazenado com alta taxa de tempo de CPU para o tempo decorrido é um candidato à migração. O relatório mostra todas as referências de tabela, pois os procedimentos armazenados compilados nativamente podem fazer referência apenas a tabelas com otimização de memória, que podem ser adicionadas ao custo de migração.  
  
 Os detalhes relatados para um procedimento armazenado consistem em duas seções:  
  
-   Seção de Estatísticas de Execução  
  
     Esta seção inclui uma tabela que mostra as estatísticas que foram coletadas sobre as execuções do procedimento armazenado. As colunas são apresentadas assim:  
  
    -   Tempo em Cache. O tempo que esse plano de execução permanece em cache. Se o procedimento armazenado for removido do cache de plano e reinserido, haverá tempos para cada cache.  
  
    -   Tempo Total de CPU. O tempo total de CPU que o procedimento armazenado consumiu durante a criação de perfil. Quanto mais alto for esse número, mais CPU o procedimento armazenado usou.  
  
    -   Tempo total de execução. A quantidade total de tempo de execução que o procedimento armazenado usou durante a criação de perfil. Quanto mais alta for a diferença entre esse número e o tempo de CPU, menos eficiente será o procedimento armazenado usando a CPU.  
  
    -   Total de Erros de Cache. O número de erros de cache (leituras de armazenamento físico) provocados pelas execuções do procedimento armazenado durante a criação de perfil.  
  
    -   Contagem de Execuções. O número de vezes em que esse procedimento armazenado foi executado durante a criação de perfil.  
  
-   Seção Referências de Tabela  
  
     Esta seção inclui uma tabela que mostra as tabelas às quais esse procedimento armazenado se refere. Antes da conversão do procedimento armazenado em um procedimento armazenado compilado nativamente, todas essas tabelas devem ser convertidas em tabelas com otimização de memória e devem permanecer no mesmo servidor e banco de dados.  
  
 As estatísticas de Execução no relatório de detalhes de procedimento armazenado são coletadas e agregadas de sys.dm_exec_procedure_stats (Transact-SQL). As referências são obtidas de sys.sql_expression_dependencies (Transact-SQL).  
  
 Para ver os detalhes sobre como converter um procedimento armazenado em um procedimento armazenado compilado nativamente, use o Native Compilation Advisor.  
  
## <a name="generating-in-memory-oltp-migration-checklists"></a>Geração de listas de verificação de migração de OLTP in-memory  
 Listas de verificação de migração identificam qualquer tabela ou recursos de procedimento armazenado que não têm suporte com tabelas com otimização de memória ou procedimentos armazenados compilados nativamente. A otimização da memória e os consultores de compilação nativa podem gerar uma lista de verificação para uma única tabela com base em disco ou procedimento armazenado T-SQL interpretado. Também é possível gerar listas de verificação de migração para várias tabelas e procedimentos armazenados em um banco de dados.  
  
 Você pode gerar uma lista de verificação de migração no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando o comando **Gerar Listas de Verificação de Migração do OLTP in-memory** ou usando o PowerShell.  
  
**Para gerar uma lista de verificação de migração usando o comando de interface de usuário**  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse em um banco de dados diferente do banco de dados do sistema, clique em **Tarefas**e clique em **Gerar Listas de Verificação de Migração de OLTP in-memory**.  
  
2.  Na caixa de diálogo Gerar Lista de Verificação de Migração do OLTP in-memory, clique em Avançar para navegar até a página **Configurar Opções de Geração de Lista de Verificação** . Nessa página, faça o seguinte.  
  
    1.  Insira um caminho para a pasta na caixa **Salvar lista de verificação em** .  
  
    2.  Verifique se **Gerar listas de verificação para tabela e procedimentos armazenados específicos** está selecionado.  
  
    3.  Expanda os nós **Tabela** e **Procedimento Armazenado** na caixa de seção.  
  
    4.  Selecione alguns objetos na caixa de seleção.  
  
3.  Clique em **Avançar** e confirme se a lista de tarefas corresponde às configurações na página **Configurar Opções de Geração de Lista de Verificação** .  
  
4.  Clique em **Concluir**e confirme a geração da lista de verificação de migração somente para os objetos selecionados.  
  
 Você pode verificar a precisão dos relatórios comparando-os com os relatórios gerados pela ferramenta Orientador de otimização da memória e pela ferramenta Native Compilation Advisor. Para obter mais informações, consulte [Memory Optimization Advisor](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md) e [Native Compilation Advisor](../../relational-databases/in-memory-oltp/native-compilation-advisor.md).  
  
**Para gerar uma lista de verificação de migração usando o SQL Server PowerShell**  
  
1.  No **Pesquisador de Objetos**, clique em um banco de dados e clique em **Iniciar PowerShell**. Verifique se o prompt a seguir é exibido.  
  
    ```  
    PS SQLSERVER: \SQL\{Instance Name}\DEFAULT\Databases\{two-part DB Name}>  
    ```  
  
2.  Digite o comando a seguir.  
  
    ```  
    Save-SqlMigrationReport –FolderPath “<folder_path>”  
    ```  
  
3.  Verifique o seguinte.  
  
    -   O caminho da pasta é criado, caso ainda não exista.  
  
    -   O relatório da lista de verificação de migração é gerado para todas as tabelas e procedimentos armazenados no banco de dados, e o relatório está no local especificado por folder_path.  
  
**Para gerar uma lista de verificação de migração usando o Windows PowerShell**  
  
1.  Inicie uma sessão do Windows PowerShell com privilégios elevados.  
  
2.  Digite os seguintes comandos. O objeto pode ser uma tabela ou um procedimento armazenado.  
  
    ```  
    [System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SqlServer.SMO')  
  
    ```  
  
    ```  
    Save-SqlMigrationReport –Server "<instance_name>" -Database "<db_name>" -FolderPath "<folder_path1>"  
  
    ```  
  
    ```  
    Save-SqlMigrationReport –Server "<instance_name>" -Database "<db_name>" -Object <object_name> -FolderPath "<folder_path2>"  
  
    ```  
  
3.  Verifique o seguinte.  
  
    -   Um relatório da lista de verificação de migração é gerado para todas as tabelas e procedimentos armazenados no banco de dados, e o relatório está no local especificado por folder_path.  
  
    -   Um relatório de lista de verificação de migração para <nome_do_objeto> é o único relatório no local especificado por folder_path2.  
  
## <a name="see-also"></a>Consulte Também  
 [Migrando para OLTP na memória](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
