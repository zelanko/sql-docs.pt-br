---
title: Comando SET NULL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- set nullSET NULL
ms.assetid: 410c5a6e-e957-4ecc-9e2d-e591cbc0bc4f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c856d439a2d811ed979c65ede925b9c2a6da2c9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
## <a name="remarks"></a>Remarks  
 SET NULL afeta somente como valores nulos são suportados pelo ALTER TABLE, CREATE TABLE e inserir - SQL. Outros comandos não são afetados por SET NULL.  
  
## <a name="see-also"></a>Consulte também  
 [ALTER TABLE - comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Criar tabela - comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT – comando SQL](../../odbc/microsoft/insert-sql-command.md)
