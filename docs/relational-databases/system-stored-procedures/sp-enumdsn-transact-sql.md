---
title: sp_enumdsn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumdsn
- sp_enumdsn_TSQL
helpviewer_keywords:
- sp_enumdsn
ms.assetid: 171cbc7d-7406-4cb0-8602-9405243bfd1d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 151b0f504080523e99fad839c17e02b786b619c0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831092"
---
# <a name="sp_enumdsn-transact-sql"></a>sp_enumdsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma lista de todos os nomes de fonte de dados ODBC e OLE DB definidos para um servidor em execução em uma conta especifica de usuário [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_enumdsn  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**Nome da fonte de dados**|**sysname**|Nome da fonte de dados.|  
|**Descrição**|**varchar(255)**|Descrição da fonte de dados|  
|**Tipo**|**int**|Tipo da fonte de dados.<br /><br /> **1** = DSN ODBC<br /><br /> **3** = OLE DB fonte de dados|  
|**Nome do Provedor**|**varchar(255)**|Nome do provedor OLE DB. O valor é NULL para ODBC DSN.|  
  
## <a name="remarks"></a>Comentários  
 Cada [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço tem um contexto de usuário. Um contexto de usuário é um conjunto de entradas de Registro que inclui as definições das fontes de dados ODBC para o usuário. O contexto de usuário é fornecido pelo nome de usuário sob o qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está executando.  
  
 Por exemplo, se o servidor estiver em execução no contexto de usuário de conta do sistema, os DSNs (nomes das fontes de dados) retornados serão todos DSNs do sistema associados à conta do sistema. Se o servidor estiver em execução em uma conta de usuário particular, somente os DSNs definidos para aquela conta particular daquele usuário serão retornados.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_enumdsn**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_dsninfo](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
