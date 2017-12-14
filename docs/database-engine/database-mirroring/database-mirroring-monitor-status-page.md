---
title: "Monitor do Espelhamento de Banco de Dados (página Status) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mirroring
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.dbmmonitor.status.f1
ms.assetid: 4f64b4e1-89e9-4827-98fa-b92c3dc73b48
caps.latest.revision: "36"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 658cb8a6783afc9b01259e8cf2e8915659550867
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="database-mirroring-monitor-status-page"></a>Monitor de Espelhamento de Banco de Dados (página Status)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Essa página somente leitura exibe o status mais recente de espelhamento das instâncias de servidor principal e espelho do banco de dados selecionadas atualmente na árvore de navegação. Se as informações sobre uma instância estiverem indisponíveis atualmente, algumas das células na grade **Status** correspondente a essa instância ficarão esmaecidas e exibirão o status **Desconhecido**.  
  
 **Para usar o SQL Server Management Studio para monitorar o espelhamento de banco de dados**  
  
-   [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="options"></a>Opções  
 **Status**  
 Exibe uma grade que contém o mais recente status de espelhamento de nível superior de cada instância de servidor principal e espelho. As linhas da grade **Status** estão na seguinte ordem:  
  
-   Instância do servidor principal  
  
-   Instância do servidor espelho  
  
 As colunas são apresentadas assim:  
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|**Instância do Servidor**|Nome da instância de servidor cujo status é exibido na linha **Status** .|  
|**Função Atual**|Função atual da instância de servidor, que é **Principal** ou **Espelho**.|  
|**Estado de Espelhamento**|O estado de espelhamento informado pela instância de servidor e um ícone que indica a severidade do estado. Os possíveis status e seus ícones associados são os seguintes:<br /><br /> Ícone: —, status **Desconhecido**. O monitor não está conectado a nenhum parceiro. As únicas informações disponíveis são aquelas armazenadas em cache pelo monitor.<br /><br /> Ícone: ícone de aviso, status **Sincronizando**. O conteúdo do banco de dados espelho está ficando atrás do conteúdo do banco de dados principal. A instância do servidor principal está enviando registros de log para a instância do servidor espelho, a qual está aplicando as alterações ao banco de dados espelho para rolagem para frente. No início de uma sessão de espelhamento de banco de dados, o banco de dados espelho e principal estão nesse estado.<br /><br /> Ícone: cilindro do banco de dados padrão, o status **Sincronizado**. Quando o servidor espelho torna-se suficientemente atualizado em relação ao servidor principal, o estado do banco de dados é alterado para **Sincronizado**. O banco de dados permanece nesse estado enquanto o servidor principal estiver enviando alterações ao servidor espelho e esse estiver aplicando alterações ao banco de dados espelho.  Para o modo de alta segurança, o failover automático e o failover manual são ambos possíveis, sem perda de dados.  No modo de alto desempenho, alguma perda de dados é sempre possível, mesmo no estado **Sincronizado** .<br /><br /> Ícone: ícone de aviso, status **Suspenso**. <br />                            O banco de dados principal está disponível, mas não está enviando logs para o servidor espelho.<br /><br /> Ícone: ícone de erro, status **Desconectado**. A instância do servidor não pode se conectar ao seu parceiro.|  
|**Conexão de Testemunha**|Status de conexão da testemunha, precedido por um ícone de status, **Desconhecido**, **Conectado**ou **Desconectado**.|  
|**Histórico**|Clique para exibir o histórico de espelhamento na instância de servidor. Isso abre a caixa de diálogo **Histórico do Espelhamento de Banco de Dados** , que exibe o histórico de status e as estatísticas de espelhamento de um banco de dados espelho em uma determinada instância de servidor.<br /><br /> O botão **Histórico** ficará esmaecido se o monitor não for conectado à instância de servidor.|  
  
 **Log principal (** *\<time>* **)**  
 Status do log na instância do servidor principal a partir da hora local da instância do servidor, indicada por *\<time>*. Os parâmetros seguintes são exibidos:  
  
 **Log não enviado**  
 A quantidade de log em espera na fila de envio (em quilobytes).  
  
 **Transação não enviada mais antiga**  
 Idade da transação não enviada mais antiga na fila de envio. A idade dessa transação indica quantos minutos de transações ainda não foram enviados à instância de servidor espelho. Esse valor ajuda a medir o potencial de perda de dados em termos de tempo.  
  
 **Tempo para enviar o log (estimado)**  
 Tempo aproximado exigido pela instância de servidor principal para enviar o log atualmente na fila de envio para a instância de servidor espelho (a *taxa de envio*). Como a taxa de transações de entrada pode variar significativamente, a hora para enviar o log é uma estimativa. A taxa de envio, porém, pode ser útil para estimar aproximadamente a hora exigida para um failover manual.  
  
 **Taxa de envio atual**  
 Taxa em que as transações estão sendo enviadas à instância de servidor espelho, em quilobytes (KB) por segundo.  
  
 **Taxa atual de transações novas**  
 Taxa em que as transações de entrada estão sendo inseridas no log do servidor principal, em KB por segundo. Para determinar se o espelhamento está atrasado, ativo ou atualizado, compare esse valor ao valor do **Tempo para enviar o log (estimado)** .  
  
 **Log espelhado (** *\<time>* **)**  
 Status do log na instância do servidor espelhado a partir da hora local da instância do servidor, indicada por *\<time>*. Os parâmetros seguintes são exibidos:  
  
 **Log não restaurado**  
 A quantidade de log esperando na fila de restauração (em KB).  
  
 **Tempo para recuperar o log (estimado)**  
 Número aproximado de minutos exigido para que o log atualmente na fila de restauração seja aplicado ao banco de dados espelho.  
  
 **Taxa atual de restauração**  
 Taxa em que as transações estão sendo restauradas no banco de dados espelho (em KB por segundo).  
  
 **Sobrecarga de confirmação de espelhamento**  
 Número de milissegundos de atraso em média, por transação, tolerado antes da geração de um aviso no servidor principal. Esse atraso consiste na quantidade de sobrecarga incidente enquanto a instância do servidor principal aguarda que a instância do servidor espelho grave o registro do log da transação na fila de restauração. Esse valor é relevante somente no modo de alta segurança.  
  
 **Tempo para enviar e restaurar todos os logs atuais (estimado)**  
 Tempo necessário para enviar e restaurar todo o log confirmado no servidor principal a partir da hora atual. Esse tempo pode ser menor do que o total dos valores dos campos **Tempo para enviar o log (estimado)** e **Tempo para recuperar o log (estimado)** , pois as ações de enviar e restaurar podem ocorrer em paralelo. Essa estimativa prevê a hora em que devem ser enviadas e restauradas as novas transações confirmadas no servidor principal enquanto trabalham em filas de pendências na fila de envio.  
  
 **Endereço de testemunha**  
 Endereço de rede da instância de servidor testemunha. Para obter informações sobre o formato desse endereço, veja [Especificar um endereço de rede do servidor &#40;Espelhamento de Banco de Dados&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md).  
  
 **Modo de operação**  
 Modo operacional da sessão de espelhamento de banco de dados:  
  
-   **Alto desempenho (assíncrono)**  
  
-   **Alta segurança sem failover automático (síncrono)**  
  
-   **Alta segurança com failover automático (síncrono)**  
  
## <a name="remarks"></a>Comentários  
 Membros da função de banco de dados fixa **dbm_monitor** podem exibir o status de espelhamento existente usando o Monitor de Espelhamento de Banco de Dados ou o procedimento armazenado **sp_dbmmonitorresults** . Esses usuários, porém, não podem atualizar a tabela de status. Eles dependem do **Trabalho do Monitor de Espelhamento de Banco de Dados**para atualizar a tabela de status em intervalos regulares. Para saber a idade do status exibido, um usuário pode examinar os horários nos rótulos **Log principal (***\<time>***)** e **Log espelhado (***\<time>***)**.  
  
 Se esse trabalho não existir ou se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent estiver parado, o status se tornará cada vez mais obsoleto e poderá deixar de refletir a configuração da sessão espelhada. Por exemplo, depois de um failover, os parceiros podem parecer compartilhando a mesma função – principal ou espelhada, ou o servidor principal atual pode ser mostrado como o espelho e o servidor espelho atual, como o principal.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar o Monitor de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
  
