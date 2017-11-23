---
title: sp_remoteoption (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_remoteoption_TSQL
- sp_remoteoption
dev_langs: TSQL
helpviewer_keywords: sp_remoteoption
ms.assetid: c9a7309b-eab7-4192-a414-e282581af4e5
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5bea191258773154019cf91063155be54d7cc373
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spremoteoption-transact-sql"></a>sp_remoteoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe ou altera opções para um logon remoto definido no servidor local que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]sp_remoteoption não altera nenhuma opção e retorna uma mensagem de erro. Tem suporte somente para compatibilidade com versões anteriores.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_remoteoption [ [ @remoteserver = ] 'remoteserver' ]   
     [ , [ @loginame = ] 'loginame' ]   
     [ , [ @remotename = ] 'remotename' ]   
     [ , [ @optname = ] 'optname' ]   
     [ , [ @optvalue = ] 'optvalue' ]  
```  
  
## <a name="remarks"></a>Comentários  
 Este procedimento armazenado retorna a seguinte mensagem de erro:  
  
 `The trusted option in remote login mapping is no longer supported.`  
  
## <a name="see-also"></a>Consulte também  
 [Servidores vinculados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)  
  
  
