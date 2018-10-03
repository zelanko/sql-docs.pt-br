---
title: xp_logevent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_logevent
- xp_logevent_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_logevent
ms.assetid: 7b379ad0-5b12-4d2e-9c52-62465df1fdbd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3c8604413718e8b318b67cf63562531e869a79ba
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47660074"
---
# <a name="xplogevent-transact-sql"></a>xp_logevent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra uma mensagem definida pelo usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] arquivo de log e no Visualizador de eventos do Windows. xp_logevent pode ser usado para enviar um alerta sem enviar uma mensagem ao cliente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xp_logevent { error_number , 'message' } [ , 'severity' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *error_number*  
 É um número de erro definido pelo usuário maior que 50.000. O valor máximo é 2147483647 (2^31 - 1).  
  
 **'** *mensagem* **'**  
 É uma cadeia de caracteres com no máximo 2048 caracteres.  
  
 **'** *severidade* **'**  
 É uma destas três cadeias de caracteres: INFORMATIONAL, WARNING ou ERROR. *severidade* é opcional, com um padrão INFORMATIONAL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 xp_logevent retorna a seguinte mensagem de erro para o exemplo de código incluído:  
  
 `The command(s) completed successfully.`  
  
## <a name="remarks"></a>Comentários  
 Quando você envia mensagens de [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos, disparadores, lotes e assim por diante, usem a instrução RAISERROR, em vez de xp_logevent. xp_logevent não chama um manipulador de mensagens de um cliente ou definir@ERROR. Para gravar mensagens em Visualizador de Eventos do Windows e no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], execute a instrução RAISERROR.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa db_owner no banco de dados master ou associação na função de servidor fixa sysadmin.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir registra a mensagem, com variáveis passadas à mensagem em Visualizador de Eventos do Windows.  
  
```  
DECLARE @@TABNAME varchar(30), @@USERNAME varchar(30), @@MESSAGE varchar(255);  
SET @@TABNAME = 'customers';  
SET @@USERNAME = USER_NAME();  
SELECT @@MESSAGE = 'The table ' + @@TABNAME + ' is not owned by the user   
   ' + @@USERNAME + '.';  
  
USE master;  
EXEC xp_logevent 60000, @@MESSAGE, informational;  
```  
  
## <a name="see-also"></a>Consulte também  
 [PRINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados estendidos gerais &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
