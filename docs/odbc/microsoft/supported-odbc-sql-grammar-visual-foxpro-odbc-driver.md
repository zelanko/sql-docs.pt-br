---
title: Gramática SQL ODBC suportada (Driver Visual FoxPro ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- native Visual FoxPro language syntax [ODBC]
- FoxPro ODBC driver [ODBC], SQL grammar
- SQL grammar [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], SQL grammar
- grammar support in Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
- FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
ms.assetid: f41a38c2-e22e-4c65-a32e-9a6777435160
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f72548d0708a63f887f7d6da4d4f5988500f0eef
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304079"
---
# <a name="supported-odbc-sql-grammar-visual-foxpro-odbc-driver"></a>Gramática SQL do ODBC com suporte (Driver ODBC do Visual FoxPro)
O Driver Microsoft Visual FoxPro ODBC suporta o seguinte:  
  
-   Todas as declarações e cláusulas SQL na gramática SQL mínima ODBC  
  
-   Uma declaração SQL adicional da gramática SQL do núcleo ODBC  
  
 A tabela a seguir lista os itens suportados pelo driver, pelo nível de Gramática SQL ODBC.  
  
|Nível|Elementos|Item|  
|-----------|--------------|----------|  
|Mínimo|DDL (linguagem de definição de dados)|CREATE TABLE e DROP TABLE|  
||DML (linguagem de manipulação de dados)|SELECIONE, INSIRA, ATUALIZE E EXCLUA|  
||Expressões|Simples (como A>B+C)|  
||Tipos de dados|CHAR, VARCHAR ou VARCHAR LONGO|  
  
 Além da gramática SQL ODBC suportada, o Visual FoxPro ODBC Driver suporta a sintaxe completa da língua Visual FoxPro nativa para os seguintes comandos Visual FoxPro:  
  
 [ALTER TABLE](../../odbc/microsoft/alter-table-sql-command.md)  
  
 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)  
  
 [Delete (excluir)](../../odbc/microsoft/delete-sql-command.md)  
  
 [EXCLUIR TAG](../../odbc/microsoft/delete-tag-command.md)  
  
 [DROP TABLE](../../odbc/microsoft/drop-table-command.md)  
  
 [Índice](../../odbc/microsoft/index-command.md)  
  
 [Inserir](../../odbc/microsoft/insert-sql-command.md)  
  
 [SELECT](../../odbc/microsoft/select-sql-command.md)  
  
 [Atualização](../../odbc/microsoft/update-sql-command.md)
