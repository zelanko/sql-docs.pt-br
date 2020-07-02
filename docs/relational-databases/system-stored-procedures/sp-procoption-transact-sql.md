---
title: sp_procoption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_procoption
- sp_procoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_procoption
ms.assetid: 6f0221bd-70b4-4b04-b15d-722235aceb3c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b8ac7eae727206e0ad9b236229dbfca009529e3d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85645825"
---
# <a name="sp_procoption-transact-sql"></a>sp_procoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Define ou limpa um procedimento armazenado para execução automática. Um procedimento armazenado definido como execução automática é executado toda vez que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_procoption [ @ProcName = ] 'procedure'   
    , [ @OptionName = ] 'option'   
    , [ @OptionValue = ] 'value'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @ProcName = ] 'procedure'`É o nome do procedimento para o qual definir uma opção. o *procedimento* é **nvarchar (776)**, sem padrão.  
  
`[ @OptionName = ] 'option'`É o nome da opção a ser definida. O único valor para a *opção* é **Startup**.  
  
`[ @OptionValue = ] 'value'`É se a opção deve ser definida em (**true** ou **on**) ou off (**false** ou **off**). o *valor* é **varchar (12)**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número de erro (falha)  
  
## <a name="remarks"></a>Comentários  
 Os procedimentos de inicialização devem estar no banco de dados **mestre** e não podem conter parâmetros de entrada ou saída. A execução dos procedimentos armazenados inicia quando todos os bancos de dados são recuperados e a mensagem "A recuperação foi concluída" é registrada na inicialização.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir define um procedimento para execução automática.  
  
```  
EXEC sp_procoption @ProcName = N'<procedure name>'   
    , @OptionName = 'startup'   
    , @OptionValue = 'on';   
```  
  
 O exemplo a seguir interrompe a execução automática de um procedimento.  
  
```  
EXEC sp_procoption @ProcName = N'<procedure name>'      
    , @OptionName = 'startup'
    , @OptionValue = 'off';   
```  
  
## <a name="see-also"></a>Consulte Também  
 [Executar um procedimento armazenado](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)  
  
  
