---
title: Tipos de dados paradoxais | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- desktop database drivers [ODBC], Paradox driver
- Paradox data types [ODBC]
- Jet-based ODBC drivers [ODBC], Paradox driver
- data types [ODBC], Paradox driver
- Paradox driver [ODBC], data types
ms.assetid: 0c9e5d21-9321-49f8-a055-69459e1c9c85
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a85cf643a6d22b9b2fce15984539d74dc43c62ab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290926"
---
# <a name="paradox-data-types"></a>Tipos de dados Paradox
O driver ODBC Paradox mapeia os tipos de dados Paradox para os tipos de dados SQL do ODBC. A tabela a seguir lista todos os tipos de dados paradoxos e mostra os tipos de dados ODBC SQL para os quais são mapeados.  
  
|Tipo de dados paradoxo|Tipo de dados ODBC|  
|-----------------------|--------------------|  
|Alfanumérico|SQL_VARCHAR|  
|AUTOINCREMENT[1]|SQL_INTEGER|  
|BCD[1]|SQL_DOUBLE|  
|BYTES[1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|IMAGEM[2]|SQL_LONGVARBINARY|  
|LÓGICA[1]|SQL_BIT|  
|LONG[1]|SQL_INTEGER|  
|MEMO[2]|SQL_LONGVARCHAR|  
|DINHEIRO[1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|SHORT|SQL_SMALLINT|  
|TIME[1]|SQL_TIMESTAMP|  
|CARIMBO DE TEMPO[1]|SQL_TIMESTAMP|  
  
 [1] Válido apenas para as versões Paradox 5. *x*.  
  
 [2] Válido apenas para as versões Paradox 4. *x* e 5. *x*.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna os tipos de dados ODBC SQL. Todas as conversões no apêndice D da *Referência do Programador ODBC* são suportadas para os tipos de dados SQL ODBC listados anteriormente neste tópico.  
  
 A tabela a seguir mostra limitações nos tipos de dados Paradox.  
  
|Tipo de dados|Descrição|  
|---------------|-----------------|  
|Alfanumérico|A criação de uma coluna ALPHANUMERIC de comprimento zero ou não especificado realmente retorna uma coluna de 255 bytes.|  
|BYTES|Se você inserir NULL em uma coluna binária com o driver Paradox5, ele será alterado para 0.|  
|LONG|O valor negativo máximo suportado pelo driver Paradoxpara o tipo de dados Longos no Paradox5. *x* não é -2^31 (-2147483648), como deve ser desde long mapeia para o tipo de dados ODBC SQL_INTEGER. O valor negativo máximo suportado para Long é na verdade -2^31 + 1 (-2147483647).|  
|timestamp|Quando um valor é inserido em uma coluna TIMESTAMP pelo driver Paradox, posteriormente recuperado da coluna, o valor recuperado pode diferir do valor inserido em até 1 segundo por causa do arredondamento.|  
  
 Mais limitações nos tipos de dados podem ser encontradas nas [Limitações do Tipo de Dados](../../odbc/microsoft/data-type-limitations.md).
