---
title: '@@SERVERNAME (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a0adbdba1c04ad4cc2e39f532ded83d3964a47ea
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37787357"
---
# <a name="x40x40servername-transact-sql"></a>&#x40;&#x40;SERVERNAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o nome do servidor local que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![Ícone do link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone do link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
@@SERVERNAME  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar**  
  
## <a name="remarks"></a>Remarks  
 A instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define o nome do servidor como o nome do computador durante instalação. Para alterar o nome do servidor, use **sp_addserver** e reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Com várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas, @@SERVERNAME retornará as seguintes informações do nome do servidor local se ele não tiver sido alterado depois da instalação.  
  
|Instância|Informações do servidor|  
|--------------|------------------------|  
|Instância padrão|'*servername*'|  
|Instância nomeada|'*servername*\\*instancename*'|  
|instância clusterizada de failover – instância padrão|'*virtualservername*'|  
|instância clusterizada de failover – instância nomeada|'*virtualservername*\\*instancename*'|  
  
 Embora a função @@SERVERNAME e a propriedade SERVERNAME da função SERVERPROPERTY possam retornar cadeias de caracteres com formatos semelhantes, as informações podem ser diferentes. Uma propriedade SERVERNAME relata automaticamente alterações no nome de rede do computador.  
  
 Por outro lado, @@SERVERNAME não relata essas alterações. @@SERVERNAME relata alterações feitas no nome do servidor local usando o procedimento armazenado **sp_addserver** ou **sp_dropserver**.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Funções de configuração &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)  
  
  
