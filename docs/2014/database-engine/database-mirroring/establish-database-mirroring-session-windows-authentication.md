---
title: Estabelecer um sessão usando a autenticação do Windows (SQL Server Management Studio) de espelhamento de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], sessions
ms.assetid: 7cb418d6-dce1-4a0d-830e-9c5ccfe3bd72
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 70d9b3f9d243531e13d3d5a46693c80288815881
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62806894"
---
# <a name="establish-a-database-mirroring-session-using-windows-authentication-sql-server-management-studio"></a>Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows (SQL Server Management Studio)
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].  
  
 Para estabelecer uma sessão de espelhamento de banco de dados e modificar as propriedades de espelhamento de banco de dados para um banco de dados, use a página **Espelhamento** da caixa de diálogo **Propriedades de Banco de Dados** . Antes de usar a página **Espelhamento** para configurar o espelhamento de banco de dados, verifique se os requisitos a seguir foram atendidos:  
  
-   As instâncias de servidor espelho e principal devem estar sendo executadas na mesma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]– Standard ou Enterprise. Além disso, é altamente recomendável que elas sejam executadas em sistemas comparáveis que possam controlar cargas de trabalho idênticas.  
  
    > [!NOTE]  
    >  Uma instância de servidor testemunha não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
-   O banco de dados espelho deve existir e ser atual.  
  
     A criação de um banco de dados espelho requer a restauração de um backup recente do banco de dados principal (usando WITH NORECOVERY) na instância do servidor espelho. Requer também que, depois do backup completo, um ou mais backups de log sejam restaurados em sequência para o banco de dados espelho (usando WITH NORECOVERY). Para obter mais informações, consulte [Prepare a Mirror Database for Mirroring &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
-   Se as instâncias do servidor estiverem sendo executadas em contas de usuário de domínio diferentes, cada uma exigirá um logon no banco de dados **mestre** da outra. Se o logon não existir, você deverá criá-lo antes de configurar o espelhamento. Para obter mais informações, consulte [Permitir o acesso à rede a um ponto de extremidade de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server&#41;](../database-mirroring-allow-network-access-windows-authentication.md).  
  
### <a name="to-configure-database-mirroring"></a>Para configurar o espelhamento de banco de dados  
  
1.  Depois de se conectar à instância do servidor principal, no Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda os **Bancos de Dados**e selecione o banco de dados a ser espelhado.  
  
3.  Clique com o botão direito do mouse no banco de dados, selecione **Tarefas**e clique em **Espelhar**. Isso abre a página **Espelhamento** da caixa de diálogo **Propriedades do Banco de Dados** .  
  
4.  Para começar a configurar o espelhamento, clique no botão **Configurar Segurança** para iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados.  
  
    > [!NOTE]  
    >  Durante uma sessão de espelhamento de banco de dados você pode usar esse assistente só para adicionar ou alterar a instância do servidor testemunha.  
  
5.  A opção Assistente para Configurar Segurança de Espelhamento de Banco de Dados cria o ponto de extremidade de espelhamento de banco de dados (se não existir nenhum) em cada instância do servidor e insere os endereços de rede do servidor no campo correspondente à função da instância do servidor (**Principal**, **Espelho**ou **Testemunha**).  
  
    > [!IMPORTANT]  
    >  Ao criar um ponto de extremidade, o Assistente para Configurar Segurança de Espelhamento de Banco de Dados sempre usa a Autenticação do Windows. Antes de você poder usar o assistente com autenticação baseada em certificado, o ponto de extremidade do espelhamento deve ser configurado para usar certificados em cada uma das instâncias do servidor. Além disso, todos os campos da caixa de diálogo **Contas de Serviço** do assistente devem permanecer em branco. Para obter informações sobre como criar um ponto de extremidade de espelhamento de banco de dados para usar certificados, veja [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql).  
  
6.  Opcionalmente, altere o modo de operação. A disponibilidade de certos modos de operação depende da especificação de um endereço TCP para um servidor testemunha. As opções são as seguintes:  
  
    |Opção|Testemunha?|Explicação|  
    |------------|--------------|-----------------|  
    |**Alto desempenho (assíncrono)**|Nulo (se existir; não usado, mas a sessão requer um quorum)|Para maximizar o desempenho, o banco de dados espelho fica sempre um pouco atrás do banco de dados principal, nunca se aproximando muito. Porém, a lacuna entre os bancos de dados é geralmente pequena. A perda de um parceiro tem o seguinte efeito:<br /><br /> Se a instância do servidor espelho ficar indisponível, o principal continuará.<br /><br /> Se a instância do servidor principal ficar indisponível, o espelho irá parar; mas se a sessão não tiver um servidor testemunha (como recomendado) ou se o servidor testemunha estiver conectado ao servidor espelho, o servidor espelho ficará acessível como espera passiva e o proprietário do banco de dados poderá forçar o serviço para a instância do servidor espelho (com possível perda de dados).<br /><br /> <br /><br /> Para obter mais informações, consulte [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md).|  
    |**Alta segurança sem failover automático (síncrono)**|Não|Todas as transações confirmadas têm a garantia de serem gravadas em disco no servidor espelho.<br /><br /> O failover manual é possível quando os parceiros estão conectados um ao outro e o banco de dados está sincronizado. A perda de um parceiro tem o seguinte efeito:<br /><br /> Se a instância do servidor espelho ficar indisponível, o principal continuará.<br /><br /> Se a instância do servidor principal ficar indisponível o espelho irá parar, mas ficará acessível como espera passiva e o proprietário de banco de dados poderá forçar o serviço para a instância do servidor espelho (com possível perda de dados).<br /><br /> Para obter mais informações, consulte [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md).|  
    |**Alta segurança com failover automático (síncrono)**|Sim (obrigatório)|Todas as transações confirmadas têm a garantia de serem gravadas em disco no servidor espelho. A disponibilidade é maximizada incluindo uma instância do servidor testemunha para dar suporte ao failover automático. Observe que você só poderá selecionar a opção **Alta segurança com failover automático (síncrono)** se tiver especificado antes um endereço de um servidor testemunha. O failover manual é possível quando os parceiros estão conectados um ao outro e o banco de dados está sincronizado.<br /><br /> Na presença de um servidor testemunha, a perda de um parceiro tem o seguinte efeito:<br /><br /> -Se a instância do servidor principal ficar indisponível, ocorrerá failover automático. A instância do servidor espelho é alternada para a função principal e oferece seu banco de dados como banco de dados principal.<br /><br /> -Se a instância do servidor espelho ficar indisponível, o principal continuará.<br /><br /> Para obter mais informações, consulte [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md).<br /><br /> **\*\* Importante \*\*** Se o servidor testemunha estiver desconectado, os parceiros deverão estar conectados entre si para que o banco de dados fique disponível. Para obter mais informações, confira [Quorum: Como uma testemunha afeta a disponibilidade do banco de dados &#40;Espelhamento de Banco de Dados&#41;](quorum-how-a-witness-affects-database-availability-database-mirroring.md).|  
  
7.  Quando todas as seguintes condições existirem, clique em **Iniciar Espelhamento** para iniciar o espelhamento:  
  
    -   Você está atualmente conectado à instância do servidor principal.  
  
    -   A segurança foi configurada corretamente.  
  
    -   Os endereços TCP totalmente qualificados das instâncias do servidor principal e espelho estão especificados (na seção **Endereços de rede do servidor** ).  
  
    -   Se o modo de operação estiver definido como **Alta segurança com failover automático (síncrono)** , o endereço TCP totalmente qualificado da instância do servidor testemunha também será especificado.  
  
8.  Depois que o espelhamento começar, você poderá alterar o modo de operação e salvar a alteração clicando em **OK**. Observe que você pode alternar para o modo de segurança alta com failover automático apenas se tiver especificado primeiro um endereço de servidor testemunha.  
  
    > [!NOTE]  
    >  Para remover o servidor testemunha, exclua seu endereço de rede do campo **Testemunha** . Se você mudar do modo de alta segurança com failover automático para o modo de alto desempenho, o campo **Testemunha** será desmarcado automaticamente.  
  
## <a name="see-also"></a>Consulte também  
 [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)   
 [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)   
 [Propriedades do banco de dados &#40;página Espelhamento&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Pausar ou retomar uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](pause-or-resume-a-database-mirroring-session-sql-server.md)   
 [Configurar um banco de dados espelho para usar a propriedade confiável &#40;Transact-SQL&#41;](set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)   
 [Remover o espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Gerenciamento de logons e trabalhos após a troca de função &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)   
 [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](setting-up-database-mirroring-sql-server.md)   
 [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [Adicionar ou substituir uma testemunha de espelhamento de banco de dados &#40;SQL Server Management Studio&#41;](../database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
  
