---
title: Classe de evento Database Mirroring Connection | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: b59dccc9-f40d-4c82-aa35-ac40acea86ff
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ffcd52ff5db3d6f04f0af1d3119aabbc4f5229c2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62663030"
---
# <a name="database-mirroring-connection-event-class"></a>Classe de evento conexão de espelhamento de banco de dados
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gera um evento **Conexão de Espelhamento de Banco de Dados** para relatar o status de uma conexão de transporte gerenciado pelo Espelhamento de Banco de Dados.  
  
## <a name="database-mirroringconnection-event-class-data-columns"></a>Colunas de dados da classe de evento Conexão de Espelhamento de Banco de Dados  
  
|Coluna de dados|Type|DESCRIÇÃO|Número da coluna|Filtrável|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|`nvarchar`|O nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**ClientProcessID**|`int`|A ID atribuída pelo computador host ao processo em que está sendo executado o aplicativo cliente. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|**DatabaseID**|`int`|A ID do banco de dados especificada pela instrução de *banco de dados* USE ou a ID do banco de dados padrão se nenhuma instrução de *banco de dados*USE tiver sido emitida para determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor de um banco de dados usando a função **DB_ID** .|3|Sim|  
|**Erro**|`int`|O número de identificação da mensagem em **Sys. messages** para o texto no evento. Se esse evento informar um erro, ele será o número de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|31|Não|  
|**EventClass**|`int`|O tipo de classe de evento capturado. Sempre **151** para **Database Mirroring Connection**.|27|Não|  
|**EventSequence**|`int`|Número de sequência para esse evento.|51|Não|  
|**EventSubClass**|`nvarchar`|O estado da conexão. Para esse evento, a subclasse é um dos valores a seguir.<br /><br /> **Conectando**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está iniciando uma conexão de transporte.<br /><br /> **Conectado**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estabeleceu uma conexão de transporte.<br /><br /> **Connect Failed**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] falhou em estabelecer uma conexão de transporte.<br /><br /> **Closing**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está encerrando a conexão de transporte.<br /><br /> **Fechado**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encerrou a conexão de transporte.<br /><br /> **Accept**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aceitou uma conexão de transporte de outra instância.<br /><br /> **Send IO Error**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou um erro de transporte ao enviar uma mensagem.<br /><br /> **Receive IO Error**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou um erro de transporte ao receber uma mensagem.|21|Sim|  
|**GUID**|`uniqueidentifier`|A ID de ponto de extremidade desta conexão.|54|Não|  
|**HostName**|`nvarchar`|O nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função **HOST_NAME** .|8|Sim|  
|**IntegerData**|`int`|O número de horas em que esta conexão esteve fechada.|25|Sim|  
|**IsSystem**|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário.<br /><br /> 0 = usuário<br /><br /> 1 = sistema|60|Não|  
|**LoginSid**|`image`|Número SID (identificação de segurança) do usuário que fez logon. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|`nvarchar`|O nome do usuário proprietário da conexão que gerou este evento.|6|Sim|  
|**ObjectName**|`nvarchar`|O identificador de conversa do diálogo.|34|Não|  
|**ServerName**|`nvarchar`|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**SPID**|`int`|A ID de processo do servidor atribuída pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao processo associado ao cliente.|12|Sim|  
|**StartTime**|`datetime`|O horário no qual o evento foi iniciado, quando disponível.|14|Sim|  
|**TextData**|`ntext`|O texto da mensagem de erro referente ao evento. Em eventos que não informam um erro, esse campo fica vazio. A mensagem de erro pode ser do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do Windows.|1|Sim|  
|**TransactionID**|`bigint`|ID da transação atribuída pelo sistema.|4|Não|  
  
  
