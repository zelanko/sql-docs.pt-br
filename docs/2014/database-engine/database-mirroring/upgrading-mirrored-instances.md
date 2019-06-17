---
title: Minimizar o tempo de inatividade para bancos de dados espelhados ao atualizar instâncias de servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading SQL Server, rolling upgrade of mirrored databases
- database mirroring [SQL Server], upgrading system
- rolling upgrades [SQL Server]
ms.assetid: 0e73bd23-497d-42f1-9e81-8d5314bcd597
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 857e18b1b956d3d8c9d2fc4c5692dbf022bf85fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754270"
---
# <a name="minimize-downtime-for-mirrored-databases-when-upgrading-server-instances"></a>Minimizar o tempo de inatividade de bancos de dados espelhados ao atualizar instâncias do servidor
  Ao atualizar instâncias de servidor [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você pode reduzir o tempo de inatividade para cada banco de dados espelho para apenas um único failover manual executando uma atualização em sequência, conhecida como uma *atualização sem interrupção*. Uma atualização sem-interrupção consiste em um processo de várias etapas que, em sua forma mais simples, envolve atualizar a instância do servidor que funciona como o servidor espelho de uma sessão de espelhamento, executar o failover manual no banco de dados espelho, atualizar o antigo servidor principal e continuar o espelhamento. Na prática, o processo exato dependerá do modo de operação e do número e do layout de sessões de espelhamento em execução nas instâncias do servidor que você está atualizando.  
  
> [!NOTE]  
>  Para obter informações sobre como executar uma atualização sem interrupção para instalar um service pack ou hotfix, consulte [instalar um Service Pack em um sistema com tempo de inatividade mínimo para bancos de dados espelhado](../install-a-service-pack-on-a-system-with-minimal-downtime-for-mirrored-databases.md).  
  
 **Preparação recomendada (práticas recomendadas)**  
  
 Antes de iniciar uma atualização sem-interrupção, é recomendável:  
  
1.  Executar um failover manual em pelo menos uma das sessões de espelhamento:  
  
    -   [Executar failover manualmente de uma sessão de espelhamento de banco de dados &#40;SQL Server Management Studio&#41;](manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   [Executar failover manualmente em uma sessão de espelhamento de banco de dados &#40;Transact-SQL&#41;](manually-fail-over-a-database-mirroring-session-transact-sql.md).  
  
    > [!NOTE]  
    >  Para obter informações sobre como funciona o failover manual, veja [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md).  
  
2.  Proteger seus dados:  
  
    1.  Executar um backup de banco de dados completo em todos os bancos de dados principais:  
  
         [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
    2.  Execute o comando [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) em todos os bancos de dados principais.  
  
 **Estágios de uma atualização sem interrupção**  
  
 As etapas específicas de uma atualização sem-interrupção dependem do modo de operação da configuração de espelhamento. No entanto, as etapas básicas são as mesmas.  
  
> [!NOTE]  
>  Para obter informações sobre os modos de operação, consulte [Modos de operação do Espelhamento de Banco de Dados](database-mirroring-operating-modes.md).  
  
 A ilustração a seguir é um fluxograma que mostra as etapas básicas de uma atualização sem-interrupção para cada modo de operação. Os procedimentos correspondentes estão descritos após a ilustração.  
  
 ![Fluxograma mostrando as etapas de uma atualização sem interrupção](../media/dbm-rolling-upgrade.gif "Flowchart showing steps of a rolling upgrade")  
  
> [!IMPORTANT]  
>  Uma instância do servidor pode estar executando diferentes funções de espelhamento (servidor principal, servidor espelho ou testemunha) nas sessões de espelhamento simultâneas. Nesse caso, é preciso adaptar o processo básico de atualização sem-interrupção na mesma proporção. Para obter mais informações, consulte [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md).  
  
### <a name="to-change-a-session-from-high-performance-mode-to-high-safety-mode"></a>Para alterar uma sessão em modo de alto desempenho para modo de segurança alta  
  
1.  Se a sessão de espelhamento estiver sendo executada em modo de alto desempenho, antes de executar a atualização sem-interrupção, altere o modo operacional para segurança alta sem failover automático.  
  
    > [!IMPORTANT]  
    >  Se o servidor espelho está geograficamente distante do servidor principal, uma atualização sem-interrupção pode ser inadequada.  
  
    -   Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: altere a opção **Modo de operação** para **Segurança alta sem failover automático (síncrono)** usando a [página Espelhamento](../../relational-databases/databases/database-properties-mirroring-page.md) da caixa de diálogo **Propriedades do Banco de Dados**. Para obter informações sobre como acessar essa página, consulte [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md).  
  
    -   Em [!INCLUDE[tsql](../../includes/tsql-md.md)]: defina a segurança de transações para FULL. Para obter mais informações, consulte [Alterar a segurança da transação em uma sessão de espelhamento de banco de dados &#40;Transact-SQL&#41;](change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)  
  
### <a name="to-remove-a-witness-from-a-session"></a>Para remover uma testemunha de uma sessão  
  
1.  Se a sessão de espelhamento envolver uma testemunha, recomendamos a remoção da testemunha antes de executar a atualização sem-interrupção. Caso contrário, quando a instância do servidor espelho estiver sendo atualizada, a disponibilidade do banco de dados dependerá da testemunha que permanece conectada à instância do servidor principal. Depois que remover uma testemunha, é possível atualizá-la a qualquer momento durante o processo de atualização sem-interrupção sem arriscar o tempo de inatividade do banco de dados.  
  
    > [!NOTE]  
    >  Para obter mais informações, confira [Quorum: Como uma testemunha afeta a disponibilidade do banco de dados &#40;Espelhamento de Banco de Dados&#41;](quorum-how-a-witness-affects-database-availability-database-mirroring.md).  
  
    -   [Remover a testemunha de uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
### <a name="to-perform-the-rolling-upgrade"></a>Para executar a atualização sem-interrupção  
  
1.  Para minimizar o tempo de inatividade, recomendamos o seguinte: inicie a atualização sem-interrupção atualizando qualquer parceiro de espelhamento que no momento seja o servidor espelho em todas as suas sessões de espelhamento. Pode ser necessário atualizar várias instâncias do servidor neste momento.  
  
    > [!NOTE]  
    >  Uma testemunha pode ser atualizada em qualquer ponto do processo de atualização sem-interrupção. Por exemplo, se uma instância do servidor for um servidor espelho na Sessão 1 e for uma testemunha na Sessão 2, será possível atualizar a instância do servidor agora.  
  
     A instância do servidor a ser atualizada primeiro depende da configuração atual de suas sessões de espelhamento, como a seguir:  
  
    -   Se qualquer instância de servidor já for o servidor espelho em todas as suas sessões de espelhamento, atualize a instância de servidor para a nova versão.  
  
    -   Se todas as instâncias de servidor forem atualmente o servidor principal em quaisquer sessões de espelhamento, selecione uma instância de servidor para atualizar primeiro. Em seguida, execute manualmente um failover em cada um de seus bancos de dados principais e atualize essa instância de servidor.  
  
     Depois de ser atualizada, a instância do servidor retoma automaticamente cada uma das sessões de espelhamento.  
  
2.  Em cada sessão de espelhamento cuja instância do servidor de espelho acabou de ser atualizada, aguarde a sessão ser sincronizada. Depois, conecte-se à instância do servidor principal e execute o failover manual na sessão. Em failover, a instância do servidor atualizada torna-se o servidor principal para aquela sessão e o servidor principal anterior torna-se o servidor espelho.  
  
     O objetivo dessa etapa é que outra instância do servidor torne-se o servidor espelho em cada sessão de espelhamento na qual é um parceiro.  
  
     **Restrições depois da execução de failover para uma instância de servidor atualizada.**  
  
     Depois de executar failover de uma instância de servidor anterior para uma instância do servidor do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , a sessão de banco de dados é suspensa. Ela não pode ser retomada até que o outro parceiro seja atualizado. Porém, o servidor principal ainda aceita conexões e permite acesso a dados e modificações no banco de dados principal.  
  
    > [!NOTE]  
    >  O estabelecimento de uma nova sessão de espelhamento exige que todas as instâncias de servidor estejam executando a mesma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Após o failover, é recomendável que você execute as [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) comando no banco de dados theprincipal.  
  
4.  Atualize cada instância de servidor que seja agora o servidor espelho em todas as sessões de espelhamento nas quais é um parceiro. Pode necessário atualizar vários servidores nesse momento.  
  
    > [!IMPORTANT]  
    >  Em uma configuração de espelhamento complexa, algumas instâncias do servidor podem ainda ser o servidor principal original em uma ou mais sessões de espelhamento. Repita as etapas 2 a 4 para essas instâncias do servidor até que todas as instâncias envolvidas sejam atualizadas.  
  
5.  Continue a sessão de espelhamento.  
  
    > [!NOTE]  
    >  O failover automático não funcionará até que a testemunha tenha sido atualizada e novamente adicionada à sessão de espelhamento.  
  
6.  Atualize qualquer instância de servidor restante que seja a testemunha em todas as suas sessões de espelhamento. Depois que uma testemunha atualizada voltar a uma sessão de espelhamento, o failover automático torna-se possível novamente. Pode necessário atualizar vários servidores nesse momento.  
  
### <a name="to-return-a-session-to-high-performance-mode"></a>Para retornar a uma sessão em modo de alto desempenho  
  
1.  Opcionalmente, retorne ao modo de alto desempenho usando um dos seguintes métodos:  
  
    -   Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: altere a opção **Modo de operação** para **Alto desempenho (assíncrono)** usando a [página Espelhamento](../../relational-databases/databases/database-properties-mirroring-page.md) da caixa de diálogo **Propriedades do Banco de Dados** .  
  
    -   Em [!INCLUDE[tsql](../../includes/tsql-md.md)]: use [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)para definir a segurança de transações como OFF.  
  
### <a name="to-add-a-witness-back-into-a-mirroring-session"></a>Para adicionar uma testemunha de volta a uma sessão de espelhamento  
  
1.  Opcionalmente, em modo de segurança alta, restabeleça a testemunha para cada sessão de espelhamento.  
  
     **Para retornar uma testemunha**  
  
    -   [Adicionar ou substituir uma testemunha de espelhamento de banco de dados &#40;SQL Server Management Studio&#41;](add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
    -   [Adicionar uma testemunha de espelhamento de banco de dados usando a Autenticação do Windows &#40;Transact-SQL&#41;](add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
## <a name="see-also"></a>Consulte também  
 [Espelhamento de banco de dados ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Exibir o estado de um banco de dados espelhado &#40;SQL Server Management Studio&#41;](view-the-state-of-a-mirrored-database-sql-server-management-studio.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Instalar um Service Pack em um sistema com tempo de inatividade mínimo para bancos de dados espelhados](../install-a-service-pack-on-a-system-with-minimal-downtime-for-mirrored-databases.md)   
 [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)   
 [Forçar o serviço em uma sessão de espelhamento de banco de dados &#40;Transact-SQL&#41;](force-service-in-a-database-mirroring-session-transact-sql.md)   
 [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Modos de operação do Espelhamento de Banco de Dados](database-mirroring-operating-modes.md)  
  
  
