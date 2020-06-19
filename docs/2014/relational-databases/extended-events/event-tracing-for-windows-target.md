---
title: Destino do Rastreamento de Eventos para Windows | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- event tracing for windows target
- ETW target
- targets [SQL Server extended events], event tracing for windows target
ms.assetid: ca2bb295-b7f6-49c3-91ed-0ad4c39f89d5
author: rothja
ms.author: jroth
ms.openlocfilehash: 55f247af30b5278f614b6505a94266cc07ec6c54
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85027589"
---
# <a name="event-tracing-for-windows-target"></a>destino do rastreamento de eventos do Windows
  Antes de usar o Rastreamento de Eventos do Windows (ETW) como destino, é recomendável ter um conhecimento prático do ETW. O rastreamento ETW é usado junto com o recurso Eventos Estendidos ou como um consumidor de Eventos Estendidos. Os links externos a seguir fornecem um ponto de partida para a obtenção de informações gerais do ETW:  
  
-   [Eventos do Windows](https://go.microsoft.com/fwlink/?LinkId=92380)  
  
-   [Melhore o ajuste de depuração e desempenho com o ETW](https://go.microsoft.com/fwlink/?LinkId=92381)  
  
 O destino de ETW é um destino singleton, embora o destino pode ser adicionado a muitas sessões. Se um evento for gerado em muitas sessões, esse evento somente será propagado para o destino de ETW uma vez por ocorrência de evento. O mecanismo de Eventos Estendidos é limitado a uma única instância por processo.  
  
> [!IMPORTANT]  
>  Para que o destino ETW funcione, a conta de inicialização do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser um membro do grupo de Usuários de Log de Desempenho.  
  
 A configuração dos eventos presente em uma sessão ETW é controlada pelo processo que hospeda o mecanismo de Eventos Estendidos. O mecanismo controla os eventos a serem gerados e as condições que devem ser atendidas para que um evento ocorra.  
  
 Depois de associar a uma sessão de Eventos Estendidos, que anexa o destino ETW pela primeira vez durante o tempo de vida de um processo, o destino ETW abre uma única sessão ETW no provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se uma sessão ETW já existir, o destino ETW obterá uma referência para a sessão existente. Essa sessão ETW é compartilhada por todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um determinado computador. Essa sessão ETW recebe todos os eventos de sessões que têm o destino ETW.  
  
 Como o ETW precisa de provedores para ser habilitado a consumir eventos e conduzi-los ao ETW, todos os pacotes de Eventos Estendidos são habilitados na sessão. Quando um evento é disparado, o destino ETW envia o evento à sessão na qual o provedor do evento está habilitado.  
  
 O destino ETW oferece suporte à publicação síncrona de eventos no thread que gera o evento. No entanto, o destino ETW não oferece suporte à publicação assíncrona de eventos.  
  
 O destino ETW não permite controle de controladores ETW externos, como Logman.exe. Para gerar rastreamentos ETW, é necessário criar uma sessão de evento com o destino ETW. Para obter mais informações, veja [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql).  
  
> [!NOTE]  
>  A habilitação do destino de ETW cria uma sessão de ETW denominada XE_DEFAULT_ETW_SESSION. Se uma sessão com o nome XE_DEFAULT_ETW_SESSION já existir, ele será usado sem que nenhuma propriedade da sessão existente seja modificada. O XE_DEFAULT_ETW_SESSION é compartilhado entre todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois de iniciar o XE_DEFAULT_ETW_SESSION, você deve pará-lo usando um controlador de ETW, como a ferramenta Logman. Por exemplo, você pode executar o seguinte comando no prompt de comando: `logman stop XE_DEFAULT_ETW_SESSION -ets`.  
  
 A tabela a seguir descreve as opções disponíveis para configuração do destino de ETW.  
  
|Opção|Valores permitidos|Descrição|  
|------------|--------------------|-----------------|  
|default_xe_session_name|Qualquer cadeia de caracteres até 256 caracteres. Esse valor é opcional.|O nome da sessão de Eventos Estendidos. Por padrão, este é XE_DEFAULT_ETW_SESSION.|  
|default_etw_session_logfile_path|Qualquer cadeia de caracteres até 256 caracteres. Esse valor é opcional.|O caminho para o arquivo de log da sessão de Eventos Estendidos. Por padrão, esse é % TEMP% \ XEEtw.etl.|  
|default_etw_session_logfile_size_mb|Qualquer inteiro não atribuído. Esse valor é opcional.|O tamanho do arquivo de log, em megabytes (MB), para a sessão de Eventos Estendidos. O padrão é 20 MB.|  
|default_etw_session_buffer_size_kb|Qualquer inteiro não atribuído. Esse valor é opcional.|O tamanho do buffer na memória, em kilobytes (KB), para a sessão de Eventos Estendidos. O padrão é 128 KB.|  
|retries|Qualquer inteiro não atribuído.|O número de vezes para tentar publicar novamente o evento no subsistema ETW antes de descartar o evento. O padrão é 0.|  
  
 A configuração dessas definições precedentes é opcional. O destino ETW usa valores padrão para essas configurações.  
  
 O destino ETW é responsável por:  
  
-   Criar a sessão ETW padrão.  
  
-   Registrar todos os pacotes de Eventos Estendidos com o ETW. Isso assegura que os eventos não sejam descartados pelo ETW.  
  
-   Gerenciar o fluxo de eventos para o ETW. O destino ETW cria um evento ETW com os dados de Eventos Estendidos e o envia para a sessão ETW apropriada. Se o evento for maior do que o tamanho do buffer, ou os dados não se encaixarem em um evento ETW, o ETW dividirá o evento em fragmentos.  
  
-   Manter os pacotes de Eventos Estendidos habilitados o tempo todo.  
  
 Os locais de arquivo padrão seguintes são usados pelo ETW:  
  
-   O arquivo de saída ETW está em %TEMP%\XEEtw.etl.  
  
    > [!IMPORTANT]  
    >  O caminho do arquivo não pode ser alterado depois que a sessão for iniciada.  
  
-   Arquivos de Managed Object Format (MOF) estão em *\<your install path>* \Microsoft SQL Server\Shared. Para obter mais informações, veja [Managed Object Format](https://go.microsoft.com/fwlink/?LinkId=92851) no MSDN.  
  
## <a name="adding-the-target-to-a-session"></a>Adicionando o destino a uma sessão  
 Para adicionar o destino de ETW a uma sessão de Eventos Estendidos, você deve incluir a instrução a seguir ao criar ou alterar uma sessão de evento:  
  
```  
ADD TARGET package0.etw_classic_sync_target  
```  
  
 Para obter mais informações sobre um exemplo completo que mostra como usar o destino ETW, inclusive como exibir os dados, veja [Monitorar a atividade do sistema usando Eventos Estendidos](monitor-system-activity-using-extended-events.md).  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server destinos de eventos estendidos](../../database-engine/sql-server-extended-events-targets.md)   
 [sys. dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CRIAR sessão de evento &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
