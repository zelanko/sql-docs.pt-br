---
title: Suporte a gramática de SQL ODBC (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7eccb1bbdb86ded6b949756b4e5762a83a59fc0e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32906911"
---
# <a name="supported-odbc-sql-grammar-visual-foxpro-odbc-driver"></a>Gramática SQL ODBC com suporte (Driver ODBC do Visual FoxPro)
O Driver ODBC do Microsoft Visual FoxPro suporta o seguinte:  
  
-   Todas as instruções SQL e cláusulas na gramática SQL mínima do ODBC  
  
-   Uma instrução SQL adicional de gramática SQL principal ODBC  
  
 A tabela a seguir lista os itens com suporte pelo driver, por nível de gramática de SQL ODBC.  
  
|Nível|Elementos|Item|  
|-----------|--------------|----------|  
|Mínimo|DDL (linguagem de definição de dados)|CREATE TABLE e DROP TABLE|  
||DML (linguagem de manipulação de dados)|Selecionar, inserir, atualizar e excluir|  
||Expressões|Simples (como um > B + C)|  
||Tipos de dados|CHAR, VARCHAR ou LONG VARCHAR|  
  
 Além a gramática SQL ODBC com suporte, o Driver de ODBC do Visual FoxPro oferece suporte a sintaxe de linguagem do Visual FoxPro nativo completa para os seguintes comandos do Visual FoxPro:  
  
 [INSTRUÇÃO ALTER TABLE](../../odbc/microsoft/alter-table-sql-command.md)  
  
 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)  
  
 [DELETE](../../odbc/microsoft/delete-sql-command.md)  
  
 [EXCLUIR MARCA](../../odbc/microsoft/delete-tag-command.md)  
  
 [DROP TABLE](../../odbc/microsoft/drop-table-command.md)  
  
 [INDEX](../../odbc/microsoft/index-command.md)  
  
 [INSERT](../../odbc/microsoft/insert-sql-command.md)  
  
 [SELECT](../../odbc/microsoft/select-sql-command.md)  
  
 [UPDATE](../../odbc/microsoft/update-sql-command.md)
