---
description: Classe de evento Audit Database Mirroring Login
title: Classe de evento Audit Database Mirroring Login | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- Audit Database Mirroring Login event class
- database mirroring [SQL Server], event notifications
ms.assetid: d0bd436d-aade-4208-a7e5-75cf3b5d0ce9
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b800c1fee12b34c17aeb28b252301bd13feef0f7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428548"
---
# <a name="audit-database-mirroring-login-event-class"></a>Classe de evento Audit Database Mirroring Login
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria um evento **Audit Database Mirroring Login** para relatar mensagens de auditoria relacionadas a segurança de transporte de espelhamento de banco de dados.  
  
## <a name="audit-database-mirroring-login-event-class-data-columns"></a>Colunas de dados da classe de evento Audit Database Mirroring Login  
  
|Coluna de dados|Type|Descrição|Número da coluna|Filtrável|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|Não usado nessa classe de evento.|10|Sim|  
|**ClientProcessID**|**int**|Não usado nessa classe de evento.|9|Sim|  
|**DatabaseID**|**int**|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**EventClass**|**int**|O tipo de classe de evento capturado. Sempre **154** para **Audit Database Mirroring Login**.|27|Não|  
|**EventSequence**|**int**|Número de sequência para esse evento.|51|Não|  
|**EventSubClass**|**int**|O tipo de subclasse de evento, fornecendo mais informações sobre cada classe de evento. A tabela a seguir lista os valores de subclasse de evento para esse evento.|21|Sim|  
|**FileName**|**nvarchar**|Método de autenticação com suporte configurado no ponto de extremidade do espelhamento de banco de dados remoto. Quando há mais de um método disponível, o ponto de extremidade de aceitação (destino) determina qual método é tentado primeiro. Os valores possíveis são:<br /><br /> <br /><br /> **None**. Nenhum método de autenticação é configurado.<br /><br /> **NTLM**. Requer autenticação NTLM.<br /><br /> **KERBEROS**. Requer autenticação Kerberos.<br /><br /> **NEGOTIATE**. O Windows negocia o método de autenticação.<br /><br /> **CERTIFICATE**. Requer a configuração do certificado para o ponto de extremidade, que é armazenado no banco de dados **mestre** .<br /><br /> **NTLM, CERTIFICATE**. Aceita NTLM ou o certificado de ponto de extremidade para autenticação.<br /><br /> **KERBEROS, CERTIFICATE**. Aceita Kerberos ou o certificado de ponto de extremidade para autenticação.<br /><br /> **NEGOTIATE, CERTIFICATE**. O Windows negocia o método de autenticação ou um certificado de ponto de extremidade pode ser usado para autenticação.<br /><br /> **CERTIFICATE, NTLM**. Aceita um certificado de ponto de extremidade ou NTLM para autenticação.<br /><br /> **CERTIFICATE, KERBEROS**. Aceita um certificado de ponto de extremidade ou Kerberos para autenticação.<br /><br /> **CERTIFICATE, NEGOTIATE**. Aceita um certificado de ponto de extremidade para autenticação ou o Windows negocia o método de autenticação.|36|Não|  
|**HostName**|**nvarchar**|Não usado nessa classe de evento.|8|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Não|  
|**LoginSid**|**imagem**|Número SID (identificação de segurança) do usuário que fez logon. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|O nome do usuário proprietário da conexão que gerou este evento.|6|Sim|  
|**ObjectName**|**nvarchar**|A cadeia de conexão usada para essa conexão.|34|Não|  
|**OwnerName**|**nvarchar**|Método de autenticação com suporte configurado no ponto de extremidade do espelhamento de banco de dados local. Quando há mais de um método disponível, o ponto de extremidade de aceitação (destino) determina qual método é tentado primeiro. Os valores possíveis são:<br /><br /> <br /><br /> **None**. Nenhum método de autenticação é configurado.<br /><br /> **NTLM**. Requer autenticação NTLM.<br /><br /> **KERBEROS**. Requer autenticação Kerberos.<br /><br /> **NEGOTIATE**. O Windows negocia o método de autenticação.<br /><br /> **CERTIFICATE**. Requer a configuração do certificado para o ponto de extremidade, que é armazenado no banco de dados **mestre** .<br /><br /> **NTLM, CERTIFICATE**. Aceita NTLM ou o certificado de ponto de extremidade para autenticação.<br /><br /> **KERBEROS, CERTIFICATE**. Aceita Kerberos ou o certificado de ponto de extremidade para autenticação.<br /><br /> **NEGOTIATE, CERTIFICATE**. O Windows negocia o método de autenticação ou um certificado de ponto de extremidade pode ser usado para autenticação.<br /><br /> **CERTIFICATE, NTLM**. Aceita um certificado de ponto de extremidade ou NTLM para autenticação.<br /><br /> **CERTIFICATE, KERBEROS**. Aceita um certificado de ponto de extremidade ou Kerberos para autenticação.<br /><br /> **CERTIFICATE, NEGOTIATE**. Aceita um certificado de ponto de extremidade para autenticação ou o Windows negocia o método de autenticação.|37|Não|  
|**ProviderName**|**nvarchar**|O método de autenticação usado para essa conexão.|46|Não|  
|**RoleName**|**nvarchar**|A função da conexão. É **initiator** (iniciador) ou **target**(destino).|38|Não|  
|**ServerName**|**nvarchar**|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**SPID**|**int**|A ID de processo do servidor atribuída pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao processo associado ao cliente.|12|Sim|  
|**StartTime**|**datetime**|O horário no qual o evento foi iniciado, quando disponível.|14|Sim|  
|**State**|**int**|Indica o local, dentro do código-fonte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que produziu o evento. Cada local que pode produzir esse evento tem um código de estado diferente. Um engenheiro de suporte da Microsoft pode usar esse código de estado para descobrir onde o evento foi produzido.|30|Não|  
|**TargetUserName**|**nvarchar**|Estado do logon. Um destes:<br /><br /> **INITIAL**<br /><br /> **WAIT LOGIN NEGOTIATE**<br /><br /> **ONE ISC**<br /><br /> **ONE ASC**<br /><br /> **TWO ISC**<br /><br /> **TWO ASC**<br /><br /> **Confirmação WAIT ISC**<br /><br /> **Confirmação WAIT ASC**<br /><br /> **WAIT REJECT**<br /><br /> **WAIT PRE-MASTER SECRET**<br /><br /> **WAIT VALIDATION**<br /><br /> **WAIT ARBITRATION**<br /><br /> **ONLINE**<br /><br /> **ERROR**<br /><br /> <br /><br /> Observação: ISC = Iniciar contexto de segurança. ASC = Aceitar contexto de segurança.|39|Não|  
|**TransactionID**|**bigint**|ID da transação atribuída pelo sistema.|4|Não|  
  
 A tabela abaixo lista os valores de subclasse para essa classe de evento.  
  
|ID|Subclasse|Descrição|  
|--------|--------------|-----------------|  
|1|Login Success|Um evento Login Success informa que o processo de logon de espelhamento de banco de dados adjacente terminou com êxito.|  
|2|Login Protocol Error|Um evento Login Protocol Error informa que o logon de espelhamento de banco de dados recebe uma mensagem bem formada, mas não válida para o estado atual do processo de logon. A mensagem pode ter sido perdida ou enviada fora de sequência.|  
|3|Message Format Error|Um evento Message Format Error informa que o logon de espelhamento de banco de dados recebeu uma mensagem que não corresponde ao formato esperado. A mensagem pode ter sido corrompida ou um programa diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode estar enviando mensagens para a porta usada pelo espelhamento de banco de dados.|  
|4|Negotiate Failure|Um evento Negotiate Failure informa que o ponto de extremidade de espelhamento de banco de dados local e o ponto de extremidade de espelhamento de banco de dados remoto oferecem suporte a níveis de autenticação mutuamente exclusivos.|  
|5|Authentication Failure|Um evento Authentication Failure informa que um  ponto de extremidade de espelhamento de banco de dados não pode executar autenticação para a conexão devido a um erro. Para Autenticação do Windows, esse evento informa que o ponto de extremidade de espelhamento do banco de dados não pode usar a Autenticação do Windows. Para autenticação com base em certificado, esse evento informa que o ponto de extremidade de espelhamento de banco de dados não pode acessar o certificado.|  
|6|Falha de autorização|Um evento Authorization Failure informa que um ponto de extremidade de espelhamento de banco de dados negou autorização para a conexão. Para Autenticação do Windows, esse evento informa que o identificador de segurança para a conexão não corresponde a um usuário de banco de dados. Para autenticação baseada em certificado, esse evento relata que a chave pública fornecida na mensagem não corresponde a um certificado no banco de dados **master** .|  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
