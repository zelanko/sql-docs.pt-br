---
title: '@@SERVERNAME (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 112e9ef765b65d9563bfda7e0ec59bac24d02053
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85714981"
---
# <a name="x40x40servername-transact-sql"></a>&#x40;&#x40;SERVERNAME (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna o nome do servidor local que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 ![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
@@SERVERNAME  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar**  
  
## <a name="remarks"></a>Comentários  
 A instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define o nome do servidor como o nome do computador durante instalação. Para alterar o nome do servidor, use **sp_addserver** e reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Com várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas, @@SERVERNAME retornará as seguintes informações do nome do servidor local se ele não tiver sido alterado depois da instalação.  
  
|Instância|Informações do servidor|  
|--------------|------------------------|  
|Instância padrão|'*servername*'|  
|Instância nomeada|'*servername*\\*instancename*'|  
|instância de cluster de failover – instância padrão|'*network_name_for_fci_in_wsfc*'|  
|instância de cluster de failover – instância nomeada|'*network_name_for_fci_in_wsfc*\\*instancename*'|  
  
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
  
  
