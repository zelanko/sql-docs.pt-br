---
title: sp_prepexecrpc (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexecrpc
- sp_cursor_prepexecrpc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexecrpc
ms.assetid: 35d686f2-ef31-4eaa-baa9-9cef5d6c87c2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6d17320174703e8fc6b21d7fecb83229f80bac41
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spprepexecrpc-transact-sql"></a>sp_prepexecrpc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Prepara e executa uma chamada de procedimento armazenado parametrizada que foi especificada com um identificador de RPC. sp_prepexecrpc é invocado por ID = 14 em um pacote de protocolo TDS de dados tabulares.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_prepexecrpc handle OUTPUT, RPCCall  
    [ , bound_param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Identificador*  
 É o identificador preparado gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *tratar* é um parâmetro obrigatório com um **int** valor de retorno.  
  
 *RPCCall*  
 Define a chamada de procedimento armazenado que usa a sintaxe canônica ODBC. *RPCCall* é um parâmetro obrigatório que chama uma **ntext** valor de cadeia de caracteres de entrada.  
  
 *bound_param*  
 Significa o uso opcional de parâmetros adicionais. *bound_param* chama um valor de entrada de qualquer tipo de dados para designar os parâmetros adicionais em uso.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
