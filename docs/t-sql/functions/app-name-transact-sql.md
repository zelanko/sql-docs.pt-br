---
description: APP_NAME (Transact-SQL)
title: APP_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- APP_NAME_TSQL
- APP_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- name checking for current session [SQL Server]
- sessions [SQL Server], application names
- applications [SQL Server], names
- current session application names
- APP_NAME function
ms.assetid: e491e192-9b30-4243-bc19-33c133fe08a8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e8b24e74faa029f72bedf464ddbd06d79a8750ef
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126265"
---
# <a name="app_name-transact-sql"></a>APP_NAME (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Esta função retornará o nome do aplicativo para a sessão atual, se o aplicativo definir esse valor de nome.
  
> [!IMPORTANT]  
>  O cliente fornece o nome do aplicativo, e `APP_NAME`não é verifica o valor do nome do aplicativo de nenhuma forma. Não use `APP_NAME` como parte de uma verificação de segurança.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
APP_NAME  ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
**nvarchar(128)**
  
## <a name="remarks"></a>Comentários  
Use a `APP_NAME` para distinguir entre diferentes aplicativos, como uma maneira de executar ações diferentes para esses aplicativos. Por exemplo, `APP_NAME` pode distinguir entre diferentes aplicativos, que permite um formato de data diferente para cada aplicativo. Ela também pode permitir o retorno de uma mensagem informativa para determinados aplicativos.
  
Para definir um nome de aplicativo no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], clique em **Opções** na caixa de diálogo **Conectar ao Mecanismo de Banco de Dados**. Na guia **Parâmetros de Conexão Adicionais**, forneça um atributo **app** no formato `;app='application_name'`
  
## <a name="example"></a>Exemplo  
Este exemplo verifica se o aplicativo cliente que iniciou este processo é uma sessão do `SQL Server Management Studio`. Em seguida, ele fornece um valor de data no formato US ou ANSI.
  
```sql
USE AdventureWorks2012;  
GO  
IF APP_NAME() = 'Microsoft SQL Server Management Studio - Query'  
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( VARCHAR(100) , GETDATE(), 101) + '.';  
ELSE   
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( VARCHAR(100) , GETDATE(), 102) + '.';  
GO  
```  
  
## <a name="see-also"></a>Confira também
[Funções do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
[Funções](../../t-sql/functions/functions.md)
  
  
