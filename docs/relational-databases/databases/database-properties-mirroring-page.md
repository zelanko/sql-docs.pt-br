---
title: "Propriedades do banco de dados (página Espelhamento) | Microsoft Docs"
ms.custom: 
ms.date: 08/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.databaseproperties.mirroring.f1
ms.assetid: 5bdcd20f-532d-4ee6-b2c7-18dbb7584a87
caps.latest.revision: "86"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 47f75acd0677fb838304de87cd9216671d019131
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="database-properties-mirroring-page"></a>Propriedades do banco de dados (página Espelhamento)
  Acesse esta página do banco de dados principal e use-a para configurar e modificar as propriedades de espelhamento de banco de dados de um banco de dados. Nela é possível também iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados, exibir o status de uma sessão de espelhamento e pausar ou remover a sessão de espelhamento de banco de dados.  
  
> **IMPORTANTE!** A segurança deve ser configurada para você poder começar o espelhamento. Se o espelhamento não tiver sido iniciado, você deve começar usando o assistente. As caixas de texto da página **Espelhamento** ficam desabilitadas até que o assistente seja encerrado.  
  
 **Configurar o espelhamento de banco de dados usando o SQL Server Management Studio**  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
## <a name="options"></a>Opções  
 **Configurar Segurança**  
 Clique neste botão para iniciar o **Assistente para Configurar a Segurança de Espelhamento de Banco de Dados.**  
  
 Se o assistente for concluído com êxito, a ação tomada dependerá de o espelhamento já ter começado, conforme explicado a seguir:  
  
|||  
|-|-|  
|Se o espelhamento não tiver começado.|A página de propriedades armazena essas informações de conexão em cache e, além disso, armazena um valor em cache que indica se o banco de dados espelho tem a propriedade de parceiro definida.<br /><br /> Ao término do assistente, você é solicitado a iniciar o espelhamento de banco de dados usando os endereços de rede do servidor e o modo de operação padrão. Se precisar alterar os endereços ou o modo de operação, clique em **Não Iniciar o Espelhamento**.|  
|Se o espelhamento já tiver começado.|Se o servidor testemunha tiver sido alterado no assistente, será definido adequadamente.|  
  
 **Endereços de rede do servidor**  
 Existe uma opção equivalente para cada instância de servidor: **Principal**, **Espelho**e **Testemunha**.  
  
 Os endereços de rede do servidor das instâncias de servidor são especificados automaticamente quando você conclui o Assistente para Configurar Segurança de Espelhamento de Banco de Dados. Após concluir o assistente, você pode modificar os endereços de rede manualmente, se necessário.  
  
 O endereço de rede do servidor tem a seguinte sintaxe básica:  
  
 TCP**://***nome_domínio_totalmente_qualificado***:***porta*  
  
 onde  
  
-   *nome_domínio_totalmente_qualificado* é o servidor em que está localizada a instância de servidor.  
  
-   *porta* é a porta atribuída ao ponto de extremidade do espelhamento de banco de dados da instância de servidor.  
  
     Para participar do espelhamento de banco de dados, um servidor exige um ponto de extremidade de espelhamento de banco de dados. Quando você usa o Assistente para Configurar Segurança de Espelhamento de Banco de Dados para estabelecer a sessão de espelhamento para uma instância de servidor, o assistente cria o ponto de extremidade automaticamente e o configura para usar a Autenticação do Windows. Para obter informações sobre como usar o assistente com autenticação baseada em certificado, veja [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md).  
  
    >**IMPORTANTE:**  Cada instância de servidor requer somente um ponto de extremidade de espelhamento de banco de dados, independentemente do número de sessões de espelhamento que deverão receber suporte.  
  
 Por exemplo, para uma instância de servidor em um sistema de computador nomeado `DBSERVER9` cujo ponto de extremidade usa a porta `7022`, o endereço de rede poderia ser:  
  
```  
TCP://DBSERVER9.COMPANYINFO.ADVENTURE-WORKS.COM:7022  
```  
  
 Para obter mais informações, consulte [Especificar um endereço de rede do servidor &#40;Espelhamento de banco de dados&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md).  
  
> **OBSERVAÇÃO:** durante uma sessão de espelhamento de banco de dados, as instâncias de servidor principal e espelho não podem ser alteradas, ao contrário da instância de servidor testemunha. Para obter mais informações, consulte "Comentários", mais adiante neste tópico.  
  
 **Iniciar Espelhamento**  
 Clique para começar o espelhamento, quando todas as condições a seguir estiverem presentes:  
  
-   O banco de dados espelho deve existir.  
  
     Antes de poder iniciar o espelhamento, o banco de dados espelho deve ser criado recuperando um backup completo recente WITH NORECOVERY e, talvez, backups de log do banco de dados principal no servidor espelho. Para obter mais informações, consulte [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
-   Os endereços TCP das instâncias de servidor principal e espelho já foram especificados (na seção **Endereços de rede do servidor**).  
  
-   Se o modo de operação for definido como alta segurança com failover automático (síncrono), o endereço TCP da instância do servidor espelho também será especificado.  
  
-   A segurança foi configurada corretamente.  
  
 Clique em **Iniciar Espelhamento** para iniciar a sessão. O Mecanismo de Banco de Dados tenta conectar-se automaticamente ao parceiro espelho para verificar se o servidor espelho está configurado corretamente e inicia a sessão de espelhamento. Se o espelhamento puder ser iniciado, uma tarefa será criada para monitorar o banco de dados.  
  
 **Pausar** ou **Retomar**  
 Durante uma sessão de espelhamento de banco de dados, clique em **Pausar** para pausar a sessão. Um prompt pedirá confirmação; se você clicar em **Sim**, a sessão será pausada e o botão será alterado para **Retomar**. Para retomar a sessão, clique em **Retomar**.  
  
 Para obter informações sobre o impacto de pausar uma sessão, veja [Pausando e retomando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md).  
  
> **IMPORTANTE:** Após um serviço forçado, quando o servidor principal original for reconectado, o espelhamento será suspenso. A retomada do espelhamento nessa situação pode causar perda de dados no servidor principal original. Para obter informações sobre como gerenciar a perda de dados potencial, veja [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md).  
  
 **Remover Espelhamento**  
 Na instância de servidor principal, clique para parar a sessão e remover a configuração de espelhamento dos bancos de dados. Um prompt solicitará a confirmação; se você clicar em **Sim**, a sessão será interrompida e o espelhamento será removido. Para obter informações sobre o impacto da remoção do espelhamento de banco de dados, veja [Removendo o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
> **OBSERVAÇÃO:** se este for o único banco de dados espelhado na instância do servidor, o trabalho de monitor será removido.  
  
 **Failover**  
 Clique para fazer failover do banco de dados principal para o banco de dados espelho manualmente.  
  
> **OBSERVAÇÃO:** se a sessão de espelhamento estiver sendo executada em modo de alto desempenho, não haverá suporte para o failover manual. Para executar failover manualmente, é necessário alterar o modo de operação para **Alta segurança sem failover automático (síncrono)**. Após a conclusão do failover, você poderá alterar o modo de volta para **Alto desempenho (assíncrono)** na instância do novo servidor principal.  
  
 Um prompt solicita confirmação. Se você clicar em **Sim**, haverá uma tentativa de failover. O servidor principal começa tentando conectar-se ao servidor espelho usando a Autenticação do Windows. Se a Autenticação do Windows não funcionar, o servidor principal exibirá a caixa de diálogo **Conectar-se ao Servidor** . Se o servidor espelho usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selecione **Autenticação do SQL Server** na caixa **Autenticação** . Na caixa de texto **Logon** , especifique a conta de logon com a qual você se conectará no servidor espelho e, na caixa de texto **Senha** , especifique a senha da conta.  
  
 Se o failover for bem-sucedido, a caixa de diálogo **Propriedades do Banco de Dados** será fechada. As funções de servidor espelho e principal são alternadas: o banco de dados espelho anterior torna-se o banco de dados principal e vice-versa. Observe que a caixa de diálogo **Propriedades do Banco de Dados** torna-se indisponível no banco de dados principal antigo porque este se tornou o banco de dados espelho. Essa caixa de diálogo ficará disponível no novo banco de dados principal após o failover.  
  
 Se o failover falhar, uma mensagem de erro será exibida e a caixa de diálogo permanecerá aberta.  
  
> **IMPORTANTE:** Se você clicar em **Failover** depois de modificar as propriedades na caixa de diálogo **Propriedades do Banco de Dados** , essas alterações serão perdidas. Para salvar as alterações atuais, responda **Não** ao prompt de confirmação e clique em **OK** para salvá-las. Em seguida, abra novamente a caixa de diálogo de propriedades do banco de dados e clique em **Failover**.  
  
 **Modo de operação**  
 Opcionalmente, altere o modo de operação. A disponibilidade de alguns modos de operação depende de você ter especificado um endereço TCP para uma testemunha. As opções são as seguintes:  
  
|Opção|Testemunha?|Explicação|  
|------------|--------------|-----------------|  
|**Alto desempenho (assíncrono)**|Nulo (se existir; não usado, mas a sessão requer um quorum)|Para maximizar o desempenho, o banco de dados espelho fica sempre um pouco atrás do banco de dados principal, nunca se aproximando muito. Porém, a lacuna entre os bancos de dados é geralmente pequena. A perda de um parceiro tem o seguinte efeito:<br /><br /> Se a instância do servidor espelho ficar indisponível, o principal continuará.<br /><br /> Se a instância do servidor principal ficar indisponível, o espelhado continuará. Mas se a sessão não tiver nenhuma testemunha (como recomendado) ou a testemunha estiver conectada ao servidor espelho, este permanecerá acessível como uma espera passiva; o proprietário do banco de dados pode forçar um serviço para a instância do servidor espelho (com possível perda de dados).|  
|**Alta segurança sem failover automático (síncrono)**|Não|Todas as transações confirmadas têm a garantia de serem gravadas em disco no servidor espelho.<br /><br /> O failover manual será possível se os parceiros estiverem conectados entre si.<br /><br /> A perda de um parceiro tem o seguinte efeito:<br /><br /> Se a instância do servidor espelho ficar indisponível, o principal continuará.<br /><br /> Se a instância de servidor principal ficar indisponível, o espelhado será interrompido, mas ficará disponível como espera passiva e o proprietário do banco de dados poderá forçar o serviço para a instância do servidor espelho (com possível perda de dados).|  
|**Alta segurança com failover automático (síncrono)**|Sim (obrigatório)|Disponibilidade maximizada, incluindo uma instância de servidor testemunha para dar suporte ao failover automático. Observe que você só poderá selecionar a opção **Alta segurança com failover automático (síncrono)** se tiver especificado antes um endereço de um servidor testemunha.<br /><br /> O failover manual será possível se os parceiros estiverem conectados entre si.<br /><br /> **\*\* Importante \*\*** Se o servidor testemunha estiver desconectado, os parceiros deverão estar conectados entre si para que o banco de dados fique disponível. Para obter mais informações, consulte [Quorum: como uma testemunha afeta a disponibilidade do banco de dados &#40;Espelhamento de Banco de Dados&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).<br /><br /> Nos modos de operação síncronos, todas as transações confirmadas têm a garantia de serem gravadas em disco no servidor espelho. Na presença de um servidor testemunha, a perda de um parceiro tem o seguinte efeito:<br /><br /> Se a instância do servidor principal ficar indisponível, ocorrerá failover automático. A instância do servidor espelho é alternada para a função principal e oferece seu banco de dados como banco de dados principal.<br /><br /> Se a instância do servidor espelho ficar indisponível, o principal continuará.<br /><br /> <br /><br /> Para obter mais informações, consulte [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).|  
  
 Depois que o espelhamento começar, você poderá alterar o modo de operação e salvar a alteração clicando em **OK**.  
  
 Para obter informações sobre os modos de operação, veja [Modos de operação de espelhamento de banco de dados](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).  
  
 **Status**  
 Após o início do espelhamento, o painel **Status** exibirá o status da sessão de espelhamento de banco de dados a partir do momento em que você selecionou a página **Espelhamento** . Para atualizar o painel **Status** , clique no botão **Atualizar** . Os possíveis estados são os seguintes:  
  
|Estados|Explicação|  
|------------|-----------------|  
|**Este banco de dados não foi configurado para espelhamento**|Não existe nenhuma sessão de espelhamento de banco de dados e não há nenhuma atividade a ser reportada na página **Espelhamento** .|  
|**Em Pausa**|O banco de dados principal está disponível, mas não está enviando logs para o servidor espelho.|  
|**Nenhuma conexão**|A instância do servidor principal não pode conectar-se a seu parceiro.|  
|**Sincronizando**|O conteúdo do banco de dados espelho está ficando atrás do conteúdo do banco de dados principal. A instância do servidor principal está enviando registros de log para a instância do servidor espelho, a qual está aplicando as alterações ao banco de dados espelho para rolagem para frente.<br /><br /> No início de uma sessão de espelhamento de banco de dados, o banco de dados espelho e principal estão nesse estado.|  
|**Failover**|Na instância do servidor principal, foi iniciado um failover manual (troca de função) e o servidor atualmente está fazendo a transição na função espelho. Nesse estado, as conexões do usuário com o banco de dados principal são encerradas rapidamente e o banco de dados assume a função espelho logo em seguida.|  
|**Sincronizado**|Quando o servidor espelho torna-se suficientemente atualizado em relação ao servidor principal, o estado do banco de dados é alterado para **Sincronizado**. O banco de dados permanece nesse estado enquanto o servidor principal continua enviando alterações para o servidor espelho e o servidor espelho continua aplicando as alterações ao banco de dados espelho.<br /><br /> No modo de alta segurança, o failover é possível, sem qualquer perda de dados.<br /><br /> No modo de alto desempenho, alguma perda de dados é sempre possível, mesmo no estado **Sincronizado**.|  
  
 Para obter mais informações, veja [Estados de espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md).  
  
 **Atualizar**  
 Clique para atualizar a caixa **Status** .  
  
## <a name="remarks"></a>Comentários  
 Se você não estiver familiarizado com o espelhamento de banco de dados, veja [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
### <a name="adding-a-witness-to-an-existing-session"></a>Adicionando um servidor testemunha a uma sessão existente  
 Você pode adicionar um servidor testemunha a uma sessão existente ou substituir uma testemunha existente. Se você souber qual é o endereço de rede do servidor testemunha, poderá inseri-lo manualmente no campo **Testemunha** . Se você não souber o endereço de rede do servidor testemunha, use a opção Assistente para Configurar Segurança de Espelhamento de Banco de Dados para configurar o servidor testemunha. Depois que o endereço estiver no campo, verifique se a opção **Alta segurança com failover automático (síncrono)** está selecionada.  
  
 Depois de configurar uma nova testemunha, clique em **OK** para adicioná-la à sessão de espelhamento.  
  
 **Para adicionar uma testemunha usando a Autenticação do Windows**  
  
 [Adicionar ou substituir uma testemunha de espelhamento de banco de dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
### <a name="removing-a-witness"></a>Removendo uma testemunha  
 Para remover uma testemunha, exclua seu endereço de rede de servidor do campo **Testemunha** . Se você mudar do modo de alta segurança com failover automático para o modo de alto desempenho, o campo **Testemunha** será desmarcado automaticamente.  
  
 Depois de excluir o servidor testemunha, clique em **OK** para removê-lo da sessão de espelhamento.  
  
### <a name="monitoring-database-mirroring"></a>Monitorando o espelhamento de banco de dados  
 Para monitorar os bancos de dados espelhados em uma instância de servidor, é possível usar o Monitor de Espelhamento de Banco de Dados ou o procedimento armazenado do sistema sp_dbmmonitorresults.  
  
 **Para monitorar bancos de dados espelhados**  
  
-   [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
-   [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
 Para obter mais informações, consulte [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Especificar um endereço de rede do servidor &#40;Espelhamento de banco de dados&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Consulte também  
 [Segurança de transporte para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [Troca de função durante uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Pausando e retomando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md)   
 [Removendo o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)   
 [Testemunha de espelhamento de banco de dados](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  
