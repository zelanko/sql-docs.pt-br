---
title: Classe de evento Audit Broker Login | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Audit Broker Login event class
ms.assetid: af9b1153-2791-40ef-a95c-50923cd0cc97
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e1064f0902369f81cff96f94ee68520ded419d39
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="audit-broker-login-event-class"></a>Classe de evento Audit Broker Login
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria um evento **Audit Broker Login** para informar mensagens de auditoria relacionadas à segurança de transporte do Agente de Serviços.  
  
## <a name="audit-broker-login-event-class-data-columns"></a>Colunas de dados da classe de evento Audit Broker Login  
  
|Coluna de dados|Tipo|Descrição|Número da coluna|Filtrável|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|Não usado nessa classe de evento.|10|Sim|  
|**ClientProcessID**|**int**|Não usado nessa classe de evento.|9|Sim|  
|**DatabaseID**|**int**|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**EventClass**|**int**|O tipo de classe de evento capturado. Sempre **159** para **Audit Broker Login**.|27|não|  
|**EventSequence**|**int**|Número de sequência para esse evento.|51|não|  
|**EventSubClass**|**int**|O tipo de subclasse de evento, fornecendo mais informações sobre cada classe de evento. A tabela a seguir lista os valores de subclasse de evento para esse evento.|21|Sim|  
|**FileName**|**nvarchar**|Nível de autenticação do agente remoto. Método de autenticação com suporte configurado no ponto de extremidade do agente remoto. Quando há mais de um método disponível, o ponto de extremidade de aceitação (destino) determina qual método é tentado primeiro. Os valores possíveis são:<br /><br /> **None**. Nenhum método de autenticação é configurado.<br /><br /> **NTLM**. Requer autenticação NTLM.<br /><br /> **KERBEROS**. Requer autenticação Kerberos.<br /><br /> **NEGOTIATE**. O Windows negocia o método de autenticação.<br /><br /> **CERTIFICATE**. Requer a configuração do certificado para o ponto de extremidade, que é armazenado no banco de dados **mestre** .<br /><br /> **NTLM, CERTIFICATE**. Aceita autenticação de certificado NTLM ou SSL.<br /><br /> **KERBEROS, CERTIFICATE**. Aceita autenticação de certificado Kerberos ou de ponto de extremidade.<br /><br /> **NEGOTIATE, CERTIFICATE**. O Windows negocia o método de autenticação ou um certificado de ponto de extremidade pode ser usado para autenticação.<br /><br /> **CERTIFICATE, NTLM**. Aceita um certificado de ponto de extremidade ou NTLM para autenticação.<br /><br /> **CERTIFICATE, KERBEROS**. Aceita um certificado de ponto de extremidade ou Kerberos para autenticação.<br /><br /> **CERTIFICATE, NEGOTIATE**. Aceita um certificado de ponto de extremidade para autenticação ou o Windows negocia o método de autenticação.|36|não|  
|**HostName**|**nvarchar**|Não usado nessa classe de evento.|8|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|não|  
|**LoginSid**|**imagem**|Número SID (identificação de segurança) do usuário que fez logon. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|O nome do usuário proprietário da conexão que gerou este evento.|6|Sim|  
|**ObjectName**|**nvarchar**|A cadeia de conexão usada para essa conexão.|34|não|  
|**OwnerName**|**nvarchar**|Método de autenticação com suporte configurado no ponto de extremidade de agente local. Quando há mais de um método disponível, o ponto de extremidade de aceitação (destino) determina qual método é tentado primeiro. Os valores possíveis são:<br /><br /> **None**. Nenhum método de autenticação é configurado.<br /><br /> **NTLM**. Requer autenticação NTLM.<br /><br /> **KERBEROS**. Requer autenticação Kerberos.<br /><br /> **NEGOTIATE**. O Windows negocia o método de autenticação.<br /><br /> **CERTIFICATE**. Requer a configuração do certificado para o ponto de extremidade, que é armazenado no banco de dados **mestre** .<br /><br /> **NTLM, CERTIFICATE**. Aceita autenticação de certificado NTLM ou SSL.<br /><br /> **KERBEROS, CERTIFICATE**. Aceita autenticação de certificado Kerberos ou de ponto de extremidade.<br /><br /> **NEGOTIATE, CERTIFICATE**. O Windows negocia o método de autenticação ou um certificado de ponto de extremidade pode ser usado para autenticação.<br /><br /> **CERTIFICATE, NTLM**. Aceita um certificado de autenticação de ponto de extremidade ou NTLM.<br /><br /> **CERTIFICATE, KERBEROS**. Aceita um certificado de ponto de extremidade ou Kerberos para autenticação.<br /><br /> **CERTIFICATE, NEGOTIATE**. Aceita um certificado de ponto de extremidade para autenticação ou o Windows negocia o método de autenticação.|37|não|  
|**ProviderName**|**nvarchar**|O método de autenticação usado para essa conexão.|46|não|  
|**RoleName**|**nvarchar**|A função da conexão. É **initiator** (iniciador) ou **target**(destino).|38|não|  
|**ServerName**|**nvarchar**|O nome da instância do SQL Server que está sendo rastreada.|26|não|  
|**SPID**|**int**|A ID de processo do servidor atribuída pelo SQL Server ao processo associado ao cliente.|12|Sim|  
|**StartTime**|**datetime**|O horário no qual o evento foi iniciado, quando disponível.|14|Sim|  
|**Estado**|**int**|Indica o local no código-fonte do SQL Server que produziu o evento. Cada local que pode produzir esse evento tem um código de estado diferente. Um engenheiro de suporte da Microsoft pode usar esse código de estado para descobrir onde o evento foi produzido.|30|não|  
|**TargetUserName**|**nvarchar**|Estado do logon. Um dos seguintes:<br /><br /> INITIAL<br /><br /> WAIT LOGIN NEGOTIATE<br /><br /> ONE ISC<br /><br /> ONE ASC<br /><br /> TWO ISC<br /><br /> TWO ASC<br /><br /> Confirmação WAIT ISC<br /><br /> Confirmação WAIT ASC<br /><br /> WAIT REJECT<br /><br /> WAIT PRE-MASTER SECRET<br /><br /> WAIT VALIDATION<br /><br /> WAIT ARBITRATION<br /><br /> ONLINE<br /><br /> erro<br /><br /> <br /><br /> **Observação**: ISC = Iniciar Contexto de Segurança. ASC = Aceitar Contexto de Segurança|39|não|  
|**TransactionID**|**bigint**|ID da transação atribuída pelo sistema.|4|não|  
  
 A tabela abaixo lista os valores de subclasse para essa classe de evento.  
  
|ID|Subclasse|Descrição|  
|--------|--------------|-----------------|  
|1|Login Success|Um evento Login Success informa que o processo de logon do agente adjacente foi concluído com êxito.|  
|2|Login Protocol Error|Um evento Login Protocol Error informa que o agente recebe uma mensagem bem formada, mas não válida para o estado atual do processo de logon. A mensagem pode ter sido perdida ou enviada fora de sequência.|  
|3|Message Format Error|Um evento Message Format Error evento informa que o agente recebeu uma mensagem que não corresponde ao formato esperado. A mensagem pode ter sido corrompida ou um programa diferente do SQL Server pode estar enviando mensagens para a porta usada pelo Agente de Serviços.|  
|4|Negotiate Failure|Um evento Negotiate Failure informa que o agente local e o agente remoto oferecem suporte a níveis de autenticação mutuamente exclusivos.|  
|5|Authentication Failure|Um evento Authentication Failure informa que o Agente de Serviços não pode executar autenticação para a conexão devido a um erro. Para Autenticação do Windows, esse evento informa que o Service Broker não pode usar a Autenticação do Windows. Para autenticação com base em certificado, esse evento informa que o Service Broker não pode acessar o certificado.|  
|6|Authorization Failure|Um evento Authorization Failure informa que o Agente de Serviços negou autorização para a conexão. Para Autenticação do Windows, esse evento informa que o identificador de segurança para a conexão não corresponde a um usuário de banco de dados. Para autenticação com base em certificado, esse evento informa que a chave pública fornecida na mensagem não corresponde a um certificado no banco de dados.|  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
