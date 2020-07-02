---
title: sys. service_broker_endpoints (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a59beeb51d59b00fbd902045f0f1aaebc9322a64
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752906"
---
# <a name="sysservice_broker_endpoints-transact-sql"></a>sys.service_broker_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Essa exibição do catálogo contém uma linha para o ponto de extremidade do Service Broker. Para cada linha nessa exibição, há uma linha correspondente com o mesmo **endpoint_id** na exibição **Sys. tcp_endpoints** que contém os metadados de configuração TCP. TCP é o único protocolo permitido para o Service Broker.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**|**--**|Herda colunas de [pontos sys. end&#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**is_message_forwarding_enabled**|**bit**|Faz com que o ponto de extremidade ofereça suporte ao encaminhamento de mensagens. Inicialmente, isso é definido como **0** (desabilitado). Não é NULLABLE.|  
|**message_forwarding_size**|**int**|O número máximo de megabytes de espaço de **tempdb** permitido para ser usado para mensagens sendo encaminhadas. Inicialmente, isso é definido como **10**. Não é NULLABLE.|  
|**connection_auth**|**tinyint**|O tipo de autenticação de conexão exigido para conexões com este ponto de extremidade; um dentre:<br /><br /> **1** -NTLM<br /><br /> **2** -Kerberos<br /><br /> **3** -negociar<br /><br /> **4** -certificado<br /><br /> **5** -NTLM, certificado<br /><br /> **6** -Kerberos, certificado<br /><br /> **7** -negociar, certificado<br /><br /> **8** -certificado, NTLM<br /><br /> **9** -certificado, Kerberos<br /><br /> **10** -Certificate, Negotiate<br /><br /> Não é NULLABLE.|  
|**connection_auth_desc**|**nvarchar(60)**|Descrição do tipo de autenticação de conexão exigido para conexões com esse ponto de extremidade, que pode ser um destes:<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM, CERTIFICATE<br /><br /> KERBEROS, CERTIFICATE<br /><br /> NEGOTIATE, CERTIFICATE<br /><br /> CERTIFICATE, NTLM<br /><br /> CERTIFICATE, KERBEROS<br /><br /> CERTIFICATE, NEGOTIATE<br /><br /> É NULLABLE.|  
|**certificate_id**|**int**|ID de certificado usado para autenticação, se houver.<br /><br /> 0 = Está sendo usada a Autenticação do Windows.|  
|**encryption_algorithm**|**tinyint**|Algoritmo de criptografia. A seguir estão os possíveis valores com suas descrições e opções DDL correspondentes.<br /><br /> **0** : nenhum. Opção DDL correspondente: desabilitada.<br /><br /> **1** : RC4. Opção DDL correspondente: {Required &#124; algoritmo necessário RC4}.<br /><br /> **2** : AES. Opção DDL correspondente: algoritmo necessário AES.<br /><br /> **3** : nenhum, RC4. Opção DDL correspondente: {supported &#124; algoritmo com suporte RC4}.<br /><br /> **4** : nenhum, AES. Opção DDL correspondente: algoritmo AES com suporte.<br /><br /> **5** : RC4, AES. Opção DDL correspondente: algoritmo necessário RC4 AES.<br /><br /> **6** : AES, RC4. Opção DDL correspondente: algoritmo necessário RC4 AES.<br /><br /> **7** : nenhum, RC4, AES. Opção DDL correspondente: algoritmo RC4 AES.<br /><br /> **8** : nenhum, AES, RC4. Opção DDL correspondente: algoritmo AES RC4.<br /><br /> Não é NULLABLE.|  
|**encryption_algorithm_desc**|**nvarchar(60)**|Descrição do algoritmo de criptografia. Os valores possíveis e suas opções DDL correspondentes estão listados abaixo:<br /><br /> NENHUM: desabilitado<br /><br /> RC4: {Required &#124; algoritmo necessário RC4}<br /><br /> AES: algoritmo necessário AES<br /><br /> NENHUM, RC4: {com suporte &#124; algoritmo RC4}<br /><br /> NENHUM, AES: algoritmo com suporte AES<br /><br /> RC4, AES: algoritmo obrigatório RC4 AES<br /><br /> AES, RC4: algoritmo necessário AES RC4<br /><br /> NENHUM, RC4, AES: algoritmo do RC4 AES com suporte<br /><br /> NENHUM, AES, RC4: algoritmo com suporte RC4 do AES<br /><br /> É NULLABLE.|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]  
>  O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e em versões posteriores, o material criptografado por meio do algoritmo RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)  
  
  
