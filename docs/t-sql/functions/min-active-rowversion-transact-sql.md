---
title: MIN_ACTIVE_ROWVERSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MIN_ACTIVE_ROWVERSION
- MIN_ACTIVE_ROWVERSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MIN_ACTIVE_ROWVERSION function [Transact-SQL]
ms.assetid: 87c89547-8ea1-4820-b75e-36be683e4e10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c4f21916de6c03c8e592702e58af481ef64cbb6d
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65944220"
---
# <a name="minactiverowversion-transact-sql"></a>MIN_ACTIVE_ROWVERSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o valor **rowversion** ativo mais baixo no banco de dados atual. Um valor **rowversion** ficará ativo se for usado em uma transação ainda não confirmada. Para obter mais informações, consulte [rowversion &#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md).  
  
> [!NOTE]  
>  O tipo de dados **rowversion** também é conhecido como **timestamp**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
MIN_ACTIVE_ROWVERSION  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna um valor **binary(8)** .  
  
## <a name="remarks"></a>Remarks  
 MIN_ACTIVE_ROWVERSION é uma função não determinística que retorna o valor de **rowversion** ativo mais baixo no banco de dados atual. Um novo valor **rowversion** normalmente é gerado quando uma inserção ou atualização é executada em uma tabela que contém uma coluna do tipo **rowversion**. Se não houver nenhum valor ativo no banco de dados, MIN_ACTIVE_ROWVERSION retornará o mesmo valor como @@DBTS + 1.  
  
 MIN_ACTIVE_ROWVERSION é útil para cenários como sincronização de dados que usam valores de **rowversion** para agrupar conjuntos de alterações. Se um aplicativo usar @@DBTS em vez de MIN_ACTIVE_ROWVERSION, as alterações que estiverem ativas quando a sincronização ocorrer poderão ser perdidas.  
  
 A função MIN_ACTIVE_ROWVERSION não é afetada pelas alterações nos níveis de isolamento da transação.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna valores de **rowversion** usando `MIN_ACTIVE_ROWVERSION` e `@@DBTS`. Observe que os valores diferem quando não há nenhuma transação ativa no banco de dados.  
  
```  
-- Create a table that has a ROWVERSION column in it.  
CREATE TABLE RowVersionTestTable (rv ROWVERSION)  
GO  
  
-- Print the current values for the database.  
PRINT ''  
PRINT 'DBTS'  
PRINT @@DBTS  
PRINT 'MIN_ACTIVE_ROWVERSION'  
PRINT MIN_ACTIVE_ROWVERSION()   
GO  
---------------- Results ----------------  
--DBTS  
--0x00000000000007E2  
--MIN_ACTIVE_ROWVERSION  
--0x00000000000007E3  
  
-- Insert a row.  
INSERT INTO RowVersionTestTable VALUES (DEFAULT)  
SELECT * FROM RowVersionTestTable  
GO  
---------------- Results ----------------  
--rv  
--0x00000000000007E3  
  
-- Print the current values for the database.  
PRINT ''  
PRINT 'DBTS'  
PRINT @@DBTS  
PRINT 'MIN_ACTIVE_ROWVERSION'  
PRINT MIN_ACTIVE_ROWVERSION()  
GO  
---------------- Results ----------------  
--DBTS  
--0x00000000000007E3  
--MIN_ACTIVE_ROWVERSION  
--0x00000000000007E4  
  
-- Insert a new row inside a transaction but do not commit.  
BEGIN TRAN  
INSERT INTO RowVersionTestTable VALUES (DEFAULT)  
SELECT * FROM RowVersionTestTable  
GO  
---------------- Results ----------------  
--rv  
--0x00000000000007E3  
--0x00000000000007E4  
  
-- Print the current values for the database.  
PRINT ''  
PRINT 'DBTS'  
PRINT @@DBTS  
PRINT 'MIN_ACTIVE_ROWVERSION'  
PRINT MIN_ACTIVE_ROWVERSION()   
GO  
---------------- Results ----------------  
--DBTS  
--0x00000000000007E4  
--MIN_ACTIVE_ROWVERSION  
--0x00000000000007E4  
  
-- Commit the transaction.  
COMMIT  
GO  
  
-- Print the current values for the database.  
PRINT ''  
PRINT 'DBTS'  
PRINT @@DBTS  
PRINT 'MIN_ACTIVE_ROWVERSION'  
PRINT MIN_ACTIVE_ROWVERSION()  
GO  
---------------- Results ----------------  
--DBTS  
--0x00000000000007E4  
--MIN_ACTIVE_ROWVERSION  
--0x00000000000007E5  
```  
  
## <a name="see-also"></a>Consulte Também  
 [@@DBTS &#40;Transact-SQL&#41;](../../t-sql/functions/dbts-transact-sql.md)   
 [rowversion &#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md)  
  
  
