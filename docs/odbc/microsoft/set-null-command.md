---
title: Comando SET NULL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b6f0e23abd31661210282967fa35080376eaaaf3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63159306"
---
# <a name="set-null-command"></a>Comando SET NULL
Determina como os valores nulos são suportados pela ALTER TABLE - SQL, CREATE TABLE - SQL e inserir - comandos SQL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 (Padrão para o driver; o padrão para o Visual FoxPro é OFF). Especifica que todas as colunas em uma tabela criada com ALTER TABLE e CREATE TABLE permitirá valores nulos. Você pode substituir o suporte de valor nulo para colunas na tabela, incluindo a cláusula NOT NULL nas definições das colunas.  
  
 Também especifica que INSERT - SQL será inserir valores nulos em colunas não incluídas na instrução INSERT - cláusula VALUE de SQL. INSERIR - SQL irá inserir valores nulos apenas em colunas que permitem valores nulos.  
  
 OFF  
 Especifica que todas as colunas em uma tabela criada com ALTER TABLE e CREATE TABLE não permitirá valores nulos. Você pode designar o suporte de valor nulo para colunas em ALTER TABLE e CREATE TABLE, incluindo a cláusula NULL nas definições das colunas.  
  
 Também especifica que inserir - SQL será inserir valores em branco em qualquer colunas não incluídas na instrução INSERT - cláusula VALUE de SQL.  
  
## <a name="remarks"></a>Comentários  
 Definir nulo afeta somente como valores nulos são compatíveis com ALTER TABLE, CREATE TABLE e INSERT - SQL. Outros comandos não são afetados por SET NULL.  
  
## <a name="see-also"></a>Consulte também  
 [ALTER TABLE – comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [CREATE TABLE – comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT – comando SQL](../../odbc/microsoft/insert-sql-command.md)
