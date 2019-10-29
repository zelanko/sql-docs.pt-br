---
title: Visão geral da restauração e recuperação (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring tables [SQL Server]
- backups [SQL Server], restore scenarios
- database backups [SQL Server], restore scenarios
- database restores [SQL Server]
- restoring [SQL Server]
- restores [SQL Server]
- table restores [SQL Server]
- restoring databases [SQL Server], about restoring databases
- database restores [SQL Server], scenarios
- accelerated database recovery
ms.assetid: e985c9a6-4230-4087-9fdb-de8571ba5a5f
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 9b034e43f918a0f6c198c29cf2f6618ba38638f8
ms.sourcegitcommit: e7c3c4877798c264a98ae8d51d51cb678baf5ee9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916070"
---
# <a name="restore-and-recovery-overview-sql-server"></a>Visão geral da restauração e recuperação (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Para recuperar um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma falha, um administrador de banco de dados precisa restaurar um conjunto de backups do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma sequência de restauração logicamente correta e significativa. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à restauração de dados de backups de um banco de dados inteiro, um arquivo de dados ou uma página de dados, como segue:  
  
-   O banco de dados (uma *restauração completa do banco de dados*)  
  
     Todo o banco de dados é restaurado e recuperado e o banco de dados fica offline durante as operações de restauração e recuperação.  
  
-   O arquivo de dados (uma *restauração de arquivo*)  
  
     Um arquivo de dados ou um conjunto de arquivos é restaurado e recuperado. Durante uma operação de restauração de arquivo, os grupos de arquivos que contêm os arquivos ficam automaticamente offline. Qualquer tentativa de acessar um grupo de arquivos offline gera um erro.  
  
-   A página de dados (uma *restauração de página*)  
  
     Você pode restaurar bancos de dados específicos por meio do modelo de recuperação completa ou do modelo de recuperação bulk-logged. As restaurações de página podem ser executadas em qualquer banco de dados, seja qual for o número de grupos de arquivos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o backup e a restauração funcionam em todos os sistemas operacionais com suporte. Para obter informações sobre os sistemas operacionais com suporte, veja [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md). Para obter informações sobre suporte para backups de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja a seção “Suporte de compatibilidade” de [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
##  <a name="RestoreScenariosOv"></a> Visão geral de cenários de restauração  
 Um *cenário de restauração* no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é o processo de restauração de dados de um ou mais backups seguida da recuperação do banco de dados. Os cenários de restauração com suporte dependem do modelo de recuperação do banco de dados e da versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A tabela abaixo descreve os possíveis cenários de restauração que têm suporte para diversos modelos de recuperação.  
  
|cenário de restauração|Modelo de recuperação simples|Modelos de recuperação completa e com log de operações em massa|  
|----------------------|---------------------------------|----------------------------------------------|  
|restauração completa do banco de dados|Esta é a estratégia básica de restauração. Uma restauração completa do banco de dados pode envolver simplesmente a restauração e recuperação do backup completo do banco de dados. Alternativamente, uma restauração completa do banco de dados pode envolver a restauração do banco de dados completo seguida pela restauração e recuperação de um backup diferencial.<br /><br /> Para obter mais informações, veja [Restaurações completas de banco de dados &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md).|Esta é a estratégia básica de restauração. Uma restauração completa do banco de dados envolve a restauração de um backup completo do banco e, opcionalmente, de um backup diferencial (se houver), seguida da restauração de todos os backups de logs subsequentes (em sequência). A restauração completa do banco de dados termina com a recuperação do último backup de log e também com sua restauração (RESTORE WITH RECOVERY).<br /><br /> Para obter mais informações, veja [Restaurações completas de banco de dados &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md).|  
|File restore **\***|Restaura um ou mais arquivos somente leitura danificados, sem restaurar todo o banco de dados. A restauração de arquivo só estará disponível se o banco de dados tiver pelo menos um grupo de arquivos somente leitura.|Restaura um ou mais arquivos, sem restaurar todo o banco de dados. A restauração de arquivo pode ser executada enquanto o banco de dados estiver offline ou, em algumas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], enquanto o banco de dados permanece online. Durante uma restauração de arquivo, os grupos de arquivos que contêm os arquivos que estão sendo restaurados sempre estão offline.|  
|restauração de página|Não aplicável|Restaura uma ou mais páginas danificadas. A restauração de página pode ser executada enquanto o banco de dados estiver offline ou, em algumas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], enquanto o banco de dados permanece online. Durante uma restauração de página, as páginas que estão sendo restauradas sempre estão offline.<br /><br /> Uma cadeia ininterrupta de backups de log deve estar disponível, inclusive o arquivo de log atual, e todos eles devem ser aplicados para atualizar a página com o arquivo de log atual.<br /><br /> Para obter mais informações, veja [Restaurar páginas &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md).|  
|Restauração por etapas **\***|Restaura e recupera o banco de dados em fases no nível do grupo de arquivos, iniciando com o grupo de arquivos primário e todos os grupos de arquivos de gravação/leitura secundários.|Restaura e recupera o banco de dados em fases no nível do grupo de arquivos, iniciando com o grupo de arquivos primário.<br /><br /> Saiba mais em [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)|  
  
 **\*** Há suporte para a restauração online somente na edição Enterprise.  

### <a name="steps-to-restore-a-database"></a>Etapas de restauração de um banco de dados
Para executar uma restauração de arquivo, o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] executa duas etapas: 

-   Criação de todos os arquivos de banco dados ausentes.

-   Cópia dos dados dos dispositivos de backup para os arquivos do banco de dados.

Para executar uma restauração do banco de dados, o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] executa três etapas: 

-   Criação de arquivos do banco de dados e de log de transações, caso ainda não existam.

-   Cópia de todos os dados, log e páginas de índice da mídia de backup de um banco de dados para os arquivos do banco de dados. 

-   Aplicação do log de transações no que é conhecido como [processo de recuperação](#TlogAndRecovery).

 Independentemente de como os dados são restaurados, antes que um banco de dados possa ser recuperado, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] garante que todo o banco de dados é logicamente consistente. Por exemplo, se você restaurar um arquivo, não poderá recuperá-lo e colocá-lo online enquanto ele não for rolado para frente o suficiente para estar consistente com o banco de dados.  
  
### <a name="advantages-of-a-file-or-page-restore"></a>Vantagens de uma restauração de arquivo ou página  
 A restauração e recuperação de arquivos ou páginas, ao invés de todo o banco de dados, oferece as seguintes vantagens:  
  
-   Restaurar menos dados diminui o tempo necessário para copiar e recuperar o banco de dados.  
  
-   No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a restauração de arquivos ou páginas pode permitir que outros dados no banco de dados permaneçam online durante a operação de restauração.  

## <a name="TlogAndRecovery"></a> Log de transações e recuperação
Para a maioria dos cenários de restauração, é necessário aplicar um backup de log de transações e permitir que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] execute o **processo de recuperação** para que o banco de dados fique online. A recuperação é o processo usado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada banco de dados iniciar em um estado transacional consistente ou limpo.

Caso ocorra um failover ou outro desligamento não limpo, os bancos de dados poderão ser deixados em um estado em que algumas modificações nunca foram gravadas do cache do buffer para os arquivos de dados, e poderá haver algumas modificações de transações incompletas nos arquivos de dados. Quando uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciada, ela executa uma recuperação de cada banco de dados, que consiste em três fases, com base no último [ponto de verificação do banco de dados](../../relational-databases/logs/database-checkpoints-sql-server.md):

-   A **Fase de análise** verifica o log de transações para determinar qual é o último ponto de verificação e cria a DPT (Tabela de página suja) e a ATT (Tabela de transação ativa). A DPT contém registros de páginas que estavam sujas no momento em que o banco de dados foi desligado. A ATT contém registros de transações que estavam ativas no momento em que o banco de dados não foi desligado corretamente.

-   A **Fase refazer** encaminha todas as modificações registradas no log que podem não ter sido gravadas nos arquivos de dados no momento em que o banco de dados foi desligado. O [número de sequência de log mínimo](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#minlsn) (minLSN) necessário para uma recuperação bem-sucedida em todo o banco de dados é encontrado na DPT e marca o início das operações refazer necessárias em todas as páginas sujas. Nessa fase, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] grava em disco todas as páginas sujas que pertencem a transações confirmadas.

-   A **Fase desfazer** reverte transações incompletas encontradas na ATT para garantir que a integridade do banco de dados seja preservada. Depois da reversão, o banco de dados fica online e mais nenhum backup de log de transações pode ser aplicado ao banco de dados.

As informações sobre o andamento de cada estágio de recuperação do banco de dados são registradas no [log de erros](../../tools/configuration-manager/viewing-the-sql-server-error-log.md) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O progresso da recuperação do banco de dados também pode ser acompanhado usando eventos estendidos. Saiba mais na postagem do blog [Novos eventos estendidos para o progresso da recuperação do banco de dados](https://blogs.msdn.microsoft.com/sql_server_team/new-extended-events-for-database-recovery-progress/).

> [!NOTE]
> Em um cenário de restauração por etapas, se o status de um grupo de arquivos for somente leitura desde antes de o backup de arquivo ser criado, aplicar backups de log ao grupo de arquivos será desnecessário e será ignorado pela restauração de arquivo. 

<a name="FastRecovery"></a>
> [!NOTE]
> Para maximizar a disponibilidade do bancos de dados em um ambiente corporativo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition poderá disponibilizar um banco de dados online após a fase refazer e enquanto a fase desfazer ainda estiver em execução. Isso é conhecido como Recuperação Rápida.

##  <a name="RMsAndSupportedRestoreOps"></a> Modelos de recuperação e operações de restauração com suporte  
 As operações de restauração disponíveis para um banco de dados dependem de seu modelo de recuperação. A tabela abaixo resume se e qual extensão cada um dos modelos de recuperação suporta um determinado cenário de restauração.  
  
|Operação de restauração|Modelo de recuperação completa|Modelo de recuperação bulk-logged|Modelo de recuperação simples|  
|-----------------------|-------------------------|---------------------------------|---------------------------|  
|Recuperação de dados|Recuperação completa (se o log estiver disponível).|Exposição a alguma perda de dados.|Quaisquer dados desde o último backup completo ou diferencial serão perdidos.|  
|Restauração em um momento determinado|Qualquer período coberto pelos backups de log.|Não permitido se o backup de log contiver quaisquer alterações com log de alteração em massa.|Sem suporte.|  
|File restore **\***|Suporte completo.|Às vezes. **\*\***|Disponível só para arquivos secundários somente leitura.|  
|Page restore **\***|Suporte completo.|Às vezes. **\*\***|Nenhum.|  
|Restauração por etapas (nível de grupo de arquivos) **\***|Suporte completo.|Às vezes. **\*\***|Disponível só para arquivos secundários somente leitura.|  
  
 **\*** Disponível somente na edição Enterprise do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 **\*\*** Para saber as condições exigidas, consulte [Restrições de restauração no modelo de recuperação simples](#RMsimpleScenarios), posteriormente neste tópico.  
  
> [!IMPORTANT]  
> Independentemente do modelo de recuperação de um banco de dados, um backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode ser restaurado por uma versão do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que seja mais antiga do que a versão que criou o backup.  
  
## <a name="RMsimpleScenarios"></a> Cenários de restauração no modelo de recuperação simples  
 O modelo de recuperação simples impõe as seguintes restrições em operações de restauração:  
  
-   Restauração de arquivo e restauração por etapas estão disponíveis apenas para grupos de arquivos secundários somente leitura. Para obter informações sobre esses cenários de restauração, veja [Restaurações de arquivos &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md) e [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md).  
  
-   A restauração de página não é permitida.  
  
-   A restauração point-in-time não é permitida.  
  
 Se quaisquer dessas restrições forem impróprias para suas necessidades de recuperação, recomendamos que você considere o uso do modelo de recuperação completa. Para obter mais informações, veja [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
> [!IMPORTANT]  
> Independentemente do modelo de recuperação de um banco de dados, um backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode ser restaurado por uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que seja mais antiga do que a versão que criou o backup.  
  
##  <a name="RMblogRestore"></a> Restauração no modelo de recuperação bulk-logged  
 Esta seção aborda as considerações de restauração que são específicas do modelo de recuperação bulk-logged, que deve ser usado exclusivamente como complemento para o modelo de recuperação completa.  
  
> [!NOTE]  
> Para obter uma introdução ao modelo de recuperação bulk-logged, veja [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
 Geralmente, o modelo de recuperação bulk-logged é semelhante ao modelo de recuperação completa e as informações descritas para o modelo de recuperação completa também se aplicam a ambos. Porém, a recuperação pontual e a restauração online são afetadas pelo modelo de recuperação bulk-logged.  
  
### <a name="restrictions-for-point-in-time-recovery"></a>Restrições para recuperação pontual  
 Se um backup de log feito no modelo de recuperação bulk-logged contiver alterações, a recuperação pontual não será permitida. Tentar executar a recuperação pontual em um backup de log que contenha alterações em massa leva à falha na operação de restauração.  
  
### <a name="restrictions-for-online-restore"></a>Restrições para restauração online  
 Uma sequência de restauração online funciona apenas se as seguintes condições forem atendidas:  
  
-   Todos os backups de log exigidos devem ter sido feitos antes do início da sequência de restauração.  
  
-   Os backups de alterações em massa devem ser feitos antes do início da sequência de restauração online.  
  
-   Se houver alterações em massa no banco de dados, todos os arquivos deverão estar online ou [extintos](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md). (Isso significa que já não faz parte do banco de dados.)  
  
 Se essas condições não forem atendidas, haverá falha na sequência de restaurações online.  
  
> [!NOTE]  
>  Recomenda-se passar para o modelo de recuperação completa antes de iniciar uma restauração online. Para obter mais informações, veja [Modelos de recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
 Para obter informações sobre como executar uma restauração online, veja [Restauração online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md).  
  
##  <a name="DRA"></a> Orientador de recuperação de banco de dados (SQL Server Management Studio)  
O orientador de recuperação de banco de dados facilita a criação de planos de restauração que implementam sequências de restauração corretas. Muitos problemas conhecidos e aperfeiçoamentos de restauração de banco de dados solicitados pelos clientes foram resolvidos. Estes são os principais aperfeiçoamentos incorporados pelo orientador de recuperação de banco de dados:  
  
-   **Algoritmo do plano de restauração:**  o algoritmo usado para criar planos de restauração melhorou significativamente, particularmente em cenários de restauração complexos. Muitos casos extremos, inclusive cenários de bifurcação em restaurações pontuais, são tratados de forma mais eficiente do que nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Restaurações pontuais:**  o Assistente de Recuperação de Banco de Dados simplifica consideravelmente a restauração de um banco de dados em um determinado momento. Uma linha de tempo de backup visual aprimora significativamente o suporte a restaurações pontuais. Essa linha de tempo visual permite que você identifique um momento viável como ponto de recuperação de destino para a restauração de um banco de dados. A linha do tempo facilita a transposição de um caminho de recuperação bifurcado (um caminho que abrange bifurcações de recuperação). Um plano de restauração pontual inclui automaticamente os backups relevantes para a restauração do momento desejado (data e hora). Para obter mais informações, veja [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
Para obter mais informações, obtenha informações sobre o orientador de recuperação de banco de dados consultando os seguintes blogs sobre capacidade de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   [Assistente de Recuperação: Uma introdução](https://blogs.msdn.com/b/managingsql/archive/2011/07/13/recovery-advisor-an-introduction.aspx)  
  
-   [Assistente de Recuperação: Usando o SSMS para criar/restaurar backups divididos](https://blogs.msdn.com/b/managingsql/archive/2011/07/13/recovery-advisor-using-ssms-to-create-restore-split-backups.aspx)  

## <a name="adr"></a> Recuperação acelerada de banco de dados
A [recuperação acelerada do banco de dados](/azure/sql-database/sql-database-accelerated-database-recovery/) está disponível no [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. A recuperação acelerada de banco de dados melhora significativamente a disponibilidade do banco de dados, especialmente na presença de transações de execução prolongada, remodelando o [processo de recuperação](#TlogAndRecovery) do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Um banco de dados para o qual a recuperação acelerada do banco de dados foi habilitada conclui o processo de recuperação significativamente mais rápido após um failover ou outro desligamento não limpo. Quando habilitada, a recuperação acelerada do banco de dados também conclui a reversão de transações canceladas de longa execução muito mais rapidamente.

Para habilitar a recuperação acelerada do banco de dados por banco de dados em [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] use a seguinte sintaxe:

```sql
ALTER DATABASE <db_name> SET ACCELERATED_DATABASE_RECOVERY = ON;
```

> [!NOTE]
> A recuperação acelerada do banco de dados é habilitada por padrão em [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].

## <a name="RelatedContent"></a> Consulte também  
 [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)      
 [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)     
 [Guia de arquitetura e gerenciamento de log de transações do SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)     
 [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)     
 [Aplicar backups de log de transações (SQL Server)](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)    
