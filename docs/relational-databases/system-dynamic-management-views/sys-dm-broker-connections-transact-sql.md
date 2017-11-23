---
title: sys.DM broker_connections (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_connections
- dm_broker_connections
- sys.dm_broker_connections_TSQL
- dm_broker_connections_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_broker_connections dynamic management view
ms.assetid: d9e20433-67fe-4fcc-80e3-b94335b2daef
caps.latest.revision: "45"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a01c8eae3b8bfdd2543fdcc1b162debceda54a3c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmbrokerconnections-transact-sql"></a>sys.dm_broker_connections (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada conexão de rede do [!INCLUDE[ssSB](../../includes/sssb-md.md)]. A tabela a seguir fornece mais informações:  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**connection_id**|**uniqueidentifier**|Identificador da conexão. É NULLABLE.|  
|**transport_stream_id**|**uniqueidentifier**|Identificador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexão de Interface de rede (SNI) usado por essa conexão para comunicações de TCP/IP. É NULLABLE.|  
|**estado**|**smallint**|O estado atual da conexão. É NULLABLE. Valores possíveis:<br /><br /> 1 = NEW<br /><br /> 2 = CONNECTING<br /><br /> 3 = CONNECTED<br /><br /> 4 = LOGGED_IN<br /><br /> 5 = FECHADO|  
|**state_desc**|**nvarchar (60)**|O estado atual da conexão. É NULLABLE. Valores possíveis:<br /><br /> NEW<br /><br /> CONNECTING<br /><br /> CONNECTED<br /><br /> LOGGED_IN<br /><br /> CLOSED|  
|**connect_time**|**datetime**|A data e hora em que a conexão foi aberta. É NULLABLE.|  
|**login_time**|**datetime**|Date e hora em que o logon da conexão foi efetuado. É NULLABLE.|  
|**authentication_method**|**nvarchar (128)**|Nome do método de Autenticação do Windows, como NTLM ou KERBEROS. O valor é fornecido pelo Windows. É NULLABLE.|  
|**principal_name**|**nvarchar (128)**|Nome do logon que foi validado para permissões de conexão. Para autenticação do Windows, este valor é o nome de usuário remoto. Para autenticação de certificado, esse valor é o proprietário do certificado. É NULLABLE.|  
|**remote_user_name**|**nvarchar (128)**|Nome do usuário de mesmo nível do outro banco de dados que é usado pela Autenticação do Windows. É NULLABLE.|  
|**last_activity_time**|**datetime**|Data e hora mais recente na qual a conexão foi usada para enviar ou receber informações. É NULLABLE.|  
|**is_accept**|**bit**|Indica se a conexão foi originada no lado remoto. É NULLABLE.<br /><br /> 1 = a conexão é uma solicitação aceita da instância remota.<br /><br /> 0 = a conexão foi iniciada pela instância local.|  
|**login_state**|**smallint**|Estado do processo de logon dessa conexão. Valores possíveis:<br /><br /> 0 = INITIAL<br /><br /> 1 = WAIT LOGIN NEGOTIATE<br /><br /> 2 = ONE ISC<br /><br /> 3 = ONE ASC<br /><br /> 4 = TWO ISC<br /><br /> 5 = TWO ASC<br /><br /> 6 = WAIT ISC Confirm<br /><br /> 7 = WAIT ASC Confirm<br /><br /> 8 = WAIT REJECT<br /><br /> 9 = WAIT PRE-MASTER SECRET<br /><br /> 10 = WAIT VALIDATION<br /><br /> 11 = WAIT ARBITRATION<br /><br /> 12 = ON-LINE<br /><br /> 13 = ERROR|  
|**login_state_desc**|**nvarchar (60)**|Estado atual de logon do computador remoto. Valores possíveis:<br /><br /> O handshake da conexão está sendo inicializado.<br /><br /> O handshake da conexão está esperando a mensagem de Negociação de Logon.<br /><br /> O handshake da conexão foi inicializado e enviou o contexto de segurança para autenticação.<br /><br /> O handshake da conexão recebeu e aceitou o contexto de segurança para autenticação.<br /><br /> O handshake da conexão foi inicializado e enviou o contexto de segurança para autenticação. Há um mecanismo opcional disponível para autenticar os pares.<br /><br /> O handshake da conexão recebeu e enviou o contexto de segurança aceito para autenticação. Há um mecanismo opcional disponível para autenticar os pares.<br /><br /> O handshake da conexão está esperando a mensagem de Confirmação para Inicializar o Contexto de Segurança.<br /><br /> O handshake da conexão está esperando a mensagem de Confirmação para Aceitar o Contexto de Segurança.<br /><br /> O handshake da conexão está esperando a mensagem de rejeição de SSPI para autenticação com falha.<br /><br /> O handshake da conexão está esperando a mensagem de Segredo Pré-masterizado.<br /><br /> O handshake da conexão está esperando a mensagem de Validação.<br /><br /> O handshake da conexão está esperando a mensagem de Arbitragem.<br /><br /> O handshake da conexão está concluído e online (pronto) para a troca de mensagens.<br /><br /> A conexão está em estado de erro.|  
|**peer_certificate_id**|**int**|A ID de objeto local do certificado usado pela instância remota para autenticação. O proprietário deste certificado deve ter permissões CONNECT no ponto de extremidade do [!INCLUDE[ssSB](../../includes/sssb-md.md)]. É NULLABLE.|  
|**encryption_algorithm**|**smallint**|Algoritmo de criptografia usado para esta conexão. É NULLABLE. Valores possíveis:<br /><br /> **Valor &#124; Descrição &#124; Opção de DDL correspondente**<br /><br /> 0 &#124; Nenhum &#124; Desabilitado<br /><br /> 1 &#124; ASSINATURA<br /><br /> 2 &#124; AES RC4 &#124; Necessário &#124; Algoritmo RC4 obrigatório}<br /><br /> 3 &#124; AES &#124; Algoritmo AES obrigatório<br /><br /> **Observação:** o algoritmo RC4 é suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. Em [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versões posteriores, o material criptografado usando RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.|  
|**encryption_algorithm_desc**|**nvarchar (60)**|Representação textual do algoritmo de criptografia. É NULLABLE. Valores possíveis:<br /><br /> **Descrição &#124; Opção de DDL correspondente**<br /><br /> Nenhum &#124; Desabilitado<br /><br /> RC4 &#124; {Necessário &#124; Necessário o algoritmo RC4}<br /><br /> AES &#124; Algoritmo AES obrigatório<br /><br /> NONE, RC4 &#124; {Com suporte &#124; Com suporte do algoritmo RC4}<br /><br /> Nenhum, AES &#124; Com suporte do algoritmo RC4<br /><br /> RC4, AES &#124; Algoritmo RC4 obrigatório AES<br /><br /> AES RC4 &#124; Necessário o algoritmo AES RC4<br /><br /> NONE, RC4, AES &#124; Suporte para o algoritmo RC4 AES<br /><br /> Nenhum, AES, RC4 &#124;  Com suporte o algoritmo AES RC4|  
|**receives_posted**|**smallint**|Número de recebimentos de rede assíncrona desta conexão que ainda não foram concluídos. É NULLABLE.|  
|**is_receive_flow_controlled**|**bit**|Se os recebimentos de rede foram adiados pelo controle de fluxo porque a rede está ocupada. É NULLABLE.<br /><br /> 1 = True|  
|**sends_posted**|**smallint**|Número de envios de rede assíncrona desta conexão que ainda não foram concluídos. É NULLABLE.|  
|**is_send_flow_controlled**|**bit**|Se os envios de rede foram adiados pelo controle de fluxo de rede porque a rede está ocupada. É NULLABLE.<br /><br /> 1 = True|  
|**total_bytes_sent**|**bigint**|Número total de bytes enviados por esta conexão. É NULLABLE.|  
|**total_bytes_received**|**bigint**|Número total de bytes recebidos por esta conexão. É NULLABLE.|  
|**total_fragments_sent**|**bigint**|Número total de fragmentos de mensagens do [!INCLUDE[ssSB](../../includes/sssb-md.md)] enviados por esta conexão. É NULLABLE.|  
|**total_fragments_received**|**bigint**|Número total de fragmentos de mensagens do [!INCLUDE[ssSB](../../includes/sssb-md.md)] recebidos por esta conexão. É NULLABLE.|  
|**total_sends**|**bigint**|Número total de solicitações de envio de rede emitidas por esta conexão. É NULLABLE.|  
|**total_receives**|**bigint**|Número total de solicitações de recebimento de rede emitidas por esta conexão. É NULLABLE.|  
|**peer_arbitration_id**|**uniqueidentifier**|Identificador interno para o ponto de extremidade. É NULLABLE.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="physical-joins"></a>Junções físicas  
 ![Junções para sys.DM broker_connections](../../relational-databases/system-dynamic-management-views/media/join-dm-broker-connections-1.gif "junções para sys.DM broker_connections")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|**dm_broker_connections.connection_id**|**dm_exec_connections.connection_id**|Um para um|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

