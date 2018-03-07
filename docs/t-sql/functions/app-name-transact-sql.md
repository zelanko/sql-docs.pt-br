---
title: App_name (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b2b65f2380cc52c7a1d084dedad5fdb744d377bf
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="appname-transact-sql"></a>APP_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o nome do aplicativo para a sessão atual se definido pelo aplicativo.
  
> [!IMPORTANT]  
>  O nome do aplicativo é fornecido pelo cliente e não é verificado de nenhuma forma. Não use **APP_NAME** como parte de uma verificação de segurança.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
  
APP_NAME  ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
**nvarchar (128)**
  
## <a name="remarks"></a>Comentários  
Use **APP_NAME** quando você deseja executar ações diferentes para diferentes aplicativos. Por exemplo, formatar uma data de maneira diferente para diferentes aplicativos ou retornar uma mensagem informativa para determinados aplicativos.
  
Para definir um nome de aplicativo [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], no **conectar ao mecanismo de banco de dados** caixa de diálogo, clique em **opções**. Sobre o **parâmetros adicionais de Conexão** guia, forneça um **aplicativo** atributo no formato`;app='application_name'`
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir verifica se o aplicativo cliente que iniciou esse processo é uma sessão do `SQL Server Management Studio` e fornece uma data no formato US ou ANSI.
  
```sql
USE AdventureWorks2012;  
GO  
IF APP_NAME() = 'Microsoft SQL Server Management Studio - Query'  
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 101) + '.';  
ELSE   
PRINT 'This process was started by ' + APP_NAME() + '. The date is ' + CONVERT ( varchar(100) , GETDATE(), 102) + '.';  
GO  
```  
  
## <a name="see-also"></a>Consulte também
[Funções do sistema &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
[Funções](../../t-sql/functions/functions.md)
  
  
