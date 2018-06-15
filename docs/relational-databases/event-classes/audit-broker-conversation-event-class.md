---
title: Classe de evento Audit Broker Conversation | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Audit Broker Conversation event class
ms.assetid: d58e3577-e297-42e5-b8fe-206665a75d13
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6ba8cd56b49c78810ebef16925073d0fedddade3
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34329557"
---
# <a name="audit-broker-conversation-event-class"></a>Classe de evento Audit Broker Conversation
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria um evento **Audit Broker Conversation** para relatar mensagens de auditoria relacionadas à segurança de diálogo do Service Broker.  
  
## <a name="audit-broker-conversation-event-class-data-columns"></a>Colunas de dados da classe de evento Audit Broker Conversation  
  
|Coluna de dados|Tipo|Descrição|Número da coluna|Filtrável|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|O nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**BigintData1**|**bigint**|O número de sequência da mensagem.|52|não|  
|**ClientProcessID**|**int**|A ID atribuída pelo computador host ao processo em que está sendo executado o aplicativo cliente. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|**DatabaseID**|**int**|A ID do banco de dados especificada pela instrução USE *database* ou a ID do banco de dados padrão se nenhuma instrução USE *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**Erro**|**int**|O número de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se esse evento informar um erro.|31|não|  
|**EventClass**|**int**|O tipo de classe de evento capturado. Sempre **158** para **Audit Broker Conversation**.|27|não|  
|**EventSubClass**|**int**|O tipo de subclasse de evento, fornecendo mais informações sobre cada classe de evento. A tabela a seguir lista os valores de subclasse de evento para esse evento.|21|Sim|  
|**FileName**|**nvarchar**|A razão para a falha no logon. Se o logon teve êxito, esta coluna estará vazia.|36|não|  
|**GUID**|**uniqueidentifier**|A ID de conversa da caixa de diálogo. Esse identificador é transmitido como parte da mensagem e é compartilhado por ambos os lados da conversa.|54|não|  
|**HostName**|**nvarchar**|O nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função **HOST_NAME** .|8|Sim|  
|**IntegerData**|**int**|O número de fragmento da mensagem.|25|não|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|O nome do usuário proprietário da conexão que gerou este evento.|6|Sim|  
|**ObjectId**|**int**|A ID de usuário do serviço de destino.|22|não|  
|**RoleName**|**nvarchar**|A função do identificador de conversa. É **initiator** (iniciador) ou **target**(destino).|38|não|  
|**ServerName**|**nvarchar**|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|não|  
|**Severity**|**int**|A severidade do erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se esse evento informar um erro.|29|não|  
|**SPID**|**int**|A ID de processo do servidor atribuída pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao processo associado ao cliente.|12|Sim|  
|**StartTime**|**datetime**|O horário no qual o evento foi iniciado, quando disponível.|14|Sim|  
|**Estado**|**int**|Indica o local, dentro do código-fonte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que produziu o evento. Cada local que pode produzir esse evento tem um código de estado diferente. Um engenheiro de suporte da Microsoft pode usar esse código de estado para descobrir onde o evento foi produzido.|30|não|  
|**TextData**|**ntext**|Para erros, contém uma mensagem que descreve a razão da falha. Um dos valores seguintes:<br /><br /> <br /><br /> **Certificado não encontrado**. O usuário especificado para segurança de protocolo do diálogo não tem certificado.<br /><br /> **Não está em um período de tempo válido**. O usuário especificado para segurança de protocolo do diálogo tem um certificado, mas o certificado expirou.<br /><br /> **O certificado é muito grande para a alocação de memória**. O usuário especificado para segurança de protocolo do diálogo tem um certificado, mas o certificado é muito grande. O tamanho máximo de certificado a que Service Broker oferece suporte são 32.768 bytes.<br /><br /> **Chave privada não encontrada**. O usuário especificado para segurança de protocolo do diálogo tem um certificado, mas não existe chave privada associada ao certificado.<br /><br /> **Tamanho da chave privada do certificado incompatível com o provedor de criptografia**. A chave privada para o certificado tem um tamanho de chave que não pode ser processado com êxito. O tamanho da chave privada deve ser um múltiplo de 64 bytes.<br /><br /> **Tamanho da chave pública do certificado incompatível com o provedor de criptografia**. A chave pública para o certificado tem um tamanho de chave que não pode ser processado com êxito. O tamanho da chave pública deve ser um múltiplo de 64 bytes.<br /><br /> **Tamanho da chave privada do certificado incompatível com a chave de troca de chaves criptografada**. O tamanho de chave especificado na chave de troca de chave não corresponde ao tamanho da chave privada para o certificado. Isso geralmente indica que o certificado no computador remoto não corresponde ao certificado no banco de dados.<br /><br /> **Tamanho da chave pública do certificado incompatível com a assinatura do cabeçalho de segurança**. O cabeçalho de segurança contém uma assinatura que não pode ser validada com a chave pública do certificado. Isso geralmente indica que o certificado no computador remoto não corresponde ao certificado no banco de dados.|1|Sim|  
  
 A tabela abaixo lista os valores de subclasse para essa classe de evento.  
  
|ID|Subclasse|Descrição|  
|--------|--------------|-----------------|  
|1|No Security Header|Durante uma conversa segura, o Service Broker recebeu uma mensagem que não contém uma chave de sessão. Quando uma conversa segura é estabelecida, o protocolo de diálogo requer que todas as mensagens na conversa contenham uma chave de sessão.|  
|2|No Certificate|O Service Broker não pôde localizar um certificado utilizável para um dos participantes na conversa. Para proteger a conversa, o banco de dados deve conter um certificado para o remetente e o destinatário da conversa.|  
|3|Invalid Signature|O Service Broker não pôde verificar a assinatura de mensagem fornecida pelo remetente usando a chave pública no certificado do remetente. Isso pode indicar que a mensagem está corrompida, que a mensagem foi violada, que o serviço remoto e o serviço local não estão configurados com o mesmo certificado de usuário ou que o certificado está desatualizado.|  
|4|Run As Target Failure|O usuário de destino não tem permissões de recebimento na fila de destino. Para impedir que usuários não autorizados recebam mensagens, o Service Broker não enfileira mensagens para um usuário de destino que não pode receber da fila, quer o usuário iniciante tenha permissão para enfileirar mensagens, quer não.|  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
