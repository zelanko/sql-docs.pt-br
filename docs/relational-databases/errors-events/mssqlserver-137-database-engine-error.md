---
title: MSSQLSERVER_137 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 137 (Database Engine error)
ms.assetid: 47fb4212-2165-4fec-bc41-6d548465d7be
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6d581cb6eeeb0965143b4830f90c0c537d4db7db
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver137"></a>MSSQLSERVER_137
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|137|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|P_SCALAR_VAR_NOTFOUND|  
|Texto da mensagem|É necessário declarar a variável escalar "%.*ls".|  
  
## <a name="explanation"></a>Explicação  
Esse erro ocorre quando uma variável é usada em um script SQL sem primeiro declarar a variável. O exemplo a seguir retorna o erro 137 para as instruções SET e SELECT porque **@mycol** não é declarada.  
  
SET @mycol = 'ContactName';  
  
SELECT @mycol;  
  
Uma das causas mais complexas desse erro inclui o uso de uma variável que é declarada fora da instrução EXECUTE. Por exemplo, a variável **@mycol** especificada na instrução SELECT é local na instrução SELECT, por isso está fora da instrução EXECUTE.  
  
USE AdventureWorks2012;  
  
GO  
  
DECLARE @mycol nvarchar(20);  
  
SET @mycol = 'Name';  
  
EXECUTE ('SELECT @mycol FROM Production.Product;');  
  
## <a name="user-action"></a>Ação do usuário  
Verifique se alguma das variáveis usadas em um script SQL foi declarada antes de ser usada em outro lugar no script.  
  
Reescreva o script de modo que ele não faça referência a variáveis na instrução EXECUTE que estejam declaradas fora dela. Por exemplo:  
  
USE AdventureWorks2012;  
  
GO  
  
DECLARE @mycol nvarchar(20) ;  
  
SET @mycol = 'Name';  
  
EXECUTE ('SELECT ' + @mycol + ' FROM Production.Product';) ;  
  
## <a name="see-also"></a>Consulte Também  
[EXECUTE &#40;Transact-SQL&#41;](~/t-sql/language-elements/execute-transact-sql.md)  
[Instruções SET &#40;Transact-SQL&#41;](~/t-sql/statements/set-statements-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](~/t-sql/language-elements/declare-local-variable-transact-sql.md)  
  
