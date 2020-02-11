---
title: Definir comando nulo | Microsoft Docs
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
ms.openlocfilehash: 9f8addb9b4c7c200ee8f213bdd959067039ccfff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063668"
---
# <a name="set-null-command"></a>Comando SET NULL
Determina como os valores nulos são suportados pelos comandos ALTER TABLE-SQL, CREATE TABLE-SQL e INSERT-SQL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ATIVADO  
 (O padrão para o driver; o padrão para o Visual FoxPro é desativado.) Especifica que todas as colunas em uma tabela criada com ALTER TABLE e CREATE TABLE permitirão valores nulos. Você pode substituir o suporte a valor nulo para colunas na tabela, incluindo a cláusula NOT NULL nas definições das colunas.  
  
 Também especifica que INSERT-SQL irá inserir valores nulos em todas as colunas não incluídas na cláusula INSERT-SQL VALUE. INSERT-SQL irá inserir valores nulos somente em colunas que permitem valores nulos.  
  
 OFF  
 Especifica que todas as colunas em uma tabela criada com ALTER TABLE e CREATE TABLE não permitirão valores nulos. Você pode designar o suporte a valor nulo para colunas em ALTER TABLE e CREATE TABLE incluindo a cláusula NULL nas definições das colunas.  
  
 Também especifica que INSERT-SQL irá inserir valores em branco em todas as colunas não incluídas na cláusula INSERT-SQL VALUE.  
  
## <a name="remarks"></a>Comentários  
 SET NULL afeta apenas a forma como os valores nulos são suportados por ALTER TABLE, CREATE TABLE e INSERT-SQL. Outros comandos não são afetados por SET NULL.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE-comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Comando CREATE TABLE-SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT – comando SQL](../../odbc/microsoft/insert-sql-command.md)
