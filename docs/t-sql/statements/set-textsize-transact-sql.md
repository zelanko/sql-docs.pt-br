---
title: SET TEXTSIZE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/12/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TEXTSIZE_TSQL
- TEXTSIZE
- SET_TEXTSIZE_TSQL
- SET TEXTSIZE
dev_langs:
- TSQL
helpviewer_keywords:
- SET TEXTSIZE statement
- SELECT statement [SQL Server], text size returned
- size [SQL Server], text and image data
- TEXTSIZE option
- text size returned [SQL Server]
ms.assetid: 787154a6-39a6-4dd6-a6d0-67b4364f95d5
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2d9925b382a7d09722846ca7da583fb92fe4609c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="set-textsize-transact-sql"></a>SET TEXTSIZE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica o tamanho do **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **texto**, **ntext** , e **imagem** dados retornados por uma instrução SELECT.  
  
> [!IMPORTANT]  
>  **ntext**, **texto**, e **imagem** tipos de dados serão removidos em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esses tipos de dados em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que os utilizam atualmente. Em vez disso, use **nvarchar(max)**, **varchar(max)**e **varbinary(max)** .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SET TEXTSIZE { number }   
```  
  
## <a name="arguments"></a>Argumentos  
 *number*  
 É o período de **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **texto**, **ntext**, ou **imagem** dados, em bytes. *número* é um inteiro com um valor máximo de 2147483647 (2 GB).  Um valor de -1 indica o tamanho ilimitado. Um valor de 0 redefine o tamanho para o valor padrão de 4 KB.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (10.0 e superior) e o Driver ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificar automaticamente `-1` (ilimitado) ao se conectar.  
  
 **Drivers anteriores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008:** o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider (versão 9) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automaticamente definem TEXTSIZE como 2147483647 durante a conexão.  
  
## <a name="remarks"></a>Comentários  
 Configuração SET TEXTSIZE afeta o @@TEXTSIZE função.  
  
 A configuração de TEXTSIZE é definida na execução ou em tempo de execução, e não no momento de análise.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="see-also"></a>Consulte também  
 [@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

