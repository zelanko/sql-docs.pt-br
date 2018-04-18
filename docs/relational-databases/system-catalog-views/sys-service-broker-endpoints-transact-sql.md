---
title: sys.service_broker_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.service_broker_endpoints_TSQL
- service_broker_endpoints
- service_broker_endpoints_TSQL
- sys.service_broker_endpoints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_broker_endpoints catalog view
ms.assetid: 6979ec9b-0043-411e-aafb-0226fa26c5ba
caps.latest.revision: 51
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e9bfbe05a6cef26dc891c0b2b8069c26ec4a55e5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysservicebrokerendpoints-transact-sql"></a>sys.service_broker_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Essa exibição do catálogo contém uma linha para o ponto de extremidade do Service Broker. Para cada linha nessa exibição, há uma linha correspondente com o mesmo **endpoint_id** no **tcp_endpoints** exibição que contém os metadados de configuração de TCP. TCP é o único protocolo permitido para o Service Broker.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**\<herdado colunas >**|**--**|Herda colunas de [Endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**is_message_forwarding_enabled**|**bit**|Faz com que o ponto de extremidade ofereça suporte ao encaminhamento de mensagens. Isso é definido inicialmente como **0** (desabilitado). Não é NULLABLE.|  
|**message_forwarding_size**|**Int**|O número máximo de megabytes de **tempdb** espaço pode ser usado para mensagens encaminhadas. Isso é definido inicialmente como **10**. Não é NULLABLE.|  
|**connection_auth**|**tinyint**|O tipo de autenticação de conexão exigido para conexões com este ponto de extremidade; um dentre:<br /><br /> **1** -NTLM<br /><br /> **2** -KERBEROS<br /><br /> **3** -NEGOCIAR<br /><br /> **4** -CERTIFICADO<br /><br /> **5** -NTLM, CERTIFICADOS<br /><br /> **6** -KERBEROS, O CERTIFICADO<br /><br /> **7** -NEGOTIATE, DE CERTIFICADO<br /><br /> **8** -CERTIFICADO, NTLM<br /><br /> **9** -CERTIFICADO, O KERBEROS<br /><br /> **10** -CERTIFICADO, NEGOTIATE<br /><br /> Não é NULLABLE.|  
|**connection_auth_desc**|**nvarchar(60)**|Descrição do tipo de autenticação de conexão exigido para conexões com esse ponto de extremidade, que pode ser um destes:<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM, CERTIFICATE<br /><br /> KERBEROS, CERTIFICATE<br /><br /> NEGOTIATE, CERTIFICATE<br /><br /> CERTIFICATE, NTLM<br /><br /> CERTIFICATE, KERBEROS<br /><br /> CERTIFICATE, NEGOTIATE<br /><br /> É NULLABLE.|  
|**certificate_id**|**Int**|ID de certificado usado para autenticação, se houver.<br /><br /> 0 = Está sendo usada a Autenticação do Windows.|  
|**encryption_algorithm**|**tinyint**|Algoritmo de criptografia. A seguir estão os valores possíveis com suas descrições e opções de DDL correspondentes.<br /><br /> **0** : NONE. Opção de DDL correspondente: desabilitado.<br /><br /> **1** :  RC4. Opção de DDL correspondente: {necessário &#124; algoritmo RC4 obrigatório}.<br /><br /> **2** : AES. Opção de DDL correspondente: necessário algoritmo AES.<br /><br /> **3** : NONE, RC4. Opção de DDL correspondente: {com suporte &#124; suporte para o algoritmo RC4}.<br /><br /> **4** : NONE, AES. Opção de DDL correspondente: suporte para o algoritmo AES.<br /><br /> **5** : RC4, AES. Opção de DDL correspondente: necessário algoritmo RC4 AES.<br /><br /> **6** : AES, RC4. Opção de DDL correspondente: algoritmo AES RC4 obrigatório.<br /><br /> **7** : NONE, RC4, AES. Opção de DDL correspondente: suporte para o algoritmo RC4 AES.<br /><br /> **8** : NONE, AES RC4. Opção de DDL correspondente: suporte para o algoritmo AES RC4.<br /><br /> Não é NULLABLE.|  
|**encryption_algorithm_desc**|**nvarchar(60)**|Descrição do algoritmo de criptografia. Suas opções de DDL correspondentes e os valores possíveis estão listadas abaixo:<br /><br /> NONE: desabilitado<br /><br /> RC4: {necessário &#124; algoritmo RC4 obrigatório}<br /><br /> AES: Algoritmo AES obrigatório<br /><br /> NONE, RC4: {suporte &#124; suporte para o algoritmo RC4}<br /><br /> Nenhum, AES: Suporte para o algoritmo AES<br /><br /> RC4, AES: Algoritmo RC4 obrigatório AES<br /><br /> AES, RC4: Necessário algoritmo AES RC4<br /><br /> NONE, RC4, AES: Suporte para o algoritmo RC4 AES<br /><br /> NONE, AES RC4: O algoritmo AES RC4 com suporte<br /><br /> É NULLABLE.|  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]  
>  O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e em versões posteriores, o material criptografado por meio do algoritmo RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [CRIAR PONTO DE EXTREMIDADE &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)  
  
  
