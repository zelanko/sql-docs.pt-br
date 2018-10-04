---
title: Pacotes de eventos estendidos do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], packages
- xe
ms.assetid: 6bcb04fc-ca04-48f4-b96a-20b604973447
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95fd92b13584ec31d7a7a70a7e63caf7baf4a393
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48141296"
---
# <a name="sql-server-extended-events-packages"></a>Pacotes de Eventos Estendidos do SQL Server
  Um pacote é um contêiner para objetos de Eventos Estendidos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Há três tipos de pacotes de Eventos Estendidos que incluem o seguinte:  
  
-   package0 - objetos de sistema de Eventos Estendidos. Esse é o pacote padrão.  
  
-   sqlserver – objetos relacionados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   sqlos – objetos relacionados do Sistema Operacional (SQLOS) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  O pacote SecAudit é usado pela Auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Nenhum dos objetos no pacote está disponível por meio da DDL (linguagem de definição de dados) de Eventos Estendidos.  
  
 Os pacotes são identificados por um nome, um GUID e o módulo binário que contém o pacote. Para obter mais informações, veja [sys.dm_xe_packages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql).  
  
 Um pacote pode conter qualquer ou todos os objetos a seguir, que serão discutidos em maiores detalhes posteriormente neste tópico:  
  
-   Eventos  
  
-   Destinos  
  
-   Ações  
  
-   Types  
  
-   Predicados  
  
-   Mapas  
  
 Objetos de pacotes diferentes podem ser mesclados em uma sessão de evento. Para obter mais informações, consulte [Sessões de eventos estendidos do SQL Server](sql-server-extended-events-sessions.md).  
  
## <a name="package-contents"></a>Conteúdo do pacote  
 A ilustração a seguir mostra os objetos que podem existir em pacotes, que estão contidos em um módulo. Um módulo pode ser um executável ou uma biblioteca de vínculo dinâmico.  
  
 ![O relacionamento de um módulo, pacotes e objeto](../../database-engine/media/xepackagesobjects.gif "O relacionamento de um módulo, pacotes e objeto")  
  
### <a name="events"></a>Eventos  
 Eventos são pontos de interesse de monitoramento no caminho de execução de um programa, como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O acionamento de um evento induz ao fato de que o ponto de interesse foi alcançado e traz informações do momento de acionamento do evento.  
  
 Os eventos somente podem ser usados para rastreamento ou ações de disparo. Essas ações podem ser síncronas ou assíncronas.  
  
> [!NOTE]  
>  Um evento não tem qualquer conhecimento das ações que podem ser disparadas em resposta ao acionamento do evento.  
  
 Um conjunto de eventos em um pacote não pode ser alterado depois que o pacote for registrado com o Extended Events.  
  
 Todos os eventos têm um esquema de versão que define seu conteúdo. Esse esquema é composto por colunas de evento com tipos bem definidos. Um evento de um tipo específico sempre tem que fornecer seus dados exatamente na mesma ordem especificada no esquema. No entanto, um evento de destino não precisa consumir todos os dados fornecidos.  
  
#### <a name="event-categorization"></a>Categorização do evento  
 O Extended Events usa um modelo de categorização de evento semelhante ao ETW (Rastreamento de Eventos do Windows). Duas propriedades de evento são usadas para categorização, canal e palavra-chave. O uso dessas propriedades dá suporte à integração do Extended Events com o ETW e suas ferramentas.  
  
 **Canal**  
  
 Um canal identifica a audiência para um evento. Esses canais são descritos na tabela a seguir.  
  
|Termo|Definição|  
|----------|----------------|  
|Admin|Os eventos Admin são principalmente direcionados aos usuários finais, administradores e suporte. Os eventos encontrados nos canais admin indicam um problema com uma solução bem definida na qual um administrador pode agir. Um exemplo de um evento admin é quando um aplicativo falha ao se conectar a uma impressora. Esses eventos são bem documentados ou têm uma mensagem associada a eles que diz ao leitor o que fazer para retificar o problema.|  
|Operacional|Eventos operacionais são usados para analisar e diagnosticar um problema ou uma ocorrência. Eles podem ser usados para disparar ferramentas ou tarefas com base no problema ou na ocorrência. Um exemplo de um evento operacional é quando uma impressora é adicionada ou removida de um sistema.|  
|Analítico|Eventos analíticos são publicados em grande volume. Eles descrevem operação de programa e são geralmente usados em investigações de desempenho.|  
|Depurador|Eventos depuradores são usados somente por desenvolvedores para diagnosticar um problema de depuração.<br /><br /> Observação: Eventos de canal de depuração retornam dados de estado interno de específico da implementação. Os esquemas e os dados retornados pelos eventos podem mudar ou se tornar inválidos em versões futuras do SQL Server. Portanto, eventos no canal de depuração podem mudar ou ser removidos em versões futuras do SQL Server, sem aviso prévio.|  
  
 **Palavra-chave**  
  
 Uma palavra-chave é específica do aplicativo e habilita um agrupamento mais refinado dos eventos relacionados, o que facilita a especificação e recuperação de um evento que você quer usar em uma sessão. A consulta a seguir pode ser usada para obter informações de palavra-chave.  
  
```  
select map_value Keyword from sys.dm_xe_map_values  
where name = 'keyword_map'  
```  
  
> [!NOTE]  
>  Palavras-chave mapeiam com precisão até o agrupamento atual de eventos de Rastreamento do SQL.  
  
### <a name="targets"></a>Destinos  
 Destinos são consumidores de evento. Os destinos processam eventos de forma síncrona no thread que aciona o evento ou de forma assíncrona em um thread fornecido pelo sistema. Os Eventos Estendidos fornecem vários destinos que você pode usar conforme apropriado para direcionar a saída do evento. Para obter mais informações, consulte [SQL Server Extended Events Targets](../../database-engine/sql-server-extended-events-targets.md).  
  
### <a name="actions"></a>Ações  
 Uma ação é uma resposta ou série de respostas de programa a um evento. As ações são associadas a um evento e cada evento pode ter um conjunto exclusivo de ações.  
  
> [!NOTE]  
>  Ações destinadas a um conjunto específico de eventos não podem ser associadas a eventos desconhecidos.  
  
 Uma ação associada a um evento é invocada de forma síncrona no thread que acionou o evento. Há muitos tipos de ação e eles têm uma ampla faixa de recursos. As ações podem:  
  
-   Capturar um despejo da pilha e inspecionar dados.  
  
-   Armazenar informações de estado em um contexto local usando armazenamento variável.  
  
-   Agregar dados de evento.  
  
-   Anexar dados aos dados de evento.  
  
 Alguns exemplos comuns e bem conhecidos de ações:  
  
-   Despejo da pilha  
  
-   Detecção de plano de execução (só no[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] )  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] coleção de pilha (somente[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] )  
  
-   Cálculo de estatísticas em tempo de execução  
  
-   Agrupamento de entrada de usuário em exceção  
  
### <a name="predicates"></a>Predicados  
 Predicados são um conjunto de regras lógicas usado para avaliar eventos quando eles são processados. Isso permite que o usuário do Extend Events capture dados de evento seletivamente com base em critérios específicos.  
  
 Predicados podem armazenar dados em um contexto local que podem ser usados para criar predicados que retornam valores verdadeiros uma vez a cada *n* minutos ou a cada *n* vezes que um evento é acionado. Esse armazenamento de contexto local também pode ser usado para atualizar o predicado dinamicamente, suprimindo, assim, acionamento de evento futuro, caso os eventos contenham dados semelhantes.  
  
 Os predicados têm a capacidade de recuperar informações de contexto, como a ID do thread e os dados específicos do evento. Os predicados são avaliados como expressões boolianas completas e oferecem suporte a circuito pequeno no primeiro ponto em que toda a expressão é considerada falsa.  
  
> [!NOTE]  
>  Predicados com efeitos colaterais não podem ser avaliados se a verificação de um predicado anterior falhar.  
  
### <a name="types"></a>Types  
 Como os dados são uma coleção de bytes unidos, o comprimento e as características da coleção de bytes são necessários na interpretação dos dados. Essas informações são encapsuladas no objeto Tipo. Os tipos seguintes são fornecidos para objetos de pacote:  
  
-   event  
  
-   action  
  
-   target  
  
-   pred_source  
  
-   pred_compare  
  
-   Tipo  
  
 Para obter mais informações, veja [sys.dm_xe_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql).  
  
### <a name="maps"></a>Mapas  
 Uma tabela de mapas mapeia um valor interno para uma cadeia de caracteres que habilita um usuário a saber o que o valor representa. Em vez de só poder obter um valor numérico, um usuário pode adquirir uma descrição significativa do valor interno. A consulta a seguir mostra como obter valores de mapa.  
  
```  
select map_key, map_value from sys.dm_xe_map_values  
where name = 'lock_mode'  
```  
  
 A consulta precedente produz a saída a seguir.  
  
 `map_key     map_value`  
  
 `---------------------`  
  
 `0           NL`  
  
 `1           SCH_S`  
  
 `2           SCH_M`  
  
 `3           S`  
  
 `4           U`  
  
 `5           X`  
  
 `6           IS`  
  
 `7           IU`  
  
 `8           IX`  
  
 `9           SIU`  
  
 `10          SIX`  
  
 `11          UIX`  
  
 `12          BU`  
  
 `13          RS_S`  
  
 `14          RS_U`  
  
 `15          RI_NL`  
  
 `16          RI_S`  
  
 `17          RI_U`  
  
 `18          RI_X`  
  
 `19          RX_S`  
  
 `20          RX_U`  
  
 `21          RX_X`  
  
 `21          RX_X`  
  
 Usando essa tabela como um exemplo, suponhamos que você tenha uma coluna denominada modo e seu valor seja 5. A tabela indica que 5 mapeia para X, o que significa que o tipo de bloqueio é Exclusivo.  
  
## <a name="see-also"></a>Consulte também  
 [Sessões de eventos estendidos do SQL Server](sql-server-extended-events-sessions.md)   
 [Mecanismo de eventos estendidos do SQL Server](sql-server-extended-events-engine.md)   
 [SQL Server Extended Events Targets](../../database-engine/sql-server-extended-events-targets.md)  
  
  
