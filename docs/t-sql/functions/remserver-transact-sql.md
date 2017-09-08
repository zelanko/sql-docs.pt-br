---
title: '@@REMSERVER (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@REMSERVER'
- '@@REMSERVER_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], remote servers
- remote servers [SQL Server], logins
- '@@REMSERVER function'
ms.assetid: 0bb451a9-3866-4064-963d-b74a2f864049
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 23ae1a37bcc84561a0ccedf10b1bb0c6ee7b6b73
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="remserver-transact-sql"></a>@@REMSERVER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Use procedimentos armazenados de servidor vinculado e servidores vinculados.  
  
 Retorna o nome do servidor de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] remoto como ele aparece no registro de logon.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
@@REMSERVER  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar (128)**  
  
## <a name="remarks"></a>Comentários  
 @@REMSERVER permite que um procedimento armazenado verificar o nome do servidor de banco de dados do qual o procedimento é executado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria o procedimento `usp_CheckServer` que retorna o nome do servidor remoto.  
  
```  
CREATE PROCEDURE usp_CheckServer  
AS  
SELECT @@REMSERVER;  
```  
  
 O procedimento armazenado a seguir é criado no servidor local `SEATTLE1`. O usuário efetua logon em um servidor remoto, `LONDON2`, e executa `usp_CheckServer`.  
  
```  
EXEC SEATTLE1...usp_CheckServer;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------  
LONDON2  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de configuração &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Servidores remotos](../../database-engine/configure-windows/remote-servers.md)  
  
  
