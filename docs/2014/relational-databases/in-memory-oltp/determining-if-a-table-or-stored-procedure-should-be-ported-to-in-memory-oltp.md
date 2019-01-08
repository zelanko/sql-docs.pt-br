---
title: Determinando se uma tabela ou um procedimento armazenado deve ser movido para o OLTP in-memory | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- Analyze, Migrate, Report
- AMR
ms.assetid: c1ef96f1-290d-4952-8369-2f49f27afee2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de6a778f9cdbfb7ab916f40a5250ca4f9e20c811
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377488"
---
# <a name="determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp"></a>Determinando se uma tabela ou um procedimento armazenado deve ser movido para o OLTP na memória
  O coletor de desempenho de transação em [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ajuda você a avaliar se o OLTP na memória melhorará o desempenho do seu aplicativo de banco de dados. O relatório de análise de desempenho da transação também indica quanto trabalho você deverá executar para habilitar o OLTP na Memória no seu aplicativo. Depois de identificar uma tabela baseada em disco a ser transportada para o OLTP in-memory, você poderá usar o [Orientador de Otimização da Memória](memory-optimization-advisor.md)para ajudar na migração da tabela. De maneira semelhante, o [Native Compilation Advisor](native-compilation-advisor.md) o ajudará a transportar um procedimento armazenado para um procedimento armazenado compilado nativamente.  
  
 Este tópico descreverá como:  
  
-   Configurar o Data Warehouse de Gerenciamento.  
  
-   Configurar a coleta de dados.  
  
-   Gerar relatórios de análise de desempenho de transação para identificar tabelas críticas de desempenho e procedimentos armazenados.  
  
 Para obter informações sobre as metodologias de migração, confira [In-Memory OLTP – Common Workload Patterns and Migration Considerations](https://msdn.microsoft.com/library/dn673538.aspx)(OLTP in-memory – Padrões comuns de carga de trabalho e considerações de migração).  
  
 O coletor de desempenho da transação e os relatórios de análise de desempenho da transação o ajudam a realizar as seguintes tarefas:  
  
-   Analisar sua carga de trabalho para determinar se o OLTP na memória melhorará o desempenho. O coletor de desempenho da transação coleta e avalia as características de desempenho de sua carga de trabalho. para obter informações sobre a ferramenta de configuração e recursos adicionais. Em seguida, o relatório de análise de desempenho da transação recomenda as tabelas e os procedimentos armazenados que serão mais beneficiados com a conversão em OLTP na memória.  
  
-   Ajudar você a planejar e executar a migração para o OLTP na memória. O caminho de migração de uma tabela com base em disco para uma tabela com otimização de memória pode ser demorado. O Orientador de Otimização da Memória o ajuda a identificar as incompatibilidades na tabela que você deve remover antes de movê-la para o OLTP na memória. O Orientador de Otimização em Memória também ajuda a entender o impacto que a migração de uma tabela para uma tabela com otimização de memória terá no seu aplicativo.  
  
     Você poderá verificar se seu aplicativo pode se beneficiar do OLTP na memória, quando desejar planejar a migração para o OLTP na memória e sempre que trabalhar para migrar alguma de suas tabelas e os procedimentos armazenados para o OLTP na memória.  
  
    > [!IMPORTANT]  
    >  O desempenho de um sistema de banco de dados depende de vários fatores e nem todos podem ser observados e medidos pelo coletor de desempenho da transação. Portanto, o relatório de análise de desempenho da transação não garante que os ganhos de desempenho reais corresponderão a essas previsões, caso elas sejam feitas.  
  
 O coletor de desempenho de transação e a capacidade de gerar um relatório de análise de desempenho da transação são instalados quando você seleciona **ferramentas de gerenciamento-Basic** ou **ferramentas de gerenciamento-avançadas** Quando você instala [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
## <a name="best-practices"></a>Práticas recomendadas  
 O fluxo de trabalho recomendado é ilustrado no fluxograma a seguir. Os nós amarelos representam os procedimentos opcionais:  
  
 ![Fluxo de trabalho da AMR](../../database-engine/media/amr-1.gif "fluxo de trabalho da AMR")  
  
 Você pode usar qualquer método para estabelecer uma linha de base de desempenho, incluindo, entre outros, usar logs do contador de desempenho ou o Monitor de Atividade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. As informações a serem usadas na linha de base de desempenho e nas comparações são:  
  
-   Consumo de CPU do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Consumo de memória do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Atividade de E/S do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Taxa de transferência de transações da instância durante o processamento de transações.  
  
 O coletor de desempenho da transação captura dados a cada 15 minutos. Para obter resultados utilizáveis, execute o coletor de desempenho da transação por, pelo menos, uma hora. Para obter os melhores resultados, execute o coletor de desempenho da transação pelo tempo necessário para capturar dados de seus cenários primários. Gere um relatório de análise de desempenho da transação somente depois de concluir a coleta de dados.  
  
 Configure o coletor de desempenho da transação para ser executado na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em produção e colete os dados em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no ambiente de desenvolvimento (teste) para garantir uma sobrecarga mínima. Para obter informações sobre como salvar dados em um banco de dados do Data Warehouse de gerenciamento em um controle remoto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da instância, consulte [configurar a coleta de dados em uma instância remota do SQL Server](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md#xxx).  
  
## <a name="performance-impacts"></a>Impactos do desempenho  
 O coletor de desempenho da transação consiste em dois conjuntos de coleta de dados:  
  
-   Análise de uso da tabela  
  
-   Análise do procedimento armazenado  
  
 Os conjuntos de coletas coletam dados de três exibições de gerenciamento dinâmico (DMV) a cada quinze minutos e carregam os dados no banco de dados configurado para atuar como Data Warehouse de Gerenciamento. O carregamento dos dados coletados resulta em um impacto mínimo no desempenho.  
  
## <a name="use-the-transaction-performance-collector"></a>Usar o coletor de desempenho da transação  
 As seguintes etapas exigem o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
> [!IMPORTANT]  
>  Não altere o esquema (por exemplo, para adicionar ou remover bancos de dados ou criar ou remover tabelas) durante a criação de perfil. Se você alterar o esquema de um banco de dados durante a coleta de dados, o banco de dados talvez não seja incluído com precisão no relatório.  
  
### <a name="configure-management-data-warehouse"></a>Configurar o Data Warehouse de Gerenciamento  
 O data warehouse de gerenciamento deve ser configurado para usar o coletor de desempenho da transação.  
  
 A versão da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sobre a qual você coletará dados (perfil) deve ser a mesma versão ou mais antiga do que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] onde o Data Warehouse de Gerenciamento está configurado.  
  
1.  No Pesquisador de Objetos, expanda **Gerenciamento**.  
  
2.  Clique com botão direito **coleta de dados** e selecione **tarefas** e, em seguida, **configurar Data Warehouse de gerenciamento**. O **Assistente Configurar o gerenciamento de Data Warehouse** começa.  
  
3.  Clique em **próxima** para selecionar o banco de dados que atuará como o Data Warehouse de gerenciamento.  
  
4.  Clique em **New** para criar um novo banco de dados para manter os dados de perfil. Depois de terminar de criar o banco de dados, clique em **próxima** no assistente.  
  
5.  A próxima etapa do assistente permite adicionar usuários e logons. Você pode mapear logons para associações de função da instância do MDW. Isso não é necessário para coletar dados da instância local. Se não estiver coletando dados da instância local, você poderá conceder a associação de função de banco de dados `mdw_admin` à conta que executará transações cujo perfil está sendo criado. Quando terminar, clique em **próxima**.  
  
6.  Verifique se o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent está em execução.  
  
7.  Na próxima tela, clique em **concluir** para sair do assistente.  
  
### <a name="configure-data-collection-on-a-local-includessnoversionincludesssnoversion-mdmd-instance"></a>Configurar a coleta de dados em uma instância local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 A coleta de dados exige que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agente seja iniciado. Você só precisará configurar um coletor de dados em um servidor.  
  
 Um coletor de dados pode ser configurado em um SQL Server 2012 ou versão posterior do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Para configurar a coleta de dados para carregar um banco de dados do Data Warehouse de Gerenciamento na mesma instância,  
  
1.  Na **Pesquisador de objetos**, expanda **Management**.  
  
2.  Clique com botão direito **coleta de dados**, selecione **tarefas**e então **configurar a coleta de dados**. O **Assistente para configurar coleta de dados** começa.  
  
3.  Clique em **próxima** para selecionar o banco de dados que coletará os dados de perfil.  
  
4.  Selecione a instância atual do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e um banco de dados do Data Warehouse de Gerenciamento nessa instância.  
  
5.  Na caixa rotulada **selecionar conjuntos de Coletores de dados você deseja habilitar**, selecione **conjuntos de coleta de desempenho de transação**. Clique em **próxima** quando terminar.  
  
6.  Verifique as seleções. Clique em **volta** para modificar as configurações. Clique em **Concluir** quando tiver terminado.  
  
###  <a name="xxx"></a> Configurar a coleta de dados em um controle remoto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância  
 A coleta de dados exige que o Agente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] seja iniciado na instância que coletará os dados.  
  
 Um coletor de dados pode ser configurado em um SQL Server 2012 ou versão posterior do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 É necessário um proxy do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent estabelecido com a credencial correta para que o coletor de dados carregue os dados em um banco de dados do Data Warehouse de Gerenciamento em uma instância que seja diferente de onde as transações serão analisadas. Para habilitar um proxy do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent, primeiramente é preciso estabelecer uma credencial com um logon habilitado para domínio. O logon habilitado para domínio deve ser um membro do grupo `mdw_admin` do banco de dados do Data Warehouse de Gerenciamento. Consulte [como: Criar uma credencial (SQL Server Management Studio)](../security/authentication-access/create-a-credential.md) para obter informações sobre como criar uma credencial.  
  
 Para configurar a coleta de dados para carregar um banco de dados do Data Warehouse de Gerenciamento em outra instância,  
  
1.  Na instância que contém os objetos com base em disco que você deseja migrar para o OLTP na memória, expanda o **gerenciamento** nó no Pesquisador de objetos.  
  
2.  Clique com botão direito **coleta de dados** e selecione **tarefas** e, em seguida, **configurar a coleta de dados**. O **Assistente para configurar coleta de dados** começa.  
  
3.  Clique em **próxima** para selecionar o banco de dados que coletará os dados de perfil.  
  
4.  Verifique se um banco de dados do Data Warehouse de Gerenciamento existe em outra instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
5.  Selecione outra instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e um banco de dados do Data Warehouse de Gerenciamento nessa instância.  
  
     A versão da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sobre a qual você coletará dados (perfil) deve ser a mesma versão ou mais antiga do que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] onde o Data Warehouse de Gerenciamento está configurado.  
  
6.  Na caixa rotulada **selecionar conjuntos de Coletores de dados você deseja habilitar**, selecione **conjuntos de coleta de desempenho de transação**.  
  
7.  Selecione **Use uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proxy de agente para carregamentos remotos**.  
  
8.  Clique em **próxima** quando terminar.  
  
9. Selecione o proxy.  
  
     Se desejar criar um novo proxy do Agente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)],  
  
    1.  Clique em **New** para exibir o **nova conta Proxy** caixa de diálogo.  
  
    2.  No **nova conta Proxy** caixa de diálogo, insira o nome do proxy, selecione a credencial e, opcionalmente, insira uma descrição. Em seguida, clique em **entidades**.  
  
    3.  Clique em **Add** e selecione **Msdb** função.  
  
    4.  Selecione `dc_proxy` e clique em **Okey**. Em seguida, clique em **Okey** novamente.  
  
     Depois que o proxy correto for selecionado, clique em **próxima**.  
  
10. Para configurar conjuntos de coleta do sistema, verifique **conjuntos de coleta do sistema** e clique em **próxima**.  
  
11. Verifique as seleções. Clique em **volta** para modificar as configurações. Clique **concluir** quando terminar.  
  
 Os conjuntos de coleta de dados agora devem estar configurados e em execução na sua instância.  
  
### <a name="generate-reports"></a>Gerar relatórios  
 Você pode gerar relatórios de análise de desempenho de transação com o botão direito clicando em banco de dados do Data Warehouse de gerenciamento e selecionando **relatórios**, em seguida, **Data Warehouse de gerenciamento**e então **Visão geral da análise de desempenho de transação**.  
  
 O relatório coleta informações sobre todos os bancos de dados do usuário no servidor de carga de trabalho. Se seu banco de dados MDW (Data Warehouse de Gerenciamento) estiver no computador local, você verá o(s) banco de dado(s) do MDW no relatório.  
  
 Um procedimento armazenado com alta taxa de tempo de CPU para o tempo decorrido é um candidato à migração. O relatório mostra todas as referências de tabela, pois os procedimentos armazenados compilados nativamente podem fazer referência apenas a tabelas com otimização de memória, que podem ser adicionadas ao custo de migração.  
  
 Os detalhes relatados para uma tabela consistem em três seções:  
  
-   Seção Estatísticas de Verificação  
  
     Esta seção inclui uma única tabela que mostra as estatísticas que foram coletadas sobre verificações na tabela do banco de dados. As colunas são:  
  
    -   Percentual de total de acessos. O percentual de verificações e pesquisas nesta tabela em relação à atividade do banco de dados inteiro. Quanto mais alto for esse percentual, mais intensa será a utilização da tabela em comparação com outras tabelas no banco de dados.  
  
    -   Estatísticas de Pesquisa/Estatísticas de Verificação do Intervalo. Essa coluna registra o número de pesquisas de ponto e de verificações de intervalo (verificações de índice e de tabela) realizadas na tabela durante a criação de perfil. A média por transação é uma estimativa.  
  
    -   Ganho de Interoperabilidade e Ganho Nativo. Essas colunas calculam a quantidade de benefícios de desempenho uma pesquisa de ponto ou a verificação de intervalo teria se a tabela fosse convertida em uma tabela com otimização de memória.  
  
-   Seção de Estatísticas de Contenção  
  
     Esta seção inclui uma tabela que mostra a contenção na tabela do banco de dados. Para obter mais informações sobre banco de dados de travas e bloqueios, consulte [arquitetura de bloqueio](https://msdn.microsoft.com/library/aa224738\(v=sql.80\).aspx). As colunas são apresentadas assim:  
  
    -   Porcentagem do total de esperas. O percentual de esperas de travas e bloqueios nessa tabela de banco de dados em comparação com a atividade do banco de dados. Quanto mais alto for esse percentual, mais intensa será a utilização da tabela em comparação com outras tabelas no banco de dados.  
  
    -   Estatísticas de Trava. Essas colunas registram o número de esperas de travas para consultas que envolvem essa tabela. Para obter informações sobre travas, consulte [travamento](https://msdn.microsoft.com/library/aa224727\(v=SQL.80\).aspx). Quanto mais alto for esse número, mais contenção de trava haverá na tabela.  
  
    -   Estatísticas de Bloqueio. Esse grupo de colunas registra o número de aquisições de bloqueio de página e esperas para consultas para essa tabela. Para obter mais informações sobre bloqueios, consulte [Noções básicas sobre bloqueio no SQL Server](https://msdn.microsoft.com/library/aa213039\(v=SQL.80\).aspx). Quanto mais esperas, maior a contenção de bloqueio na tabela.  
  
-   Seção Dificuldades de Migração  
  
     Esta seção inclui uma tabela que mostra a dificuldade de converter essa tabela de banco de dados em uma tabela com otimização de memória. Uma classificação de dificuldade mais alta indica mais dificuldade para converter a tabela. Para ver os detalhes da conversão dessa tabela de banco de dados, use o [orientador de otimização de memória](memory-optimization-advisor.md).  
  
 Estatísticas de verificação e contenção no relatório de detalhes da tabela são coletadas e agregadas de [DM db_index_operational_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql).  
  
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
  
 Estatísticas de execução do relatório de detalhes de procedimento armazenado são coletadas e agregadas de [DM exec_procedure_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql). As referências são obtidas [sys. sql_expression_dependencies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql).  
  
 Para ver os detalhes sobre como converter um procedimento armazenado em um procedimento armazenado nativamente compilado, use o [Native Compilation Advisor](native-compilation-advisor.md).  
  
## <a name="see-also"></a>Consulte também  
 [Migrando para OLTP na memória](migrating-to-in-memory-oltp.md)  
  
  
