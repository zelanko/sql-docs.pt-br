---
title: DEFINIR Comando NULO | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set nullSET NULL
ms.assetid: 410c5a6e-e957-4ecc-9e2d-e591cbc0bc4f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c83c9ef9f8a0ce143308b73d8df09b05fb2cdea
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300806"
---
# <a name="set-null-command"></a>Comando SET NULL
Determina como os valores nulos são suportados pelos comandos ALTER TABLE - SQL, CREATE TABLE - SQL e INSERT - SQL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ATIVADO  
 (Padrão para o driver; o padrão para Visual FoxPro é OFF.) Especifica que todas as colunas em uma tabela criada com TABELA ALTER e TABELA CRIAR permitirão valores nulos. Você pode substituir o suporte de valor nulo para colunas na tabela, incluindo a cláusula NÃO NULA nas definições das colunas.  
  
 Também especifica que INSERT - SQL inserirá valores nulos em quaisquer colunas não incluídas na cláusula INSERT - SQL VALUE. INSERIR - O SQL inserirá valores nulos apenas em colunas que permitem valores nulos.  
  
 OFF  
 Especifica que todas as colunas em uma tabela criada com TABELA ALTER e TABELA CRIAR não permitirão valores nulos. Você pode designar suporte de valor nulo para colunas em ALTER TABLE e CREATE TABLE, incluindo a cláusula NULL nas definições das colunas.  
  
 Também especifica que INSERT - SQL inserirá valores em branco em quaisquer colunas não incluídas na cláusula INSERT - SQL VALUE.  
  
## <a name="remarks"></a>Comentários  
 SET NULL afeta apenas a forma como os valores nulos são suportados por ALTER TABLE, CREATE TABLE e INSERT - SQL. Outros comandos não são afetados pelo SET NULL.  
  
## <a name="see-also"></a>Consulte Também  
 [TABELA ALTER - Comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [CRIAR TABELA - Comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT – comando SQL](../../odbc/microsoft/insert-sql-command.md)
