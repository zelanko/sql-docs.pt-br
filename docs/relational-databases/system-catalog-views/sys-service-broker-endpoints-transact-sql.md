---
title: sys.service_broker_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f93ac0b4a11e10d3db952fd850f4c83668a97d3b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855264"
---
# <a name="sysservicebrokerendpoints-transact-sql"></a>sys.service_broker_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Essa exibição do catálogo contém uma linha para o ponto de extremidade do Service Broker. Para cada linha nesta exibição, há uma linha correspondente com o mesmo **endpoint_id** na **sys. tcp_endpoints** exibição que contém os metadados de configuração de TCP. TCP é o único protocolo permitido para o Service Broker.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<herdado colunas >**|**--**|Herda colunas de [Endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**is_message_forwarding_enabled**|**bit**|Faz com que o ponto de extremidade ofereça suporte ao encaminhamento de mensagens. Inicialmente, isso é definido como **0** (desabilitado). Não é NULLABLE.|  
|**message_forwarding_size**|**int**|O número máximo de megabytes de **tempdb** espaço pode ser usado para mensagens encaminhadas. Inicialmente, isso é definido como **10**. Não é NULLABLE.|  
|**connection_auth**|**tinyint**|O tipo de autenticação de conexão exigido para conexões com este ponto de extremidade; um dentre:<br /><br /> **1** - NTLM<br /><br /> **2** -KERBEROS<br /><br /> **3** -NEGOCIAR<br /><br /> **4** -CERTIFICADO<br /><br /> **5** -NTLM, O CERTIFICADO<br /><br /> **6** -KERBEROS, O CERTIFICADO<br /><br /> **7** -NEGOCIAR, DE CERTIFICADO<br /><br /> **8** -CERTIFICADO, NTLM<br /><br /> **9** -CERTIFICADO, O KERBEROS<br /><br /> **10** -CERTIFICADO, NEGOTIATE<br /><br /> Não é NULLABLE.|  
|**connection_auth_desc**|**nvarchar(60)**|Descrição do tipo de autenticação de conexão exigido para conexões com esse ponto de extremidade, que pode ser um destes:<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM, CERTIFICATE<br /><br /> KERBEROS, CERTIFICATE<br /><br /> NEGOTIATE, CERTIFICATE<br /><br /> CERTIFICATE, NTLM<br /><br /> CERTIFICATE, KERBEROS<br /><br /> CERTIFICATE, NEGOTIATE<br /><br /> É NULLABLE.|  
|**certificate_id**|**int**|ID de certificado usado para autenticação, se houver.<br /><br /> 0 = Está sendo usada a Autenticação do Windows.|  
|**encryption_algorithm**|**tinyint**|Algoritmo de criptografia. A seguir estão os possíveis valores com suas descrições e opções de DDL correspondentes.<br /><br /> **0** : NONE. Opção de DDL correspondente: Desabilitado.<br /><br /> **1** :  RC4. Opção de DDL correspondente: {necessária &#124; algoritmo RC4 obrigatório}.<br /><br /> **2** : AES. Opção de DDL correspondente: Algoritmo AES obrigatório.<br /><br /> **3** : NONE, RC4. Opção de DDL correspondente: {com suporte &#124; suporte para o algoritmo RC4}.<br /><br /> **4** : NENHUM, AES. Opção de DDL correspondente: Suporte para o algoritmo AES.<br /><br /> **5** : RC4, AES. Opção de DDL correspondente: Algoritmo RC4 obrigatório AES.<br /><br /> **6** : AES, RC4. Opção de DDL correspondente: Necessário algoritmo AES RC4.<br /><br /> **7** : NONE, RC4, AES. Opção de DDL correspondente: Suporte para o algoritmo RC4 AES.<br /><br /> **8** : NONE, AES, RC4. Opção de DDL correspondente: Suporte para o algoritmo AES RC4.<br /><br /> Não é NULLABLE.|  
|**encryption_algorithm_desc**|**nvarchar(60)**|Descrição do algoritmo de criptografia. Os valores possíveis e suas opções de DDL correspondentes são listadas abaixo:<br /><br /> NENHUM: Desabilitado<br /><br /> RC4: {necessária &#124; algoritmo RC4 obrigatório}<br /><br /> AES: Algoritmo AES obrigatório<br /><br /> NONE, RC4: {com suporte &#124; suporte para o algoritmo RC4}<br /><br /> NENHUM, AES: Algoritmo AES com suporte<br /><br /> RC4, AES : Algoritmo RC4 obrigatório AES<br /><br /> AES, RC4 : Necessário algoritmo AES RC4<br /><br /> NONE, RC4, AES : Suporte para o algoritmo RC4 AES<br /><br /> NENHUM, AES, RC4: Com suporte do algoritmo AES RC4<br /><br /> É NULLABLE.|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]  
>  O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e em versões posteriores, o material criptografado por meio do algoritmo RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)  
  
  
