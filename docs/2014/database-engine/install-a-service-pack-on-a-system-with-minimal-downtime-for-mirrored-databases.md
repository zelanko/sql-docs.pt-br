---
title: Instalar um Service Pack em um sistema com tempo de inatividade mínimo para bancos de dados espelhados | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- hotfixes [SQL Server]
- database mirroring [SQL Server], upgrading system
- rolling upgrades [SQL Server]
- service packs [SQL Server]
- upgrading mirrored database systems
- upgrading SQL Server, mirrored databases
ms.assetid: bdc63142-027d-4ead-9d3e-147331387ef5
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 821fd05e94ac820dff50bd08c70c75e7e9cc653d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62779590"
---
# <a name="install-a-service-pack-on-a-system-with-minimal-downtime-for-mirrored-databases"></a>Instalar um service pack em um sistema com tempo de inatividade mínimo para bancos de dados espelhados
  Este tópico descreve como minimizar o tempo de inatividade para bancos de dados espelhados ao instalar service packs e hotfixes. Esse processo envolve atualizar sequencialmente as instâncias do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] que estão participando do espelhamento de banco de dados. Essa forma de atualização, o que é conhecida como um *atualização sem interrupção*, reduz o tempo de inatividade para um único failover. Observe que para sessões em modo de alto desempenho em que o servidor espelho está geograficamente distante do servidor principal, uma atualização sem interrupção pode ser inadequada.  
  
 A atualização sem interrupção é um processo de vários estágios que consiste no seguinte:  
  
-   Proteção de seus dados.  
  
-   Se a sessão incluir uma testemunha, recomendamos a remoção da testemunha. Caso contrário, quando a instância do servidor espelho estiver sendo atualizada, a disponibilidade do banco de dados dependerá da testemunha que permanece conectada à instância do servidor principal. Depois que você remover uma testemunha, poderá atualizá-la a qualquer momento durante o processo de atualização sem interrupção sem arriscar o tempo de inatividade do banco de dados.  
  
    > [!NOTE]  
    >  Para obter mais informações, confira [Quorum: Como uma testemunha afeta a disponibilidade do banco de dados &#40;Espelhamento de Banco de Dados&#41;](database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).  
  
-   Se uma sessão estiver sendo executada em modo de alto desempenho, altere o modo operacional para o modo de segurança alta.  
  
-   Atualize cada instância de servidor que esteja envolvida no espelhamento de banco de dados. Uma atualização sem interrupção envolve a atualização da instância do servidor, que é atualmente o servidor espelho, executando o failover manual de cada um de seus bancos de dados espelhados e atualizando a instância do servidor que era o servidor principal (e é agora o novo servidor espelho). Neste momento, é necessário retomar o espelhamento.  
  
    > [!NOTE]  
    >  Antes de iniciar uma atualização sem interrupção, é recomendável a execução de um failover manual em, pelo menos, uma das sessões de espelhamento.  
  
-   Reverta para o modo de alto desempenho, se for necessário.  
  
-   Retorne a testemunha para a sessão de espelhamento, se for necessário.  
  
 Os procedimentos para esses estágios são descritos aqui.  
  
> [!IMPORTANT]  
>  Uma instância do servidor pode estar executando diferentes funções de espelhamento (servidor principal, servidor espelho ou testemunha) nas sessões de espelhamento simultâneas. Nesse caso, é preciso adaptar o processo básico de atualização sem interrupção na mesma proporção.  
  
### <a name="to-protect-your-data-before-an-update-a-best-practice"></a>Para proteger os dados antes de uma atualização (uma prática recomendada)  
  
1.  Execute um backup de banco de dados completo em todos os bancos de dados principais.  
  
     **Para fazer o backup de um banco de dados**  
  
    -   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
2.  Execute o comando [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) em todos os bancos de dados principais.  
  
### <a name="to-remove-a-witness-from-a-session"></a>Para remover uma testemunha de uma sessão  
  
1.  Se a sessão de espelhamento envolver uma testemunha, é recomendável a remoção da testemunha antes de executar uma atualização sem interrupção.  
  
     **Para remover a testemunha**  
  
    -   [Remover a testemunha de uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring/remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
### <a name="to-change-a-session-from-high-performance-mode-to-high-safety-mode"></a>Para alterar uma sessão em modo de alto desempenho para modo de segurança alta  
  
1.  Se a sessão de espelhamento estiver sendo executada em modo de alto desempenho, antes de executar uma atualização sem interrupção, altere o modo operacional para segurança alta sem failover automático. Use um dos métodos a seguir:  
  
    -   No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]: Alterar o **modo de operação** opção para **alta segurança sem failover automático (síncrono)** usando o [página espelhamento](../relational-databases/databases/database-properties-mirroring-page.md) do **banco de dados Propriedades** caixa de diálogo. Para obter informações sobre como acessar essa página, consulte [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](database-mirroring/start-the-configuring-database-mirroring-security-wizard.md).  
  
    -   No [!INCLUDE[tsql](../includes/tsql-md.md)]: Definir a segurança da transação como FULL. Para obter mais informações, consulte [Alterar a segurança da transação em uma sessão de espelhamento de banco de dados &#40;Transact-SQL&#41;](database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md).  
  
### <a name="to-perform-the-rolling-update"></a>Para executar a atualização sem interrupção  
  
1.  Para minimizar o tempo de inatividade, recomendamos o seguinte: Inicie a atualização sem interrupção atualizando qualquer parceiro de espelhamento é atualmente o servidor espelho em todas as suas sessões de espelhamento. Pode ser necessário atualizar várias instâncias do servidor neste momento.  
  
    > [!NOTE]  
    >  Uma testemunha pode ser atualizada em qualquer ponto do processo de atualização sem interrupção. Por exemplo, se uma instância de servidor for um servidor de espelho na sessão 1 e uma testemunha na sessão 2, você pode atualizar a instância do servidor agora.  
  
     A instância do servidor a ser atualizada primeiro depende da configuração atual de suas sessões de espelhamento, da seguinte maneira:  
  
    -   Se qualquer instância do servidor já for o servidor espelho em todas as suas sessões de espelhamento, instale o service pack ou o hotfix nessa instância do servidor.  
  
    -   Se todas as suas instâncias de servidor forem atualmente o servidor principal em quaisquer sessões de espelhamento, selecione uma instância de servidor para atualizar primeiro. Em seguida, execute manualmente um failover em cada um dos bancos de dados principais e atualize essa instância instalando o service pack ou hotfix.  
  
     Depois de atualizada, a instância do servidor reingressa automaticamente em cada uma das sessões de espelhamento.  
  
     **Para executar um failover manual**  
  
    -   [Executar failover manualmente de uma sessão de espelhamento de banco de dados &#40;SQL Server Management Studio&#41;](database-mirroring/manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   [Executar failover manualmente em uma sessão de espelhamento de banco de dados &#40;Transact-SQL&#41;](database-mirroring/manually-fail-over-a-database-mirroring-session-transact-sql.md).  
  
     Para obter informações sobre como funciona o failover manual, veja [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md).  
  
2.  Em cada sessão de espelhamento cuja instância do servidor espelho acabou de ser atualizada, aguarde a sessão ser sincronizada. Depois, conecte-se à instância do servidor principal e execute o failover manual na sessão. No failover, a instância do servidor atualizada torna-se o servidor principal dessa sessão, e o servidor principal antigo torna-se o servidor espelho.  
  
     O objetivo dessa etapa é que outra instância do servidor torne-se o servidor espelho em cada sessão de espelhamento na qual é um parceiro.  
  
3.  Depois de executar o failover, recomendamos a execução do comando [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) no banco de dados principal.  
  
4.  Instale o service pack ou o hotfix em cada instância do servidor que seja agora o servidor espelho, em todas as sessões de espelhamento na qual seja um parceiro. Pode necessário atualizar vários servidores nesse momento.  
  
    > [!IMPORTANT]  
    >  Em uma configuração de espelhamento complexa, algumas instâncias do servidor podem ainda ser o servidor principal original em uma ou mais sessões de espelhamento. Repita as etapas 2 a 4 para essas instâncias do servidor até que todas as instâncias envolvidas sejam atualizadas.  
  
5.  Continue a sessão de espelhamento.  
  
    > [!NOTE]  
    >  Failover automático não funcionará até que a testemunha tiver sido atualizada.  
  
6.  Instale os service packs ou hotfixes nas instâncias do servidor restantes que sejam a testemunha em todas as suas sessões de espelhamento. Depois que uma testemunha atualizada reingressar em uma sessão de espelhamento, o failover automático será possível novamente. Pode necessário atualizar vários servidores nesse momento.  
  
### <a name="to-return-a-session-to-high-performance-mode"></a>Para retornar a uma sessão em modo de alto desempenho  
  
1.  Opcionalmente, retorne ao modo de alto desempenho usando um dos seguintes métodos:  
  
    -   No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]: Alterar o **modo de operação** opção para **alto desempenho (assíncrono)** usando o [página espelhamento](../relational-databases/databases/database-properties-mirroring-page.md) do **propriedades de banco de dados**caixa de diálogo.  
  
    -   No [!INCLUDE[tsql](../includes/tsql-md.md)]: Use [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring) para definir a segurança da transação como OFF.  
  
### <a name="to-return-a-witness-to-a-mirroring-session"></a>Para retornar a testemunha a uma sessão de espelhamento  
  
1.  Opcionalmente, em modo de segurança alta, restabeleça a testemunha para cada sessão de espelhamento.  
  
     **Para restabelecer a testemunha**  
  
    -   [Adicionar ou substituir uma testemunha de espelhamento de banco de dados &#40;SQL Server Management Studio&#41;](database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
    -   [Adicionar uma testemunha de espelhamento de banco de dados usando a Autenticação do Windows &#40;Transact-SQL&#41;](database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
## <a name="see-also"></a>Consulte também  
 [Espelhamento de banco de dados ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring/database-mirroring-sql-server.md)   
 [Modos de operação de espelhamento de banco de dados](database-mirroring/database-mirroring-operating-modes.md)   
 [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Exibir o estado de um banco de dados espelhado &#40;SQL Server Management Studio&#41;](database-mirroring/view-the-state-of-a-mirrored-database-sql-server-management-studio.md)  
  
  
