---
title: sys.database_mirroring_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring_endpoints_TSQL
- database_mirroring_endpoints
- sys.database_mirroring_endpoints
- database_mirroring_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], endpoint
- HADR [SQL Server], endpoint
- database mirroring [SQL Server], catalog views
- sys.database_mirroring_endpoints catalog view
ms.assetid: f2285199-97ad-473c-a52d-270044dd862b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0aa757203ba82794a0564e50c715134e502c6ac1
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52538071"
---
# <a name="sysdatabasemirroringendpoints-transact-sql"></a>sys.database_mirroring_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para o banco de dados que reflete o ponto de extremidade de uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  O ponto de extremidade de espelhamento de banco de dados oferece suporte a ambas as sessões entre parceiros de espelhamento de banco de dados e com testemunhas e sessões entre a réplica primária de um grupo de disponibilidade AlwaysOn e suas réplicas secundárias.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<herdado colunas >**|-|Herda colunas de **Endpoints** (para obter mais informações, consulte [sys. Endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)).|  
|**role**|**tinyint**|Função de reflexão; uma dentre:<br /><br /> **0** = nenhum<br /><br /> **1** = partner<br /><br /> **2** = testemunha<br /><br /> **3** = all<br /><br /> Observação: Esse valor é relevante somente para espelhamento de banco de dados.|  
|**role_desc**|**nvarchar(60)**|Descrição da função de reflexão; uma dentre:<br /><br /> **NONE**<br /><br /> **PARCEIRO**<br /><br /> **TESTEMUNHA**<br /><br /> **ALL**<br /><br /> Observação: Esse valor é relevante somente para espelhamento de banco de dados.|  
|**is_encryption_enabled**|**bit**|**1** significa que a criptografia está habilitada.<br /><br /> **0** significa que a criptografia está desabilitada.|  
|**connection_auth**|**tinyint**|O tipo de autenticação de conexão exigido para conexões com este ponto de extremidade; um dentre:<br /><br /> **1** -NTLM<br /><br /> **2** -KERBEROS<br /><br /> **3** -NEGOCIAR<br /><br /> **4** -CERTIFICADO<br /><br /> **5** -NTLM, O CERTIFICADO<br /><br /> **6** -KERBEROS, O CERTIFICADO<br /><br /> **7** -NEGOCIAR, DE CERTIFICADO<br /><br /> **8** -CERTIFICADO, NTLM<br /><br /> **9** -CERTIFICADO, O KERBEROS<br /><br /> **10** -CERTIFICADO, NEGOTIATE|  
|**connection_auth_desc**|**Nvarchar (60)**|Descrição do tipo de autenticação de conexão exigido para conexões com este ponto de extremidade; uma dentre:<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM, CERTIFICATE<br /><br /> KERBEROS, CERTIFICATE<br /><br /> NEGOTIATE, CERTIFICATE<br /><br /> CERTIFICATE, NTLM<br /><br /> CERTIFICATE, KERBEROS<br /><br /> CERTIFICATE, NEGOTIATE|  
|**certificate_id**|**int**|ID de certificado usado para autenticação, se houver.<br /><br /> 0 = Está sendo usada a Autenticação do Windows.|  
|**encryption_algorithm**|**tinyint**|Algoritmo de criptografia; um dentre:<br /><br /> **0** -NONE<br /><br /> **1** -RC4<br /><br /> **2** -AES<br /><br /> **3** -NONE, RC4<br /><br /> **4** -NONE, AES<br /><br /> **5** -RC4, AES<br /><br /> **6** -AES, RC4<br /><br /> **7** -NONE, RC4, AES<br /><br /> **8** -NONE, AES, RC4|  
|**encryption_algorithm_desc**|**nvarchar(60)**|Descrição do algoritmo de criptografia; uma dentre:<br /><br /> Nenhuma<br /><br /> RC4<br /><br /> AES<br /><br /> NONE, RC4<br /><br /> NONE, AES<br /><br /> RC4, AES<br /><br /> AES, RC4<br /><br /> NONE, RC4, AES<br /><br /> NONE, AES, RC4|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]  
>  O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e superior, o material criptografado usando RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Especifique a URL de ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)   
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [sys.database_mirroring &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
