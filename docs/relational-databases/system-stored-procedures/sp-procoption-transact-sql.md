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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 218371ab6d8133dbaf1865eeffc11f92883b4305
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533668"
---
# <a name="spprocoption-transact-sql"></a>sp_procoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define ou limpa um procedimento armazenado para execução automática. Um procedimento armazenado que é definido como execuções de execução automática sempre que uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_procoption [ @ProcName = ] 'procedure'   
    , [ @OptionName = ] 'option'   
    , [ @OptionValue = ] 'value'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @ProcName = ] 'procedure'` É o nome do procedimento para o qual definir uma opção. *procedimento* está **nvarchar(776)**, sem padrão.  
  
`[ @OptionName = ] 'option'` É o nome da opção a ser definido. O único valor para *opção* é **inicialização**.  
  
`[ @OptionValue = ] 'value'` Se deseja definir a opção on (**true** ou **na**) ou desativado (**false** ou **off**). *valor* está **varchar(12)**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número de erro (falha)  
  
## <a name="remarks"></a>Comentários  
 Procedimentos de inicialização devem estar na **mestre** de banco de dados e não pode conter parâmetros de entrada ou saída. A execução dos procedimentos armazenados inicia quando todos os bancos de dados são recuperados e a mensagem "A recuperação foi concluída" é registrada na inicialização.  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Executar um procedimento armazenado](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)  
  
  
