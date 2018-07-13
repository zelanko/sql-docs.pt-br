---
title: Restaurações por etapas (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- partial updates [SQL Server]
- staged restores [SQL Server]
- piecemeal restores [SQL Server]
- restoring [SQL Server], piecemeal restore scenario
ms.assetid: 208f55e0-0762-4cfb-85c4-d36a76ea0f5b
caps.latest.revision: 73
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a9f42180f42071d53bcb3754e29baaee3b6bc82d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37182863"
---
# <a name="piecemeal-restores-sql-server"></a>Restaurações por etapas (SQL Server)
  Este tópico é relevante apenas para os bancos de dados na edição Enterprise do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contêm vários arquivos ou grupos de arquivos. No modelo simples, ele é relevante apenas para grupos de arquivos somente leitura.  
  
 Para obter informações sobre a restauração por etapas e as tabelas com otimização de memória, consulte [Restauração por etapas de bancos de dados com tabelas com otimização de memória](../in-memory-oltp/memory-optimized-tables.md).  
  
 A*restauração por etapas* permite que os bancos de dados que contêm vários grupos de arquivos sejam restaurados e recuperados em etapas. A restauração por etapas envolve uma série de sequências de restauração, iniciando com o grupo de arquivos primário e, em alguns casos, com um ou mais grupos de arquivos secundários. A restauração por etapas mantém verificações para garantir que o banco de dados será consistente no final. Depois que a sequência de restauração é concluída, os arquivos recuperados, se forem válidos e consistentes com o banco de dados, poderão ser colocados online diretamente.  
  
 A restauração por etapas trabalha com todos os modelos de recuperação, mas é mais flexível para os modelos completo e bulk-logged, do que para o modelo simples.  
  
 Toda restauração por etapas inicia com uma sequência inicial de restauração chamada de *sequência de restauração parcial*. No mínimo, a sequência de restauração parcial restaura e recupera o grupo de arquivos primário e, no modelo simples de recuperação, todos os grupos de arquivos de leitura/gravação. Durante a sequência de restauração por etapas, o banco de dados inteiro precisa estar offline. Depois disso, o banco de dados ficará online e os grupos de arquivos restaurados estarão disponíveis. No entanto, quaisquer grupos de arquivos não restaurados permanecerão offline e não serão acessíveis. No entanto, quaisquer grupos de arquivos offline poderão ser restaurados e colocados online mais tarde por uma restauração de arquivo.  
  
 Independentemente do modelo de recuperação usado pelo banco de dados, a sequência de restauração parcial inicia com uma instrução RESTORE DATABASE que restaura um backup completo e especifica a opção PARTIAL. A opção PARTIAL sempre inicia uma nova restauração por etapas; portanto, você deve especificar PARTIAL só uma vez na instrução inicial da sequência de restauração parcial. Quando a sequência de restauração parcial termina e o banco de dados é colocado online, o estado dos arquivos restantes ficam em "recuperação pendente" porque a sua recuperação foi adiada.  
  
 Subsequentemente, uma restauração por etapas tipicamente inclui uma ou mais sequências de restauração que são chamadas *sequências de restauração de grupos de arquivos*. Você pode esperar para executar uma sequência de restauração de grupos de arquivos específica o quanto quiser. Cada sequência de restauração de grupos de arquivos restaura e recupera um ou mais grupos de arquivos offline a um ponto consistente com o banco de dados. O tempo e número de sequências de restauração de grupos de arquivos dependem de sua meta de recuperação, o número de grupos de arquivos offline que você quer restaurar, e quantos deles você vai restaurar por sequência de restauração de grupos de arquivos.  
  
 Os requisitos exatos para executar uma restauração por etapas dependem do modelo de recuperação do banco de dados. Para obter mais informações, veja "Restauração por etapas no modelo de recuperação simples" e "Restauração por etapas no modelo de recuperação completo", adiante neste tópico.  
  
## <a name="piecemeal-restore-scenarios"></a>Cenários de restauração por etapas  
 Todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dão suporte a restauração por etapas offline. Na edição Enterprise, uma restauração por etapas pode ser online ou offline. As implicações de restauração por etapas offline são as seguintes:  
  
-   Cenário de restauração por etapas offline  
  
     Em uma restauração por etapas offline, o banco de dados ficará online após a sequência de restauração parcial. Os grupos de arquivos que ainda não foram restaurados permanecem offline, mas eles podem ser restaurados quando você precisar deles, depois colocar o banco de dados offline.  
  
-   Cenário de restauração por etapas online  
  
     Em uma restauração por etapas online, após a sequência de restauração parcial, o banco de dados está online e o grupo de arquivos primário e quaisquer grupos de arquivos secundários recuperados estão disponíveis. Os grupos de arquivos que ainda não foram restaurados permanecem offline, mas eles podem ser restaurados quando você precisar deles, enquanto o banco de dados permanecer online.  
  
     Restaurações por etapas online podem envolver transações adiadas. Quando apenas um subconjunto de grupos de arquivos foi restaurado, as transações no banco de dados que dependem de grupos de arquivos online podem ser adiadas. Isso é normal, porque o banco de dados inteiro deve ser consistente. Para obter mais informações, veja [Transações adiadas &#40;SQL Server&#41;](deferred-transactions-sql-server.md).  
  
-   [!INCLUDE[hek_1](../../includes/hek-1-md.md)] cenários de restauração por etapas  
  
     Para obter informações sobre Restaurações por Etapas de bancos de dados OLTPin-memory, consulte [Backup e restauração por etapas de bancos de dados com tabelas com otimização de memória](../in-memory-oltp/memory-optimized-tables.md).  
  
## <a name="restrictions"></a>Restrictions  
 Se uma sequência de restauração parcial excluir qualquer grupo de arquivos [FILESTREAM](../blob/filestream-sql-server.md) , não haverá suporte para a restauração pontual. Você pode forçar a sequência de restauração a continuar. Contudo, os grupos de arquivos FILESTREAM omitidos de sua instrução RESTORE nunca poderão ser restaurados. Para forçar uma restauração pontual, especifique a opção CONTINUE_AFTER_ERROR juntamente com a opção STOPAT, STOPATMARK ou STOPBEFOREMARK, que você também deve especificar nas instruções RESTORE LOG subsequentes. Se você especificar CONTINUE_AFTER_ERROR, a sequência de restauração parcial terá êxito e o grupo de arquivos FILESTREAM se tornará irrecuperável.  
  
## <a name="piecemeal-restore-under-the-simple-recovery-model"></a>Restauração por etapas no modelo de recuperação simples  
 No modelo de recuperação simples, a sequência de restauração por etapas deve iniciar com um banco de dados completo ou um backup parcial. Então, se o backup restaurado for uma base diferencial, restaure o último backup diferencial a seguir.  
  
 Durante a primeira sequência de restauração parcial, se você restaurar apenas um subconjunto de grupos de arquivos de leitura/gravação, quaisquer grupos de arquivos não restaurados estarão expirados quando você recuperar o banco de dados parcialmente restaurado. Omitir um grupo de arquivos de leitura/gravação da sequência de restauração parcial só é apropriado nos seguintes casos:  
  
-   Você quer que os grupos de arquivos não restaurados se tornem expirados.  
  
-   A sequência de restauração chegará a um ponto de recuperação no qual cada grupo de arquivos não restaurado tornou-se somente leitura, cancelado ou expirado (durante uma restauração anterior na sequência de restauração parcial).  
  
-   O backup completo foi realizado enquanto o banco de dados estava usando o modelo de recuperação simples, mas o ponto de recuperação é no momento que o banco de dados estiver usando o modelo de recuperação completa. Para obter mais informações, consulte "Executando uma restauração por etapas de um banco de dados cujo modelo de recuperação foi trocado de simples para completo", adiante neste tópico.  
  
### <a name="requirements-for-piecemeal-restore-under-the-simple-recovery-model"></a>Requisitos para uma restauração por etapas no modelo de recuperação simples  
 No modelo de recuperação simples, a fase inicial restaura e recupera o grupo de arquivos primário e todos os grupos de arquivos de leitura/gravação secundários. Depois que a fase inicial é concluída, os arquivos recuperados, se forem válidos e consistentes com o banco de dados, poderão ser colocados online diretamente.  
  
 Depois disso, os grupos de arquivos somente leitura podem ser restaurados em uma ou mais fases adicionais.  
  
 A restauração por etapas só estará disponível para um grupo de arquivos secundário somente leitura caso os seguinte itens sejam verdadeiros:  
  
-   Era somente leitura quando o backup foi realizado.  
  
-   Permaneceu somente leitura (mantendo-o logicamente consistente com o grupo de arquivos primário).  
  
 Para executar uma restauração por etapas, estas diretrizes devem ser seguidas:  
  
-   Um conjunto completo de backups para a restauração por etapas de um modelo de recuperação simples banco de dados deve conter o seguinte:  
  
    -   Um backup de banco de dados parcial ou completo que contenha o grupo de arquivos primário e todos os grupos de arquivos, que eram leitura/gravação na hora do backup.  
  
    -   Um backup de cada arquivo somente leitura.  
  
-   Para o backup de um arquivo somente leitura ser consistente com o grupo de arquivos primário, os grupos de arquivos secundários deveriam permanecer somente leitura desde que o backup foi realizado até que o backup que contém o grupo de arquivos primário tenha sido concluído. Você pode usar backups de arquivos diferenciais, se eles foram realizados depois que os grupos de arquivos tornaram-se somente leitura.  
  
### <a name="piecemeal-restore-stages-simple-recovery-model"></a>Fases da restauração por etapas (modelo de recuperação simples)  
 O cenário da restauração por etapas envolve as seguintes fases:  
  
-   Fase inicial (restaura e recupera o grupo de arquivos primário e todos os grupos de arquivos de leitura/gravação)  
  
     A fase inicial executa uma restauração parcial. A sequência parcial de restauração restaura o grupo de arquivos primário, todos os grupos secundários de arquivos leitura/gravação, e (opcionalmente) alguns grupos de arquivos somente leitura. Durante a fase inicial, o banco de dados inteiro deve ir offline. Depois da fase inicial, o banco de dados estará online, e os grupos de arquivos restaurados estarão disponíveis. Entretanto, quaisquer grupos de arquivos somente leitura que ainda não tiverem sido restaurados, permanecerão offline.  
  
     A primeira instrução RESTORE da fase inicial deve fazer o seguinte:  
  
    -   Usar um backup de banco de dados parcial ou completo que contenha o grupo de arquivos primário e todos os grupos de arquivos que eram leitura/gravação na hora do backup. É comum iniciar uma sequência de restauração parcial restaurando um backup parcial.  
  
    -   Especifique a opção PARTIAL, que indica o início de uma restauração por etapas.  
  
    > [!NOTE]  
    >  A opção PARTIAL executa verificações de segurança que garantem que o banco de dados resultante seja adequado para uso como um banco de dados de produção.  
  
    -   Especifique a opção READ_WRITE_FILEGROUPS se o backup for um backup de banco de dados completo.  
  
-   Enquanto o banco de dados estiver online, você pode usar uma ou mais restaurações de arquivo online para restaurar e recuperar arquivos offline somente leitura que eram somente leitura na hora do backup. A hora da restauração do arquivo online depende de quando você quer ter os dados online.  
  
     Dependendo do seguinte, você precisará restaurar dados a um arquivo:  
  
    -   Arquivos somente leitura válidos, que estão consistentes com o banco de dados podem ser colocados online diretamente pela recuperação, sem restaurar quaisquer dados.  
  
    -   Arquivos que estão danificados ou inconsistentes com o banco de dados devem ser restaurados antes de serem recuperados.  
  
### <a name="examples"></a>Exemplos  
  
-   [Exemplo: restauração por etapas de banco de dados &#40;Modelo de recuperação simples&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação simples&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
## <a name="piecemeal-restore-under-the-full-recovery-model"></a>Restauração por etapas no modelo de recuperação completa  
 No modelo de recuperação completa ou bulk-logged, a restauração por etapas está disponível para qualquer banco de dados que contenha vários grupos de arquivo, e você pode restaurar um banco de dados para qualquer ponto especificado. A sequência de restauração por etapas se comporta assim:  
  
-   sequência de restauração parcial  
  
     A sequência de restauração parcial restaura o grupo de arquivos primário e, opcionalmente alguns dos grupos de arquivos secundários.  
  
     A primeira instrução RESTORE DATABASE na fase inicial deve fazer o seguinte:  
  
    -   Especificar a opção PARTIAL. Isso indica o início de uma restauração por etapas.  
  
    -   Use qualquer backup de banco de dados completo que contenha o grupo de arquivos primário. A prática comum é iniciar uma sequência de restauração parcial restaurando um backup parcial.  
  
    -   Para restaurar a um ponto específico no tempo, você deve especificar a hora na sequência de restauração parcial. Todas as etapas seguintes da sequência de restauração devem mencionar o mesmo ponto especificado.  
  
-   Sequências de restauração de grupo de arquivos trazem grupos de arquivos online adicionais para um ponto consistente com o banco de dados.  
  
     Na edição Enterprise, qualquer grupo de arquivos secundário offline pode ser restaurado e recuperado enquanto o banco de dados permanecer online. Se um arquivo somente leitura específico não for danificado e for consistente com o banco de dados, o arquivo não terá de ser restaurado. Para obter mais informações, veja [Recuperar um banco de dados sem restaurar dados &#40;Transact-SQL&#41;](recover-a-database-without-restoring-data-transact-sql.md).  
  
### <a name="applying-log-backups"></a>Aplicando backups de log   
 Se um grupo de arquivos somente leitura era somente leitura desde antes de o backup de arquivo ser criado, aplicar backups de log ao grupo de arquivos será desnecessário e é ignorado pela restauração de arquivo. Se o grupo de arquivos for leitura/gravação, uma cadeia ininterrupta de backups de log deve ser aplicada à última restauração completa ou diferencial, para trazer o grupo de arquivos para o arquivo de log atual.  
  
### <a name="examples"></a>Exemplos  
  
-   [Exemplo: restauração por etapas de banco de dados &#40;Modelo de recuperação completa&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação completa&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
## <a name="performing-a-piecemeal-restore-of-a-database-whose-recovery-model-has-been-switched-from-simple-to-full"></a>Para obter mais informações, consulte "Executando uma restauração por etapas de um banco de dados cujo modelo de recuperação foi trocado de simples para completo", adiante neste tópico.  
 Você pode executar uma restauração por etapas de um banco de dados que foi trocado do modelo de recuperação simples para o modelo de recuperação completa, a partir do backup de banco de dados completo ou parcial. Por exemplo, considere um banco de dados para o qual você executa as seguintes etapas:  
  
1.  Crie um backup parcial (backup_1) de um banco de dados modelo simples.  
  
2.  Depois de algum tempo, altere o modelo de recuperação para completo.  
  
3.  Crie um backup diferencial.  
  
4.  Comece a fazer backups de log.  
  
 Depois disso, a sequência seguinte é válida:  
  
1.  Uma restauração parcial omite alguns grupos de arquivos secundários.  
  
2.  Uma restauração diferencial seguida por qualquer outra restauração necessária.  
  
3.  Depois, uma restauração de arquivo de um grupo de arquivos de leitura/gravação secundário WITH NORECOVERY do backup parcial, backup_1  
  
4.  O backup diferencial seguido por quaisquer outros backups que foram restaurados pela sequência de restauração por etapas original, para restaurar os dados até o ponto de recuperação original.  
  
## <a name="see-also"></a>Consulte também  
 [Aplicar backups de log de transações &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [Visão geral de restauração e recuperação &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [Planejar e executar sequências de restauração &#40;Modelo de recuperação completa&#41;](plan-and-perform-restore-sequences-full-recovery-model.md)  
  
  
