---
title: sp_setnetname (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_setnetname
- sp_setnetname_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_setnetname
ms.assetid: f416ba81-3835-4588-b0a3-2fe75589490e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 87401c8f90f0351f797aa3572c7717bb02360e00
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881522"
---
# <a name="sp_setnetname-transact-sql"></a>sp_setnetname (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Define os nomes de rede em **Sys. Servers** para seus nomes de computador de rede reais para instâncias remotas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Este procedimento pode ser usado para habilitar a execução de chamadas de procedimento armazenado remoto para computadores com nomes de rede contendo identificadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não são válidos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_setnetname  
@server = 'server',   
     @netname = 'network_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 ** @server = '** *servidor* **'**  
 É o nome do servidor remoto conforme referenciado em sintaxe de chamada de procedimento armazenado remoto codificado pelo usuário. Exatamente uma linha em **Sys. Servers** já deve existir para usar esse *servidor*. *server* é **sysname**, sem padrão.  
  
 ** @netname = '** *network_name* **'**  
 É o nome de rede do computador ao qual as chamadas de procedimento armazenado remoto são feitas. *network_name* é **sysname**, sem padrão.  
  
 Esse nome deve corresponder ao nome do computador de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, e o nome pode incluir caracteres que não são permitidos em identificadores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Algumas chamadas de procedimento armazenado remoto a computadores com Windows podem encontrar problemas se o nome do computador tiver identificadores que não são válidos.  
  
 Como servidores vinculados e servidores remotos residem no mesmo namespace, eles não podem ter o mesmo nome. No entanto, você pode definir um servidor vinculado e um servidor remoto em um servidor especificado atribuindo nomes diferentes e usando **sp_setnetname** para definir o nome de rede de um deles como o nome de rede do servidor subjacente.  
  
```  
--Assume sqlserv2 is actual name of SQL Server   
--database server  
EXEC sp_addlinkedserver 'sqlserv2';  
GO  
EXEC sp_addserver 'rpcserv2';  
GO  
EXEC sp_setnetname 'rpcserv2', 'sqlserv2';  
```  
  
> [!NOTE]  
>  Não há suporte para o uso de **sp_setnetname** para apontar um servidor vinculado de volta para o servidor local. Os servidores referenciados dessa maneira não podem participar de uma transação distribuída.  
  
## <a name="permissions"></a>Permissões  
 Requer associação nas funções de servidor fixas **sysadmin** e **setupadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra uma sequência administrativa típica usada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para emitir a chamada de procedimento armazenado remoto.  
  
```  
USE master;  
GO  
EXEC sp_addserver 'Win_1';  
EXEC sp_setnetname 'Win_1','Win-1';  
EXEC Win_1.master.dbo.sp_who;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addserver](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
