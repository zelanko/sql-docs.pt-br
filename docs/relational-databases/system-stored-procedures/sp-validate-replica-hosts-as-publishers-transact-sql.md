---
title: sp_validate_replica_hosts_as_publishers (T-SQL)
description: Descreve o sp_validate_replica_hosts_as_publishers procedimento armazenado que permite que todas as réplicas secundárias sejam validadas.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validate_replica_hosts_as_publishers_TSQL
- sp_validate_replica_hosts_as_publishers
helpviewer_keywords:
- sp_validate_replica_hosts_as_publishers
ms.assetid: 45001fc9-2dbd-463c-af1d-aa8982d8c813
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9375be2a2af2b7653b3f0f036405533f1571ff3f
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2019
ms.locfileid: "75319986"
---
# <a name="sp_validate_replica_hosts_as_publishers-transact-sql"></a>sp_validate_replica_hosts_as_publishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  **sp_validate_replica_hosts_as_publishers** é uma extensão de **sp_validate_redirected_publisher** que permite que todas as réplicas secundárias sejam validadas, em vez de apenas a réplica primária atual. **sp_validate_replicat_hosts_as_publisher** valida uma topologia de replicação de Always on inteira. **sp_validate_replica_hosts_as_publishers** deve ser executado diretamente no distribuidor usando uma sessão de área de trabalho remota para evitar um erro de segurança de salto duplo (21892).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_validate_replica_hosts_as_publishers   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @original_publisher = ] 'original_publisher'`O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que originalmente publicou o banco de dados. *original_publisher* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'`O nome do banco de dados que está sendo publicado. *publisher_db* é **sysname**, sem padrão.  
  
`[ @redirected_publisher = ] 'redirected_publisher'`O destino de redirecionamento quando **sp_redirect_publisher** foi chamado para o par Publicador original/banco de dados publicado. *redirected_publisher* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum.  
  
## <a name="remarks"></a>Comentários  
 Se não existir nenhuma entrada para o Publicador e o banco de dados de publicação, **sp_validate_redirected_publisher** retornará NULL para o parâmetro * \@* de saída redirected_publisher. Caso contrário, o publicador redirecionado associado será retornado, nos casos de êxito e de falha.  
  
 Se a validação for bem-sucedida, **sp_validate_redirected_publisher** retornará uma indicação de êxito.  
  
 Se a validação falhar, serão emitidos erros apropriados.  **sp_validate_redirected_publisher** faz um melhor esforço para gerar todos os problemas e não apenas o primeiro encontrado.  
  
> [!NOTE]  
>  **sp_validate_replica_hosts_as_publishers** falhará com o seguinte erro ao validar hosts de réplica secundária que não permitem acesso de leitura ou exigir que a intenção de leitura seja especificada.  
>   
>  Msg 21899, Level 11, State 1, Procedure **sp_hadr_verify_subscribers_at_publisher**, Line 109  
>   
>  A consulta ao publicador redirecionado 'MyReplicaHostName' para determinar se havia entradas de sysserver para os assinantes do publicador original 'MyOriginalPublisher' falhou com erro '976', mensagem de erro 'Erro 976, Nível 14, Estado 1, Mensagem: O banco de dados de destino, 'MyPublishedDB', está participando de um grupo de disponibilidade e no momento não está acessível para consultas. Qualquer movimento de dados é suspenso ou a réplica de disponibilidade não é habilitada para acesso de leitura. Para permitir o acesso somente leitura a esse banco de dados e a outros no grupo de disponibilidade, habilite o acesso de leitura para uma ou mais réplicas de disponibilidade secundárias no grupo.  Para obter mais informações, consulte a instrução **ALTER AVAILABILITY GROUP** nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
>   
>  Foram encontrados um ou mais erros de validação de publicador para o host de réplica 'MyReplicaHostName'.  
  
## <a name="permissions"></a>Permissões  
 O chamador deve ser um membro da função de servidor fixa **sysadmin** , a **db_owner** função fixa de banco de dados para o banco de dados de distribuição ou um membro de uma lista de acesso à publicação para uma publicação definida associada ao banco de dados Publicador.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_get_redirected_publisher](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_redirect_publisher](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_validate_redirected_publisher](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)  
  
  
