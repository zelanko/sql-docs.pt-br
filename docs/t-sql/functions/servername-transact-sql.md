---
title: '@@SERVERNAME (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@SERVERNAME'
- '@@SERVERNAME_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@SERVERNAME function'
- local servers [SQL Server]
ms.assetid: b0ef33fb-954a-4294-b05b-a87c14ce25a3
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5f1e7dbd47562368653ce75eee9d2a412164a9c9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40servername-transact-sql"></a>& #x 40; & #x 40. SERVERNAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o nome do servidor local que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
@@SERVERNAME  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar**  
  
## <a name="remarks"></a>Comentários  
 A instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define o nome do servidor como o nome do computador durante instalação. Para alterar o nome do servidor, use **sp_addserver**e, em seguida, reinicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Com várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas, @@SERVERNAME retorna as informações de nome o seguinte servidor local se o nome do servidor local não foi alterado desde a instalação.  
  
|Instância|Informações do servidor|  
|--------------|------------------------|  
|Instância padrão|'*servername*'|  
|Instância nomeada|'*servername*\\*instancename*'|  
|instância clusterizada de failover - instância padrão|'*virtualservername*'|  
|instância clusterizada de failover - instância nomeada|'*virtualservername*\\*instancename*'|  
  
 Embora o @@SERVERNAME função e a propriedade SERVERNAME da função SERVERPROPERTY podem retornar cadeias de caracteres com formatos semelhantes, as informações podem ser diferentes. Uma propriedade SERVERNAME relata automaticamente alterações no nome de rede do computador.  
  
 Por outro lado, @@SERVERNAME não relata tais alterações. @@SERVERNAME relata as alterações feitas para o nome do servidor local usando o **sp_addserver** ou **sp_dropserver** procedimento armazenado.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra o uso de `@@SERVERNAME`.  
  
```  
SELECT @@SERVERNAME AS 'Server Name'  
```  
  
 Este é um exemplo de conjunto de resultados.  
  
```  
Server Name  
---------------------------------  
ACCTG  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de configuração &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sp_addserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)  
  
  
