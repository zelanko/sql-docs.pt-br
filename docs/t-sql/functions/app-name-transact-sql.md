---
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 21b49eb9638b4651ff52c6515f6e5f62177fc504
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73843437"
---
# <a name="app_name-transact-sql"></a>APP_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Esta função retornará o nome do aplicativo para a sessão atual, se o aplicativo definir esse valor de nome.
  
> [!IMPORTANT]  
>  O cliente fornece o nome do aplicativo, e `APP_NAME`não é verifica o valor do nome do aplicativo de nenhuma forma. Não use `APP_NAME` como parte de uma verificação de segurança.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
  
APP_NAME  ( )  
```  
  
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
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 101) + '.';  
ELSE   
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 102) + '.';  
GO  
```  
  
## <a name="see-also"></a>Confira também
[Funções do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
[Funções](../../t-sql/functions/functions.md)
  
  
