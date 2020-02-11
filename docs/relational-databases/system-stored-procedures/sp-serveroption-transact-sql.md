---
title: sp_serveroption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_serveroption_TSQL
- sp_serveroption
dev_langs:
- TSQL
helpviewer_keywords:
- 7343 (Database Engine error)
- sp_serveroption
ms.assetid: 47d04a2b-dbf0-4f15-bd9b-81a2efc48131
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1fcd6f158908893ce5eb86c24a3bb3882867bc2d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104377"
---
# <a name="sp_serveroption-transact-sql"></a>sp_serveroption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define opções de servidor para servidores remotos e servidores vinculados.  
  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_serveroption [@server = ] 'server'   
      ,[@optname = ] 'option_name'       
      ,[@optvalue = ] 'option_value' ;  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @server = ] 'server'`É o nome do servidor para o qual definir a opção. o *servidor* é **sysname**, sem padrão.  
  
`[ @optname = ] 'option_name'`É a opção a ser definida para o servidor especificado. *option_name* é **varchar (** 35 **)**, sem padrão. *option_name* pode ser qualquer um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**compatível com agrupamento**|Afeta a execução da Consulta Distribuída nos servidores vinculados. Se essa opção for definida como **true**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o assumirá que todos os caracteres no servidor vinculado são compatíveis com o servidor local, em relação ao conjunto de caracteres e à sequência de agrupamento (ou à ordem de classificação). Isso permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envie comparações sobre colunas de caracteres ao provedor. Se essa opção não estiver definida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre avaliará comparações sobre colunas de caracteres localmente.<br /><br /> Essa opção deve ser definida somente se você tiver certeza de que a fonte de dados correspondente ao servidor vinculado tem o mesmo conjunto de caracteres e ordem de classificação do servidor local.|  
|**nome do agrupamento**|Especifica o nome do agrupamento usado pela fonte de dados remota se **usar agrupamento remoto** for **true** e a fonte de dados não for uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fonte de dados. O nome deve ser uma das ordenações que têm suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Use essa opção ao acessar uma origem de dados OLE DB diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas cuja ordenação coincide com uma das ordenações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> O servidor vinculado deve fornecer suporte a uma única ordenação a ser usada para todas as colunas naquele servidor. Não defina essa opção se o servidor vinculado fornecer suporte a várias ordenações dentro de uma única fonte de dados ou se a ordenação do servidor vinculado não puder ser determinada para corresponder a uma das ordenações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**tempo limite de conexão**|Valor de tempo limite em segundos para se conectar a um servidor vinculado.<br /><br /> Se **0**, use a **sp_configure** padrão.|  
|**acesso a dados**|Habilita e desabilita um servidor vinculado para o acesso às consultas distribuídas. Pode ser usado somente para entradas **Sys. Server** adicionadas por meio de **sp_addlinkedserver**.|  
|**dist**|Distribuidor.|  
|**validação de esquema lenta**|Determina se o esquema de tabelas remotas será verificado.<br /><br /> Se **for true**, ignorará a verificação de esquema de tabelas remotas no início da consulta.|  
|**pub**|Editor.|  
|**tempo limite da consulta**|O valor do tempo limite para consultas em um servidor vinculado.<br /><br /> Se **0**, use a **sp_configure** padrão.|  
|**RPC**|Habilita RPC a partir do servidor fornecido.|  
|**saída de RPC**|Habilita RPC para o servidor fornecido.|  
|**projeto**|Farão.|  
|**sistema**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**usar agrupamento remoto**|Determina se a ordenação de uma coluna remota ou de um servidor local será usada.<br /><br /> Se **for true**, o agrupamento de colunas remotas será [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado para fontes de dados e o Agrupamento especificado no **nome do agrupamento** será usado[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fontes que não são de dados.<br /><br /> Se **for false**, as consultas distribuídas sempre usarão o agrupamento padrão do servidor local, enquanto o **nome do agrupamento** e o agrupamento de colunas remotas são ignorados. O padrão é **false**. (O valor **falso** é compatível com a semântica de agrupamento usada em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7,0.)|  
|**promoção de transação de proc remoto**|Use esta opção para proteger as ações de um procedimento servidor a servidor por meio de uma transação do MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ). Quando esta opção for TRUE (ou ON), a chamada de um procedimento armazenado remoto iniciará uma transação distribuída e inscreverá a transação no MS DTC. A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que chama o procedimento armazenado remoto é o que origina a transação e controla a conclusão da transação. Quando as instruções subsequentes COMMIT TRANSACTION ou ROLLBACK TRANSACTION são emitidas para a conexão, a instância controladora solicita que o MS DTC gerencie a conclusão da transação distribuída em todas os computadores envolvidos.<br /><br /> Depois que uma transação distribuída [!INCLUDE[tsql](../../includes/tsql-md.md)] foi iniciada, é possível fazer chamadas de procedimento armazenado remoto a outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que foram definidas como servidores vinculados. Os servidores vinculados são todos inscritos na transação de distribuição do [!INCLUDE[tsql](../../includes/tsql-md.md)], e o MS DTC garante que a transação seja completada em cada servidor vinculado.<br /><br /> Se essa opção estiver definida como FALSE (ou OFF), uma transação local não será promovida a uma transação distribuída durante a chamada de um procedimento remoto em um servidor vinculado.<br /><br /> Se antes de fazer uma chamada de procedimento de servidor a servidor, a transação já for uma transação distribuída, essa opção não terá efeito. A chamada de procedimento em relação ao servidor vinculado executará sob a mesma transação distribuída.<br /><br /> Se antes de fazer uma chamada de procedimento armazenado de servidor a servidor não houver nenhuma transação ativa, essa opção não terá efeito. Em seguida, o procedimento executa em relação ao servidor vinculado sem transações ativas.<br /><br /> O valor padrão dessa opção é TRUE (ou ON).|  
  
`[ @optvalue = ] 'option_value'`Especifica se a *option_name* deve ou não ser habilitada (**true** ou **on**) ou desabilitada (**false** ou **off**). *option_value* é **varchar (** 10 **)**, sem padrão.  
  
 *option_value* pode ser um inteiro não negativo para as opções **tempo limite de conexão** e **tempo limite de consulta** . Para a opção de **nome de agrupamento** , *option_value* pode ser um nome de agrupamento ou nulo.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Se a opção **compatível com agrupamento** for definida como true, o **nome do agrupamento** será definido automaticamente como NULL. Se o **nome do agrupamento** for definido como um valor não nulo, o **agrupamento compatível** automaticamente será definido como false.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão ALTER ANY LINKED SERVER no servidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir configura um servidor vinculado correspondente a outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `SEATTLE3`, para que seja compatível com ordenação com a instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```sql  
USE master;  
EXEC sp_serveroption 'SEATTLE3', 'collation compatible', 'true';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de consultas distribuídas &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_adddistpublisher](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropdistpublisher](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpserver](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
