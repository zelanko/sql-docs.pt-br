---
description: Instruções de utilitários do SQL Server – GO
title: Instruções de utilitários do SQL Server – GO | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GO
- GO_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- batches [SQL Server], ending
- ending batches [SQL Server]
- GO command
ms.assetid: b2ca6791-3a07-4209-ba8e-2248a92dd738
author: rothja
ms.author: jroth
ms.openlocfilehash: 973c8eb74a26047dfa8472497e403385e3678326
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445397"
---
# <a name="sql-server-utilities-statements---go"></a>Instruções de utilitários do SQL Server – GO
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece comandos que não são instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], mas que são reconhecidos pelos utilitários **sqlcmd** e **osql** e pelo Editor de Códigos [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Estes comandos podem ser usados para facilitar a legibilidade e a execução de lotes e scripts.  
  
  O GO sinaliza o término de um lote de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] para os utilitários do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
GO [count]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *contagem*  
 É um número inteiro positivo. O lote que precede GO será executado pelo número de vezes especificado.  
  
## <a name="remarks"></a>Comentários  
 O GO não é uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)], ele é um comando reconhecido pelos utilitários **sqlcmd** e **osql** e pelo Editor de Códigos [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Os utilitários [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpretam GO como um sinal de que eles devem enviar o lote atual de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O lote atual de instruções é composto de todas as instruções digitadas desde o último GO, ou desde o início da sessão ad hoc ou script, se esse for o primeiro GO.  
  
 Uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] não pode ocupar a mesma linha que um comando GO. No entanto, a linha pode conter comentários.  
  
 Os usuários precisam seguir as regras de lotes. Por exemplo, qualquer execução de um procedimento armazenado depois da primeira instrução em um lote deve incluir a palavra-chave EXECUTE. O escopo de variáveis locais (definidas pelo usuário) é limitado a um lote e não pode ser referenciado após um comando GO.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyMsg VARCHAR(50)  
SELECT @MyMsg = 'Hello, World.'  
GO -- @MyMsg is not valid after this GO ends the batch.  
  
-- Yields an error because @MyMsg not declared in this batch.  
PRINT @MyMsg  
GO  
  
SELECT @@VERSION;  
-- Yields an error: Must be EXEC sp_who if not first statement in   
-- batch.  
sp_who  
GO  
```  
  
 Os aplicativos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem enviar várias instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para execução como lote. As instruções em lote são compiladas em um único plano de execução. Os programadores que executam instruções ad hoc em utilitários do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ou que compilam scripts de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] a serem executados por meio dos utilitários do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usam GO para sinalizar o término de um lote.  
  
 Os aplicativos baseados em APIs ODBC ou OLE DB recebem um erro de sintaxe quando tentam executar um comando GO. Os utilitários do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nunca enviam um comando GO ao servidor.  
  
 Não use um ponto e vírgula como terminador de instrução depois de GO.
 
```
-- Yields an error because ; is not permitted after GO  
SELECT @@VERSION;  
GO;  
```
  
## <a name="permissions"></a>Permissões  
 GO é um comando de utilitário que não exige nenhuma permissão. Pode ser executado por qualquer usuário.    
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria dois lotes. O primeiro lote contém apenas uma instrução `USE AdventureWorks2012` para definir o contexto do banco de dados. As instruções restantes usam uma variável local. Portanto, todas as declarações de variável local devem ser agrupadas em um único lote. Isso é feito sem que haja um comando `GO` até depois da última instrução que faz referência à variável.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @NmbrPeople int  
SELECT @NmbrPeople = COUNT(*)  
FROM Person.Person;  
PRINT 'The number of people as of ' +  
      CAST(GETDATE() AS char(20)) + ' is ' +  
      CAST(@NmbrPeople AS char (10));  
GO  
```  
  
 O exemplo a seguir executa as instruções no lote duas vezes.  
  
```  
SELECT DB_NAME();  
SELECT USER_NAME();  
GO 2  
```  
  
  
