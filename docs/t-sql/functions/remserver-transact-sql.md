---
title: '@@REMSERVER (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: fa8c4f46b623d0893354fe07618a8d190950422b
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823751"
---
# <a name="x40x40remserver-transact-sql"></a>&#x40;&#x40;REMSERVER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Use procedimentos armazenados de servidor vinculado e servidores vinculados.  
  
 Retorna o nome do servidor de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] remoto como ele aparece no registro de logon.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
@@REMSERVER  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar(128)**  
  
## <a name="remarks"></a>Comentários  
 @@REMSERVER permite que um procedimento armazenado verifique o nome do servidor de banco de dados do qual o procedimento é executado.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Funções de configuração &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Servidores remotos](../../database-engine/configure-windows/remote-servers.md)  
  
  
