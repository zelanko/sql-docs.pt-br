---
title: SET REMOTE_PROC_TRANSACTIONS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- REMOTE_PROC_TRANSACTIONS_TSQL
- SET REMOTE_PROC_TRANSACTIONS
- REMOTE_PROC_TRANSACTIONS
- SET_REMOTE_PROC_TRANSACTIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote stored procedures [SQL Server]
- SET REMOTE_PROC_TRANSACTIONS statement
- distributed transactions [SQL Server], starting
- REMOTE_PROC_TRANSACTIONS option
- active transactions
ms.assetid: 4d284ae9-3f5f-465a-b0dd-1328a4832a03
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ddb45f9c1767e65e39870ecf32d12e3ac1f80658
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62939716"
---
# <a name="set-remoteproctransactions-transact-sql"></a>SET REMOTE_PROC_TRANSACTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Especifica que quando uma transação local está ativa, a execução de um procedimento armazenado remoto inicia uma transação distribuída [!INCLUDE[tsql](../../includes/tsql-md.md)], gerenciada pelo MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)]).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Essa opção é fornecida para compatibilidade com versões anteriores para aplicativos que usam procedimentos armazenados remotos. Em vez de emitir chamadas de procedimento armazenado remotas, use consultas distribuídas, que fazem referência a servidores vinculados. Elas são definidas usando [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET REMOTE_PROC_TRANSACTIONS { ON | OFF }   
```  
  
## <a name="arguments"></a>Argumentos  
 ON | OFF  
 Quando ON, uma transação [!INCLUDE[tsql](../../includes/tsql-md.md)] distribuída é iniciada quando um procedimento armazenado remoto é executado de uma transação local. Quando OFF, chamar um procedimento armazenado remoto de uma transação local, não origina uma transação distribuída [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="remarks"></a>Remarks  
 Quando REMOTE_PROC_TRANSACTIONS está ON, chamar um procedimento remoto armazenado irá iniciar uma transação distribuída e inscreverá a transação com o MS DTC. A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que chama o procedimento armazenado remoto é o que origina a transação e controla a conclusão da transação. Quando as instruções subsequentes COMMIT TRANSACTION ou ROLLBACK TRANSACTION são emitidas para a conexão, a instância controladora solicita que o MS DTC gerencie a conclusão da transação distribuída em todas os computadores envolvidos.  
  
 Depois que uma transação distribuída [!INCLUDE[tsql](../../includes/tsql-md.md)] foi iniciada, é possível fazer chamadas de procedimento armazenado remoto a outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que foram definidas como servidores remotos. Os servidores remotos são todos inscritos na transação distribuída do [!INCLUDE[tsql](../../includes/tsql-md.md)], e o MS DTC assegura que a transação seja completada em cada servidor remoto.  
  
 REMOTE_PROC_TRANSACTIONS é uma configuração no nível de conexão que pode ser usada para substituir a opção em nível de instância **sp_configure remote proc trans**.  
  
 Quando REMOTE_PROC_TRANSACTIONS estiver OFF, chamadas de procedimento armazenado remotas não farão parte de uma transação local. As modificações feitas pelo procedimento armazenado remoto estão confirmadas ou revertidas na ocasião em que o procedimento armazenado se completa. Instruções COMMIT TRANSACTION ou ROLLBACK TRANSACTION subsequentes, emitidas pela conexão que chamou o procedimento armazenado remoto não têm nenhum efeito no processamento feito pelo procedimento.  
  
 A opção REMOTE_PROC_TRANSACTIONS é uma opção de compatibilidade que afeta apenas chamadas remotas de procedimento armazenado feitas para instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definidas como servidor remoto usando **sp_addserver**. A opção não se aplica a consultas distribuídas que executem um procedimento armazenado em uma instância definida como servidor vinculado usando **sp_addlinkedserver**.  
  
 A configuração de SET REMOTE_PROC_TRANSACTIONS é definida na execução ou no tempo de execução, e não no momento da análise.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="see-also"></a>Consulte Também  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
