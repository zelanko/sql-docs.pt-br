---
title: Comando SET NULL | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- set nullSET NULL
ms.assetid: 410c5a6e-e957-4ecc-9e2d-e591cbc0bc4f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 14cade223de7014dd4a0c27295d3ff742d18af17
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="set-null-command"></a>Comando de conjunto nulo
Determina como os valores nulos são suportados pelo SQL ALTER TABLE - SQL, criar tabela - e inserir - comandos SQL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 (Padrão para o driver; o padrão para o Visual FoxPro é OFF). Especifica que todas as colunas em uma tabela criada com ALTER TABLE e CREATE TABLE permitirá valores nulos. Você pode substituir o suporte de valor nulo para colunas na tabela, inclusive a cláusula NOT NULL nas definições das colunas.  
  
 Também especifica que inserir - SQL será inserir valores nulos em todas as colunas não incluídas na instrução INSERT - cláusula VALUE do SQL. INSERIR - SQL inserir valores nulos apenas em colunas que permitem valores nulos.  
  
 OFF  
 Especifica que todas as colunas em uma tabela criada com ALTER TABLE e CREATE TABLE não permite valores nulos. Você pode designar o suporte de valor nulo para colunas em ALTER TABLE e CREATE TABLE, incluindo a cláusula NULL nas definições das colunas.  
  
 Também especifica que inserir - SQL será inserir valores em branco em todas as colunas não incluídas na instrução INSERT - cláusula VALUE de SQL.  
  
## <a name="remarks"></a>Comentários  
 SET NULL afeta somente como valores nulos são suportados pelo ALTER TABLE, CREATE TABLE e inserir - SQL. Outros comandos não são afetados por SET NULL.  
  
## <a name="see-also"></a>Consulte também  
 [ALTER TABLE - comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Criar tabela - comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT – comando SQL](../../odbc/microsoft/insert-sql-command.md)

