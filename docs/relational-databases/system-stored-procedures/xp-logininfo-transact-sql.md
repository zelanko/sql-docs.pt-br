---
title: xp_logininfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_logininfo_TSQL
- xp_logininfo
dev_langs:
- TSQL
helpviewer_keywords:
- xp_logininfo
ms.assetid: ee7162b5-e11f-4a0e-a09c-1878814dbbbd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b5a1a7067e1ebda150d0236020288514eb90a8fc
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890730"
---
# <a name="xp_logininfo-transact-sql"></a>xp_logininfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre os usuários e grupos do Windows.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xp_logininfo [ [ @acctname = ] 'account_name' ]   
     [ , [ @option = ] 'all' | 'members' ]   
     [ , [ @privilege = ] variable_name OUTPUT]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @acctname = ] 'account_name'`É o nome de um usuário ou grupo do Windows com acesso concedido ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *account_name* é **sysname**, com um padrão de NULL. Se *account_name* não for especificado, todos os grupos do Windows e usuários do Windows que receberam permissão de logon explicitamente serão relatados. *account_name* deve ser totalmente qualificado. Por exemplo, 'ADVWKS4\macraes' ou 'BUILTIN\Administrators'.  
  
 **' todos '**  |  **' Members '**  
 Especifica se as informações sobre todos os caminhos de permissão para a conta ou sobre os membros do grupo do Windows devem ser relatadas. a ** \@ opção** é **varchar (10)**, com um padrão de NULL. A menos que **All** seja especificado, somente o primeiro caminho de permissão é exibido.  
  
`[ @privilege = ] variable_name`É um parâmetro de saída que retorna o nível de privilégio da conta do Windows especificada. *variable_name* é **varchar (10)**, com um padrão de ' not desejable '. O nível de privilégio retornado é **usuário**, **administrador**ou **nulo**.  
  
 OUTPUT  
 Quando especificado, coloca *variable_name* no parâmetro de saída.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**nome da conta**|**sysname**|Nome da conta do Windows completamente qualificada.|  
|**type**|**Char (8)**|Tipo de conta do Windows. Os valores válidos são **User** ou **Group**.|  
|**privilégio**|**char(9)**|Privilégio de acesso para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os valores válidos são **admin**, **User**ou **NULL**.|  
|**mapped login name**|**sysname**|Para contas de usuário que têm privilégio de usuário, **nome de logon mapeado** mostra o nome de logon mapeado que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta usar ao fazer logon com essa conta usando as regras mapeadas com o nome de domínio adicionado antes dela.|  
|**permission path**|**sysname**|Associação de grupo que permitiu o acesso à conta.|  
  
## <a name="remarks"></a>Comentários  
 Se *account_name* for especificado, **xp_logininfo** relatará o nível de privilégio mais alto do usuário ou grupo do Windows especificado. Se um usuário do Windows tiver acesso como administrador de sistema e como usuário de domínio, ele será relatado como um administrador de sistema. Se o usuário for membro de vários grupos do Windows com o mesmo nível de privilégio, somente o grupo ao qual o acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi concedido primeiro será relatado.  
  
 Se *account_name* for um usuário ou grupo válido do Windows que não esteja associado a um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon, um conjunto de resultados vazio será retornado. Se *account_name* não puder ser identificado como um usuário ou grupo válido do Windows, uma mensagem de erro será retornada.  
  
 Se *account_name* e **todos** forem especificados, todos os caminhos de permissão para o usuário ou grupo do Windows serão retornados. Se *account_name* for um membro de vários grupos, todos os quais receberam acesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , várias linhas serão retornadas. As linhas de privilégio de **administrador** são retornadas antes das linhas de privilégio de **usuário** e dentro de uma linha de nível de privilégio são retornadas na ordem em que os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logons correspondentes foram criados.  
  
 Se *account_name* e **Membros** forem especificados, uma lista dos membros de nível posterior do grupo será retornada. Se *account_name* for um grupo local, a listagem poderá incluir usuários locais, usuários de domínio e grupos. Se *account_name* for uma conta de domínio, a lista será composta de usuários de domínio. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve conectar-se ao controlador de domínio para recuperar informações de associação de grupo. Se o servidor não puder contatar o controlador de domínio, nenhuma informação será retornada.  
  
 **xp_logininfo** retorna informações de Active Directory grupos globais, não de grupos universais.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa **sysadmin** ou associação na função de banco de dados fixa **pública** no banco de dados **mestre** com a permissão de execução concedida.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exibe informações sobre o grupo do Windows `BUILTIN\Administrators`.  
  
```  
EXEC xp_logininfo 'BUILTIN\Administrators';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_denylogin](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_revokelogin](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados estendidos gerais &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
