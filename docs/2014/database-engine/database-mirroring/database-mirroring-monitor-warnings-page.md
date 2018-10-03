---
title: Monitor de Espelhamento de Banco de Dados (página Avisos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.dbmmonitor.warningsandalerts.f1
ms.assetid: 01936122-961d-436b-ba3c-5f79fefe5469
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 56720ad795fb6df4de3c4cca72b9634d6fb6cf96
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48213206"
---
# <a name="database-mirroring-monitor-warnings-page"></a>Monitor de Espelhamento de Banco de Dados (página Avisos)
  Exibe uma lista somente leitura de avisos com suporte em eventos de espelhamento de banco de dados e dos valores limite de aviso especificados, se houver.  
  
 **Para usar o SQL Server Management Studio para monitorar o espelhamento de banco de dados**  
  
-   [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="columns"></a>Colunas  
 **Aviso**  
 Os avisos para os quais é possível definir limite incluem:  
  
|Aviso|Limite|  
|-------------|---------------|  
|**Avisar se o log não enviado exceder o limite**|Especifica quantos quilobytes (KB) de logs não enviados gerarão um aviso na instância principal do servidor. Esse aviso ajuda a medir o potencial de perda de dados em termos de KB e é particularmente relevante para o modo de alto desempenho. No entanto, o aviso também é relevante para o modo de segurança alta, quando o espelhamento é pausado ou suspenso devido à desconexão dos parceiros.|  
|**Avisar se o log não restaurado exceder o limite**|Especifica quantos KB de log não restaurado gerarão um aviso na instância do servidor espelho. Esse aviso é útil para medir o período do failover em termos de quilobytes. *Tempo de failover* consiste, essencialmente, no tempo necessário para que o servidor espelho anterior efetue o roll-forward de quaisquer logs restantes em sua fila de restauração, mais um pequeno tempo adicional.<br /><br /> Observação: em um failover automático, o tempo necessário para que o sistema observe o erro é independente do período do failover.<br /><br /> Para obter mais informações, veja [Estime a interrupção do serviço durante troca de função &#40;Espelhamento de Banco de Dados&#41;](estimate-the-interruption-of-service-during-role-switching-database-mirroring.md).|  
|**Avisar se a idade da transação não enviada mais antiga exceder o limite**|Especifica o número de minutos de transações que podem ser acumuladas na fila de envio, antes da geração de um aviso na instância do servidor principal. Esse aviso ajuda a medir o potencial de perda de dados em termos de tempo, sendo particularmente relevante para o modo de alto desempenho. No entanto, o aviso também é relevante para o modo de segurança alta, quando o espelhamento é pausado ou suspenso devido à desconexão dos parceiros.|  
|**Avisar se a sobrecarga espelhada confirmada exceder o limite**|Especifica o número de milissegundos de espera em média, por transação, tolerado antes da geração de um aviso no servidor principal. Esse atraso consiste na quantidade de sobrecarga incidente enquanto a instância do servidor principal aguarda que a instância do servidor espelho grave o registro do log da transação na fila de restauração. Esse valor é relevante somente no modo de alta segurança.|  
  
 **Limite em '** *<server_instance>* **'**  
 Para cada um dos avisos, exibe o limite especificado pelo usuário atual, se houver, para uma das instâncias de servidor. O nome da instância completa da instância de servidor é indicado no título de coluna correspondente.  
  
 Para obter mais informações, consulte "Comentários", mais adiante neste tópico.  
  
 **Definir Limites**  
 Clique neste botão para definir um limite para um aviso em cada um dos parceiros de failover.  
  
 Para obter mais informações, consulte "Comentários", mais adiante neste tópico.  
  
## <a name="remarks"></a>Comentários  
 Se informações relativas a uma instância de servidor estiverem presentemente indisponíveis, as células da coluna **Limite em** correspondentes serão exibidas em plano de fundo cinza e texto marca d’água. Se o monitor não estiver conectado à instância do servidor, em todas as células a grade exibirá **Não conectado a** *<SYSTEM_NAME>* ou **Não conectado a** *<SYSTEM_NAME>***\\***<instance_name>*, dependendo de a instância ser padrão ou nomeada. Se o monitor estiver esperando por uma consulta para retornar, a grade exibirá **Aguardando dados…** em todas as células.  
  
 Quando houver informações disponíveis, a célula de cada aviso exibirá um valor limite especificado (e unidade de medida), ou **Não habilitado**.  
  
 Se um limite se exceder no momento da atualização da tabela de status, será registrado um evento no log de eventos do Windows no momento do registro da linha de status. Por padrão, a linha de status será registrada uma vez por minuto se o monitor não estiver em execução. Você pode configurar um alerta em cada tipo de evento registrado usando o SQL Server Agent ou outro programa, como o MOM (Microsoft Management Operations Administrador).  
  
 Em um determinado parceiro, os eventos registrados dependem de sua função atual, principal ou espelho. Porém, é recomendado que se defina um limite de avisos para um evento específico em ambos os parceiros, para assegurar que o aviso persista caso o banco de dados apresente failover. O limite adequado para cada parceiro depende das capacidades de desempenho o sistema daquele parceiro.  
  
> [!NOTE]  
>  Você também pode usar o procedimento armazenado de sistema **sp_dbmmonitorchangealert** para configurar limites para os eventos equivalentes, ou seja, log não enviado, log não restaurado, transação não enviada mais antiga e sobrecarga de confirmação no espelho. Para obter mais informações, consulte [sp_dbmmonitorchangealert &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql).  
  
 A tabela a seguir mostra a ID de evento associada a cada um dos avisos.  
  
|Aviso do Monitor de Espelhamento de Banco de Dados|Nome do evento|ID do evento|  
|----------------------------------------|----------------|--------------|  
|**Avisar se o log não enviado exceder o limite**|Log não enviado|32042|  
|**Avisar se o log não restaurado exceder o limite**|Log não restaurado|32043|  
|**Avisar se a idade da transação não enviada mais antiga exceder o limite**|Transação não enviada mais antiga|32044|  
|**Avisar se a sobrecarga espelhada confirmada exceder o limite**|Sobrecarga espelhada confirmada|32045|  
  
## <a name="permissions"></a>Permissões  
 Para acesso completo, é necessária a associação na função de servidor fixa **sysadmin** . Só os membros de **sysadmin** podem configurar e exibir limites de aviso para métrica de desempenho de chave.  
  
 A associação na função **de dbm_monitor** só permite a exibição da linha de status mais recente na página **Avisos** .  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
  
