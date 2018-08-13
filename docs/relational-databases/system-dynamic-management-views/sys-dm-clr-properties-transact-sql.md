---
title: sys.dm_clr_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_properties
- sys.dm_clr_properties_TSQL
- dm_clr_properties_TSQL
- dm_clr_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_properties dynamic management view
ms.assetid: 220d062f-d117-46e7-a448-06fe48db8163
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 46eb510f9f943d2f63bd3eb1ea3ee4c2bf5f1a52
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39548746"
---
# <a name="sysdmclrproperties-transact-sql"></a>sys.dm_clr_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Retorna uma linha para cada propriedade relacionada à integração common language runtime (CLR) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluindo a versão e o estado de CLR hospedado. O CLR hospedado é inicializado executando o [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md), [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md), ou [DROP ASSEMBLY](../../t-sql/statements/drop-assembly-transact-sql.md) instruções, ou executando qualquer rotina CLR, tipo ou gatilho. O **sys.dm_clr_properties** exibição não especifica se a execução de código CLR do usuário foi habilitada no servidor. Execução de código CLR do usuário é habilitada usando o [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) procedimento armazenado com o [clr habilitado](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) opção definido como 1.  
  
 O **sys.dm_clr_properties** modo de exibição contém o **nome** e **valor** colunas. Cada linha nesta exibição fornece detalhes sobre uma propriedade do CLR hospedado. Use esta exibição para coletar informações sobre o CLR hospedado, como o diretório de instalação do CLR, a versão do CLR e o estado atual do CLR hospedado. Esta exibição poderá ajudá-lo a determinar se o código de integração CLR não está funcionando devido a problemas com a instalação de CLR no computador do servidor.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|O nome da propriedade.|  
|**value**|**nvarchar(128)**|Valor da propriedade.|  
  
## <a name="properties"></a>Propriedades  
 O **directory** propriedade indica o diretório que o .NET Framework foi instalado no servidor. Pode haver várias instalações do .NET Framework no computador do servidor e o valor dessa propriedade identifica qual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de instalação está sendo usada.  
  
 O **versão** propriedade indica a versão do .NET Framework e o CLR hospedado no servidor.  
  
 O **sys.dm_clr_properties** exibição gerenciada dinâmica pode retornar seis valores diferentes para o **estado** propriedade, que reflete o estado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR hospedado. São eles:  
  
-   Mscoree não está carregado.  
  
-   Mscoree está carregado.  
  
-   Versão de CLR bloqueada com mscoree.  
  
-   CLR é inicializado.  
  
-   Inicialização de CLR falhou permanentemente.  
  
-   CLR é interrompido.  
  
 O **Mscoree não está carregado** e **Mscoree está carregado** estados mostrarão a progressão da inicialização de CLR hospedado na inicialização do servidor e não são mais prováveis de serem vistos.  
  
 O **versão de CLR bloqueada com mscoree** estado pode ser visto em que o CLR hospedado não estiver sendo usado e, assim, ele ainda não foi inicializado. O CLR hospedado é inicializado na primeira vez em uma instrução DDL (como [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)) ou um objeto de banco de dados gerenciado é executado.  
  
 O **CLR é inicializado** estado indica que o CLR hospedado foi inicializado com êxito. Observe que isso não indica se a execução do código CLR do usuário foi habilitada. Se a execução de código CLR do usuário é o primeira habilitada e, em seguida, desabilitada usando o [!INCLUDE[tsql](../../includes/tsql-md.md)] [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) procedimento armazenado, o valor de estado ainda será **CLR é inicializado**.  
  
 O **inicialização de CLR falhou permanentemente** estado indica que o CLR que hospedado Falha na inicialização. A pressão de memória é uma causa provável ou também poderia ser o resultado de uma falha no handshake de hospedagem entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o CLR. Nesse caso, será gerada a mensagem de erro 6512 ou 6513.  
  
 O **CLR é interrompido estado** só é visto quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo desligado.  
  
## <a name="remarks"></a>Remarks  
 As propriedades e os valores dessa exibição pode ser alterado em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devido a aprimoramentos da funcionalidade da integração CLR.  
  
## <a name="permissions"></a>Permissões  
  
Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` permissão no banco de dados.   

## <a name="examples"></a>Exemplos  
 O exemplo a seguir recupera informações sobre o CLR hospedado:  
  
```  
SELECT name, value   
FROM sys.dm_clr_properties;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Common Language Runtime relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
