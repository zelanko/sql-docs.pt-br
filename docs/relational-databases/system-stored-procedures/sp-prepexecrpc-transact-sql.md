---
description: sp_prepexecrpc (Transact-SQL)
title: sp_prepexecrpc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexecrpc
- sp_cursor_prepexecrpc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexecrpc
ms.assetid: 35d686f2-ef31-4eaa-baa9-9cef5d6c87c2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9db0c4450f6726d39934afac27c3306dae9ded3f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534991"
---
# <a name="sp_prepexecrpc-transact-sql"></a>sp_prepexecrpc (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Prepara e executa uma chamada de procedimento armazenado parametrizada que foi especificada com um identificador de RPC. sp_prepexecrpc é invocado por ID = 14 em um pacote TDS (tabela de dados tabulares).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_prepexecrpc handle OUTPUT, RPCCall  
    [ , bound_param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *processamento*  
 É o identificador preparado gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. o *identificador* é um parâmetro necessário com um valor de retorno **int** .  
  
 *RPCCall*  
 Define a chamada de procedimento armazenado que usa a sintaxe canônica ODBC. *RPCCall* é um parâmetro necessário que chama um valor de entrada de cadeia de caracteres **ntext** .  
  
 *bound_param*  
 Significa o uso opcional de parâmetros adicionais. *bound_param* chama um valor de entrada de qualquer tipo de dados para designar os parâmetros adicionais em uso.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
