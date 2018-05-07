---
title: sys.DM db_mirroring_connections (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_mirroring_connections
- dm_db_mirroring_connections
- sys.dm_db_mirroring_connections_TSQL
- dm_db_mirroring_connections_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_mirroring_connections dynamic management view
ms.assetid: e4df91b6-0240-45d0-ae22-cb2c0d52e0b3
caps.latest.revision: 41
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6f47e52efdca87c064f16199e7a553aacf5536b2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="database-mirroring---sysdmdbmirroringconnections"></a>-O espelhamento de banco de dados sys.DM db_mirroring_connections
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada conexão estabelecida para espelhamento de banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**connection_id**|**uniqueidentifier**|Identificador da conexão.|  
|**transport_stream_id**|**uniqueidentifier**|Identificador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexão de Interface de rede (SNI) usado por essa conexão para comunicações de TCP/IP.|  
|**state**|**smallint**|O estado atual da conexão. Valores possíveis:<br /><br /> 1 = NEW<br /><br /> 2 = CONNECTING<br /><br /> 3 = CONNECTED<br /><br /> 4 = LOGGED_IN<br /><br /> 5 = FECHADO|  
|**state_desc**|**nvarchar(60)**|O estado atual da conexão. Valores possíveis:<br /><br /> NEW<br /><br /> CONNECTING<br /><br /> CONNECTED<br /><br /> LOGGED_IN<br /><br /> CLOSED|  
|**connect_time**|**datetime**|A data e hora em que a conexão foi aberta.|  
|**login_time**|**datetime**|Date e hora em que o logon da conexão foi efetuado.|  
|**authentication_method**|**nvarchar(128)**|Nome do método de Autenticação do Windows, como NTLM ou KERBEROS. O valor é fornecido pelo Windows.|  
|**principal_name**|**nvarchar(128)**|Nome do logon que foi validado para permissões de conexão. Para autenticação do Windows, este valor é o nome de usuário remoto. Para autenticação de certificado, esse valor é o proprietário do certificado.|  
|**remote_user_name**|**nvarchar(128)**|Nome do usuário de mesmo nível do outro banco de dados que é usado pela Autenticação do Windows.|  
|**last_activity_time**|**datetime**|Data e hora mais recente na qual a conexão foi usada para enviar ou receber informações.|  
|**is_accept**|**bit**|Indica se a conexão foi originada no lado remoto.<br /><br /> 1 = a conexão é uma solicitação aceita da instância remota.<br /><br /> 0 = a conexão foi iniciada pela instância local.|  
|**login_state**|**smallint**|Estado do processo de logon dessa conexão. Valores possíveis:<br /><br /> 0 = INITIAL<br /><br /> 1 = WAIT LOGIN NEGOTIATE<br /><br /> 2 = ONE ISC<br /><br /> 3 = ONE ASC<br /><br /> 4 = TWO ISC<br /><br /> 5 = TWO ASC<br /><br /> 6 = WAIT ISC Confirm<br /><br /> 7 = WAIT ASC Confirm<br /><br /> 8 = WAIT REJECT<br /><br /> 9 = WAIT PRE-MASTER SECRET<br /><br /> 10 = WAIT VALIDATION<br /><br /> 11 = WAIT ARBITRATION<br /><br /> 12 = ON-LINE<br /><br /> 13 = ERROR|  
|**login_state_desc**|**nvarchar(60)**|Estado atual de logon do computador remoto. Valores possíveis:<br /><br /> O handshake da conexão está sendo inicializado.<br /><br /> O handshake da conexão está esperando a mensagem de Negociação de Logon.<br /><br /> O handshake da conexão foi inicializado e enviou o contexto de segurança para autenticação.<br /><br /> O handshake da conexão recebeu e aceitou o contexto de segurança para autenticação.<br /><br /> O handshake da conexão foi inicializado e enviou o contexto de segurança para autenticação. Há um mecanismo opcional disponível para autenticar os pares.<br /><br /> O handshake da conexão recebeu e enviou o contexto de segurança aceito para autenticação. Há um mecanismo opcional disponível para autenticar os pares.<br /><br /> O handshake da conexão está esperando a mensagem de Confirmação para Inicializar o Contexto de Segurança.<br /><br /> O handshake da conexão está esperando a mensagem de Confirmação para Aceitar o Contexto de Segurança.<br /><br /> O handshake da conexão está esperando a mensagem de rejeição de SSPI para autenticação com falha.<br /><br /> O handshake da conexão está esperando a mensagem de Segredo Pré-masterizado.<br /><br /> O handshake da conexão está esperando a mensagem de Validação.<br /><br /> O handshake da conexão está esperando a mensagem de Arbitragem.<br /><br /> O handshake da conexão está concluído e online (pronto) para a troca de mensagens.<br /><br /> A conexão está em estado de erro.|  
|**peer_certificate_id**|**Int**|A ID de objeto local do certificado usado pela instância remota para autenticação. O proprietário deste certificado deve ter permissões de CONNECT no ponto de extremidade de espelhamento de banco de dados.|  
|**encryption_algorithm**|**smallint**|Algoritmo de criptografia usado para esta conexão. É NULLABLE. Valores possíveis:<br /><br /> **Valor:** 0<br /><br /> **Descrição:** None<br /><br /> **Opção de DDL:** desabilitado<br /><br /> **Valor:** 1<br /><br /> **Descrição:** RC4<br /><br /> **Opção de DDL:** {necessário &#124; algoritmo RC4 obrigatório}<br /><br /> **Valor:** 2<br /><br /> **Descrição:** AES<br /><br /> **Opção de DDL:** algoritmo AES obrigatório<br /><br /> **Valor:** 3<br /><br /> **Descrição:** None, RC4<br /><br /> **Opção de DDL:** {com suporte &#124; algoritmo RC4 com suporte}<br /><br /> **Valor:** 4<br /><br /> **Descrição:** none, AES<br /><br /> **Opção de DDL:** algoritmo RC4 com suporte<br /><br /> **Valor:** 5<br /><br /> **Descrição:** RC4, AES<br /><br /> **Opção de DDL:** algoritmo RC4 AES obrigatório<br /><br /> **Valor:** 6<br /><br /> **Descrição:** AES, RC4<br /><br /> **Opção de DDL:** algoritmo AES RC4 obrigatório<br /><br /> **Valor:** 7<br /><br /> **Descrição:** NONE, RC4, AES<br /><br /> **Opção de DDL:** suporte para o algoritmo RC4 AES<br /><br /> **Valor:** 8<br /><br /> **Descrição:** NONE, AES RC4<br /><br /> **Opção de DDL:** algoritmo AES RC4 com suporte<br /><br /> **Observação:** o algoritmo RC4 é suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. Em [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versões posteriores, o material criptografado usando RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.|  
|**encryption_algorithm_desc**|**nvarchar(60)**|Representação textual do algoritmo de criptografia. É NULLABLE. Valores possíveis:<br /><br /> **Descrição:** None<br /><br /> **Opção de DDL:** desabilitado<br /><br /> **Descrição:** RC4<br /><br /> **Opção de DDL:** {necessário &#124; algoritmo RC4 obrigatório}<br /><br /> **Descrição:** AES<br /><br /> **Opção de DDL:** necessário algoritmo AES<br /><br /> **Descrição:** NONE, RC4<br /><br /> **Opção de DDL:** {suporte &#124; suporte para o algoritmo RC4}<br /><br /> **Descrição:** NONE, AES<br /><br /> **Opção de DDL:** suporte para o algoritmo RC4<br /><br /> **Descrição:** RC4, AES<br /><br /> **Opção de DDL:** algoritmo RC4 obrigatório AES<br /><br /> **Descrição:** AES, RC4<br /><br /> **Opção de DDL:** algoritmo AES RC4 obrigatório<br /><br /> **Descrição:** NONE, RC4, AES<br /><br /> **Opção de DDL:** suporte para o algoritmo RC4 AES<br /><br /> **Descrição:** NONE, AES RC4<br /><br /> **Opção de DDL:** suporte para o algoritmo AES RC4|  
|**receives_posted**|**smallint**|Número de recebimentos de rede assíncrona desta conexão que ainda não foram concluídos.|  
|**is_receive_flow_controlled**|**bit**|Se os recebimentos de rede foram adiados pelo controle de fluxo porque a rede está ocupada.<br /><br /> 1 = True|  
|**sends_posted**|**smallint**|Número de envios de rede assíncrona desta conexão que ainda não foram concluídos.|  
|**is_send_flow_controlled**|**bit**|Se os envios de rede foram adiados pelo controle de fluxo de rede porque a rede está ocupada.<br /><br /> 1 = True|  
|**total_bytes_sent**|**bigint**|Número total de bytes enviados por esta conexão.|  
|**total_bytes_received**|**bigint**|Número total de bytes recebidos por esta conexão.|  
|**total_fragments_sent**|**bigint**|Número total de fragmentos de mensagens de espelhamento de banco de dados enviados por esta conexão.|  
|**total_fragments_received**|**bigint**|Número total de fragmentos de mensagens de espelhamento de banco de dados recebidos por esta conexão.|  
|**total_sends**|**bigint**|Número total de solicitações envio de rede emitidas por esta conexão.|  
|**total_receives**|**bigint**|Número total de solicitações de recebimento de rede emitidos por esta conexão.|  
|**peer_arbitration_id**|**uniqueidentifier**|Identificador interno para o ponto de extremidade. É NULLABLE.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="physical-joins"></a>Junções físicas  
 ![associação de sys.join_dm_db_mirroring_connections](../../relational-databases/system-dynamic-management-views/media/join-dm-db-mirroring-connections.gif "join para sys.join_dm_db_mirroring_connections")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|**dm_db_mirroring_connections.connection_id**|**dm_exec_connections.connection_id**|Um para um|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
  
