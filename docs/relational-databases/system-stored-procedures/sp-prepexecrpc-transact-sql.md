---
title: sp_prepexecrpc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexecrpc
- sp_cursor_prepexecrpc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexecrpc
ms.assetid: 35d686f2-ef31-4eaa-baa9-9cef5d6c87c2
caps.latest.revision: 5
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 50b9cc2ec1ce4cfa3a953e73568bc0bff0546089
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spprepexecrpc-transact-sql"></a>sp_prepexecrpc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Prepara e executa uma chamada de procedimento armazenado parametrizada que foi especificada com um identificador de RPC. sp_prepexecrpc é invocado por ID = 14 em um pacote de protocolo TDS de dados tabulares.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
  
  
