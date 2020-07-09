---
title: Notificações de evento | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications, about
- events [SQL Server], notifications
ms.assetid: 4da73ca1-6c06-4e96-8ab8-2ecba30b6c86
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: de9035c84862bcde78c3a6f42133d8cbd52ae9b5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764969"
---
# <a name="event-notifications"></a>Notificações de eventos
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  As notificações de evento enviam informações sobre eventos a um serviço do [!INCLUDE[ssSB](../../includes/sssb-md.md)] . As notificações de evento são executadas em resposta a uma variedade de instruções DDL (linguagem de definição de dados) do [!INCLUDE[tsql](../../includes/tsql-md.md)] e eventos de Rastreamento do SQL por meio do envio de informações sobre esses eventos a um serviço do [!INCLUDE[ssSB](../../includes/sssb-md.md)] .  
  
 Notificações de eventos podem ser usadas para fazer o seguinte:  
  
-   Registrar em log e examinar alterações ou atividade ocorridas no banco de dados.  
  
-   Executar uma ação em resposta a um evento de maneira assíncrona, em vez de síncrona.  
  
 As notificações de evento podem oferecer uma alternativa de programação a gatilhos DDL e ao Rastreamento do SQL.  
  
## <a name="event-notifications-benefits"></a>Benefícios das notificações de evento  
 Notificações de evento são executadas de forma assíncrona, fora do escopo de uma transação. Portanto, ao contrário dos gatilhos DDL, as notificações de evento podem ser usadas dentro de um aplicativo de banco de dados para responder a eventos sem usar nenhum recurso definido pela transação imediata.  
  
 Ao contrário do Rastreamento do SQL, as notificações de evento podem ser usadas para executar uma ação dentro de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em resposta a um evento do Rastreamento do SQL.  
  
 Os dados de evento podem ser usados por aplicativos que se encontram em execução junto com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para rastrear o andamento e tomar decisões. Por exemplo, a notificação de evento a seguir envia um aviso a determinado serviço todas as vezes que uma instrução `ALTER TABLE` é emitida no banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```  
USE AdventureWorks2012;  
GO  
CREATE EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE '//Adventure-Works.com/ArchiveService' ,  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
```  
  
## <a name="event-notifications-concepts"></a>Conceitos das notificações de evento  
 Quando uma notificação de evento é criada, uma ou mais conversas de [!INCLUDE[ssSB](../../includes/sssb-md.md)] são abertas entre uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o serviço de destino especificado. Normalmente, as conversações permanecem abertas enquanto a notificação de eventos existir como objeto na instância do servidor. Em alguns casos de erro, as conversações podem ser fechadas antes de a notificação de eventos ser descartada. Essas conversações nunca são compartilhadas entre notificações de eventos. Cada notificação de eventos tem suas próprias conversações exclusivas. Terminar explicitamente uma conversa impede que o serviço de destino receba mais mensagens, e a conversa não será reaberta na próxima vez que a notificação de evento for acionada.  
  
 As informações de evento são entregues ao serviço do [!INCLUDE[ssSB](../../includes/sssb-md.md)] como uma variável do tipo **xml** que fornece informações especificando quando um evento ocorreu, informações sobre o objeto de banco de dados afetado, a instrução do lote [!INCLUDE[tsql](../../includes/tsql-md.md)] envolvida e outros dados. Para obter mais informações sobre o esquema XML produzido por notificações de evento, consulte [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md).  
  
### <a name="event-notifications-vs-triggers"></a>Notificações de evento x Gatilhos  
 A tabela a seguir compara e contrasta gatilhos e notificações de evento.  
  
|Gatilhos|Notificações de eventos|  
|--------------|-------------------------|  
|Os gatilhos DML respondem a eventos DML (linguagem de manipulação de dados). Gatilhos DDL respondem a eventos de linguagem de definição de dados (DDL).|Notificações de eventos respondem a eventos DDL e a um subconjunto de eventos de Rastreamento do SQL.|  
|Gatilhos podem executar Transact-SQL ou código gerenciado CLR (Common Language Runtime).|Notificações de eventos não executam código. Em vez disso, enviam mensagens **xml** a um serviço de Service Broker.|  
|Gatilhos são processados sincronicamente, dentro do escopo das transações que os acionam.|Notificações de eventos podem ser processadas de forma assíncrona e não são executadas no escopo das transações que as acionam.|  
|O consumidor de um gatilho encontra-se estreitamente acoplado ao evento que o aciona.|O consumidor de uma notificação de eventos encontra-se desacoplado do evento que o aciona.|  
|Gatilhos devem ser processados no servidor local.|Notificações de eventos podem ser processadas em um servidor remoto.|  
|Gatilhos podem ser revertidos.|Notificações de eventos não podem ser revertidas.|  
|Os nomes dos gatilhos DML seguem o escopo do esquema. Os nomes dos gatilhos DDL seguem o escopo do banco de dados ou do servidor.|Os nomes das notificações de eventos seguem o escopo do servidor ou do banco de dados. Notificações de eventos em um evento QUEUE_ACTIVATION seguem o escopo de uma fila específica.|  
|Gatilhos DML são de propriedade do mesmo proprietário das tabelas a que se aplicam.|O proprietário de uma notificação de eventos em uma fila pode ser diferente do proprietário do objeto a que se aplica.|  
|Gatilhos têm suporte à cláusula EXECUTE AS.|Notificações de eventos não têm suporte à cláusula EXECUTE AS.|  
|Informações de eventos de gatilhos DDL podem ser capturadas por meio da função EVENTDATA, que retorna um tipo de dados **xml** .|Notificações de eventos enviam informações **xml** sobre o evento para um serviço de Service Broker. As informações são formatadas no mesmo esquema da função EVENTDATA.|  
|Metadados sobre gatilhos localizam-se nas exibições de catálogo **sys.triggers** e **sys.server_triggers** .|Os metadados sobre notificações de evento localizam-se nas exibições de catálogo **sys.event_notifications** e **sys.server_event_notifications** .|  
  
### <a name="event-notifications-vs-sql-trace"></a>Notificações de evento x Rastreamento do SQL  
 A tabela a seguir compara e contrasta o uso de notificações de evento e do Rastreamento do SQL para monitorar eventos de servidor.  
  
|Rastreamento do SQL|Notificações de eventos|  
|---------------|-------------------------|  
|O Rastreamento do SQL não gera nenhuma sobrecarga de desempenho associada às transações. O empacotamento de dados é eficiente.|Há sobrecarga de desempenho associada à criação dos dados de eventos formatados por XML e ao envio da notificação de eventos.|  
|O Rastreamento do SQL pode monitorar qualquer classe de evento.|Notificações de eventos podem monitorar um subconjunto de classes de evento de rastreamento e também todos os eventos de linguagem de definição de dados (DDL).|  
|Você pode personalizar quais colunas de dados devem ser geradas em um evento de rastreamento.|O esquema dos dados de evento formatados por XML retornado por notificações de eventos é fixo.|  
|Eventos de rastreamento gerados por DDL sempre são gerados, independentemente de a instrução DDL ser revertida ou não.|As notificações de eventos não serão acionadas se o evento na instrução DDL correspondente for revertido.|  
|Gerenciar o fluxo intermediário de dados de evento de rastreamento envolve popular e gerenciar arquivos ou tabelas de rastreamento.|O gerenciamento intermediário de dados de notificação de eventos é feito automaticamente, através de filas do Service Broker.|  
|Os rastreamentos devem ser reiniciados toda vez que o servidor for reiniciado.|Depois de registradas, as notificações de eventos persistem pelos ciclos de servidor e são transacionadas.|  
|Depois de iniciado, o acionamento de rastreamentos não pode ser controlado. Podem ser usados horários de parada e de filtro para especificar quando devem ser iniciados. Os rastreamentos são acessados pela sondagem do arquivo de rastreamento correspondente.|As notificações de eventos podem ser controladas pelo uso da instrução WAITFOR em relação à fila que recebe a mensagem gerada pela notificação. Elas podem ser acessadas pela sondagem da fila.|  
|ALTER TRACE é a permissão mínima exigida para a criação de um rastreamento. Também é necessária permissão para criar um arquivo de rastreamento no computador correspondente.|A permissão mínima depende do tipo de notificação de evento que está sendo criada. Também é necessária permissão RECEIVE na fila correspondente.|  
|Os rastreamentos podem ser recebidos remotamente.|As notificações de eventos podem ser recebidas remotamente.|  
|Os eventos de rastreamento são implementados pelo uso de procedimentos armazenados do sistema.|As notificações de eventos são implementadas pelo uso de uma combinação de instruções de [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssSB](../../includes/sssb-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|Os dados de eventos do rastreamento podem ser acessados via programação, por consultas à tabela de rastreamento correspondente, análise do o arquivo de rastreamento ou uso da classe TraceReader do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO).|Os dados de evento são acessados via programação emitindo XQuery em relação aos dados de evento formatados por XML ou por meio das classes de evento do SMO.|  
  
## <a name="event-notification-tasks"></a>Tarefas da notificação de evento  
  
|Tarefa|Tópico|  
|----------|-----------|  
|Descreve como criar e implementar notificações de evento.|[Implementar notificações de evento](../../relational-databases/service-broker/implement-event-notifications.md)|  
|Descreve como configurar a caixa de diálogo do [!INCLUDE[ssSB](../../includes/sssb-md.md)] para notificações de evento que enviam mensagens a um agente de serviços em um servidor remoto.|[Configurar segurança de caixa de diálogo para notificações de evento](../../relational-databases/service-broker/configure-dialog-security-for-event-notifications.md)|  
|Descreve como retornar informações sobre notificações de evento.|[Obter informações sobre notificações de eventos](../../relational-databases/service-broker/get-information-about-event-notifications.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Gatilhos DDL](../../relational-databases/triggers/ddl-triggers.md)   
 [Gatilhos DML](../../relational-databases/triggers/dml-triggers.md)   
 [Rastreamento do SQL](../../relational-databases/sql-trace/sql-trace.md)  
  
  
