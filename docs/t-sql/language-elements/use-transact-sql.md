---
title: USE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2016
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- USE_TSQL
- USE
dev_langs:
- TSQL
helpviewer_keywords:
- USE statement
- database context [SQL Server]
- context changes [SQL Server]
- modifying database context
ms.assetid: c05acac8-c063-4770-8e36-d7f71d500b10
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 97f81016057c9c92f782b81243117d3f0dbe519f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47741974"
---
# <a name="use-transact-sql"></a>USE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Altera o contexto de banco de dados para o banco de dados ou instantâneo de banco de dados especificado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
USE { database_name }   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 É o nome do banco de dados ou instantâneo de banco de dados para os quais o contexto de usuário é alternado. Os nomes do banco de dados e do instantâneo do banco de dados devem seguir as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 Em [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], o parâmetro de banco de dados só pode se referir ao banco de dados atual. Se um banco de dados que não seja o banco de dados atual é fornecido, a instrução `USE` não alterna entre bancos de dados e o código de erro 40508 é retornado. Para alterar os bancos de dados, você deve conectar-se diretamente ao banco de dados. A instrução USE é marcada como não aplicável ao Banco de Dados SQL na parte superior desta página, porque, embora você possa ter a instrução `USE` em um lote, ela não executa nenhuma ação.
  
## <a name="remarks"></a>Remarks  
 Quando um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ele é automaticamente conectado ao seu banco de dados padrão e adquire o contexto de segurança de um usuário de banco de dados. Se nenhum usuário de banco de dados foi criado para o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o logon se conectará como convidado. Se o usuário de banco de dados não tiver permissão CONNECT no banco de dados, a instrução USE falhará. Se nenhum banco de dados padrão foi atribuído ao logon, seu banco de dados padrão será definido como mestre.  
  
 USE é executado em tempo de compilação e de execução e entra em vigor imediatamente. Portanto, as instruções exibidas em um lote depois da instrução USE são executadas no banco de dados especificado.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão de CONNECT no banco de dados de destino.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera o contexto de banco de dados para o banco de dados `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
  
  


