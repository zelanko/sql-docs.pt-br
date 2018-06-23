---
title: Examine os resultados da repetição | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: da999781-f0ff-47eb-ba7a-09c0ed8f61ad
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ecfcf05a685543e22d9ea9bf3b2889fcb8098064
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119025"
---
# <a name="review-the-replay-results"></a>Revisar os resultados da reprodução
  Depois que o recurso [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Distributed Replay conclui uma reprodução distribuída, a atividade de reprodução para cada cliente pode ser capturada e salva em arquivos de rastreamento de resultado em cada cliente. Para capturar essa atividade, você deve usar o parâmetro **-o** ao executar a ferramenta de administração com a opção **reproduzir**. Para obter mais informações sobre a opção de reprodução, consulte [Opção Reprodução &#40;Ferramenta de administração de reprodução distribuída&#41;](replay-option-distributed-replay-administration-tool.md).  
  
 O local onde os arquivos de rastreamento de resultado são armazenados é especificado pelo elemento XML `<ResultDirectory>` no arquivo de configuração de cliente, `DReplayClient.xml`, situado em cada cliente. Os arquivos de rastreamento no diretório de resultados do cliente são substituídos em cada reprodução.  
  
 Para especificar que tipo de saída deve ser capturada nos arquivos de rastreamento de resultado, modifique o arquivo de configuração de reprodução, `DReplay.exe.replay.config`. Você pode usar o elemento XML `<OutputOptions>` para especificar se a contagem de linhas ou o conteúdo do conjunto de resultados deve ser gravado.  
  
 Para obter mais informações sobre esses parâmetros de configuração, consulte [Configurar Distributed Replay](configure-distributed-replay.md).  
  
## <a name="event-classes-captured-in-result-trace-files"></a>Classes de evento capturadas em arquivos de rastreamento de resultado  
 A tabela a seguir lista todas as classes de eventos que são capturadas nos dados de rastreamento de resultado.  
  
|Categoria|Nome de EventClass|Frequência de captura|Ponto de captura|  
|--------------|---------------------|-----------------------|----------------------|  
|Eventos reproduzíveis|Audit Login|Uma vez para cada evento Audit Login nos dados de rastreamento originais|Na conclusão bem-sucedida ou na falha do evento|  
||Audit Logout|Uma vez para cada evento Audit Logout nos dados de rastreamento originais|Na conclusão bem-sucedida ou na falha do evento|  
||SQL:BatchCompleted|Uma vez para cada evento SQL:BatchStarting nos dados de rastreamento originais|Na conclusão bem-sucedida ou na falha do evento|  
||RPC:Completed|Uma vez para cada evento RPC:Starting nos dados de rastreamento originais|Na conclusão bem-sucedida ou na falha do evento|  
|Estatísticas e resultados|Replay Settings Event|Uma vez|Primeiro evento de rastreamento de resultado|  
||Replay Statistics Event|Uma vez|Último evento de rastreamento de resultado|  
||Replay Result Set Event|Uma vez para cada evento SQL:BatchStarting e RPC:Starting.<br /><br /> É capturado somente se o valor da opção `<RecordResultSet>` no arquivo de configuração de reprodução tiver sido definida como `Yes`.||  
||Replay Result Row Event|Uma vez para cada linha no conjunto de resultados para eventos SQL:BatchStarting e RPC:Starting.<br /><br /> É capturado somente se o valor da opção `<RecordResultSet>` no arquivo de configuração de reprodução tiver sido definida como `Yes`.||  
|Erros e avisos|Replay Internal Error|Uma vez para cada erro interno|Na condição de erro interno|  
||Replay Provider Error|Uma vez para cada erro de provedor|Na condição de erro de provedor|  
  
 Observe o seguinte:  
  
-   Para cada evento que é reproduzido com êxito no servidor de destino, há uma classe de evento de saída correspondente.  
  
-   Para cada falha ou cancelamento de evento, pode haver vários erros que são gerados.  
  
## <a name="event-class-column-mapping"></a>Mapeamento de coluna de classe de evento  
 As figura a seguir lista as colunas do rastreamento de resultado disponíveis para cada tipo de classe de evento que é capturada durante a reprodução.  
  
 ![Mapeamento de coluna de classe de evento](../../database-engine/media/eventclassmappings.gif "mapeamento de coluna de classe de evento")  
  
## <a name="column-descriptions-for-result-trace"></a>Descrições de coluna para rastreamento de resultado  
 A tabela a seguir descreve as colunas dos dados de rastreamento de resultado.  
  
|Nome da coluna de dados|Tipo de Dados|Description|ID da coluna|  
|----------------------|---------------|-----------------|---------------|  
|EventClass|`nvarchar`|O nome da classe de evento.|1|  
|EventSequence|`bigint`|Para erros de provedor, e erros e avisos internos, esta é a sequência de eventos de captura que corresponde ao erro ou aviso.<br /><br /> Para todas as outras classes de eventos, esta é a sequência do evento nos dados de rastreamento originais.|2|  
|ReplaySequence|`bigint`|Para erros de provedor, e erros e avisos internos, esta é a sequência de eventos de reprodução que corresponde ao erro ou aviso.<br /><br /> Para todas as outras classes de eventos, esta é a sequência do evento que é atribuído durante a reprodução.|3|  
|TextData|`ntext`|O conteúdo de TextData depende da EventClass.<br /><br /> Para Audit Login e ExistingConnection, este é a opção definida para a conexão.<br /><br /> Para SQL:BatchStarting, este é o corpo da solicitação de lote.<br /><br /> Para RPC:Starting, este é o procedimento armazenado que foi chamado.<br /><br /> Para Replay Settings Event, esta coluna contém as configurações que são definidas no arquivo de configuração de reprodução.<br /><br /> Para Replay Statistics Event, ela contém as seguintes informações:<br />O SQL Server de destino da reprodução<br />Número total de eventos reproduzíveis<br />O número de erros de provedor<br />O número de erros internos<br />Avisos internos<br />Número total de erros<br />Taxa de passagem global<br />A hora da reprodução (HH:MM:SS:MMM)<br /><br /> Para Replay Result Set Event, mostra a lista de cabeçalhos da coluna de resultados de retorno.<br /><br /> Para Replay Result Row Event, mostra o valor de retorno de todas as colunas dessa linha.<br /><br /> Para Replay Internal Warning e Replay Provider Error, esta coluna contém os avisos ou erros de provedor.|4|  
|Attention|`bigint`|A duração da atenção (em microssegundos) para o evento. Isso é calculado a partir do evento Attention do rastreamento de captura. Se não havia nenhum tempo limite de consulta especificado para o evento, esta coluna não será populada (null).|5|  
|SubmitTime|`datetime`|A hora em que o evento foi enviado ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|6|  
|IsSuccessful|`int`|Um sinalizador booliano que indica se um evento específico foi executado com êxito, e se conjuntos de resultados foram retornados ao cliente.<br /><br /> Um evento que gera um aviso (como quando um evento é cancelado devido a Attention ou um tempo limite especificado pelo usuário) é considerado bem-sucedido.<br /><br /> IsSuccessful pode ter um dos seguintes valores:<br /><br /> 1 = êxito<br /><br /> 0 = falha|7|  
|Duration [microsec]|`bigint`|A duração do tempo de resposta (em microssegundos) para o evento. A medição começa quando o evento logon/log off/RPC/Language é enviado ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Se o evento obtiver êxito, a medição terminará quando o conjunto de resultados completo tiver sido consumido.<br /><br /> Se o evento não obtiver êxito, a medição terminará na hora da falha ou do cancelamento do evento.|8|  
|RowCount|`bigint`|Populado de acordo com o valor de `<RecordRowCount>` no arquivo de configuração de reprodução:<br /><br /> Se `<RecordRowCount>` for igual a Yes, esta célula conterá o número de linhas do conjunto de resultados que são retornadas pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Se `<RecordRowCount>` for igual a No, esta célula não será populada (null).|9|  
|CaptureSPID|`int`|A ID da sessão de captura do evento.|10|  
|ConnectionID|`int`|A ID da conexão de captura do evento.|11|  
|ReplaySPID|`int`|A ID da sessão de reprodução do evento.|12|  
|DatabaseName|`nvarchar`|O nome do banco de dados no qual a instrução do usuário está sendo executada.|13|  
|LoginName|`nvarchar`|O nome de logon do usuário. Pode ser um logon de segurança do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou as credenciais de logon do Microsoft Windows no formato *nome_do_domínio*\\*nome_do_usuário*.|14|  
|CaptureHostName|`nvarchar`|O nome do computador no qual o serviço cliente está sendo executado durante a captura.|15|  
|ReplayHostName|`nvarchar`|O nome do computador em que o aplicativo cliente está sendo executado durante a reprodução.|16|  
|ApplicationName|`nvarchar`|O nome do aplicativo cliente que criou a conexão com a conexão com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] durante a captura.|17|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)   
 [Requisitos do Distributed Replay](distributed-replay-requirements.md)   
 [Opções de linha de comando da ferramenta de administração &#40;Distributed Replay Utility&#41;](administration-tool-command-line-options-distributed-replay-utility.md)   
 [Configurar o Distributed Replay](configure-distributed-replay.md)  
  
  