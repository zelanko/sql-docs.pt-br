---
title: Tipos de dados do Microsoft Access | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], data types
- access data types [ODBC]
- data types [ODBC], Access driver
ms.assetid: b537348a-bea0-4bd6-84a4-52a75292957f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 024fb65b6fdc81ae0a8e007d1cee150c6a35b91c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307725"
---
# <a name="microsoft-access-data-types"></a>Tipos de dados do Microsoft Access
A tabela a seguir mostra os tipos de dados do Microsoft Access, os tipos de dados usados para criar tabelas e os tipos de dados SQL ODBC.  
  
|Tipo de dados do Microsoft Access|Tipo de dados (CRIARtable)|Tipo de dados SQL ODBC|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY [1]|LONGBINARY|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|NEUTRALIZA|NEUTRALIZA|SQL_INTEGER|  
|CURRENCY|CURRENCY|SQL_NUMERIC|  
|DATA/HORA|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|BINÁRIO LONGO|LONGBINARY|SQL_LONGVARBINARY|  
|TEXTO LONGO|LONGTEXT|SQL_LONGVARCHAR [2] SQL_WLONGVARCHAR [3]|  
|CAMPOS|LONGTEXT|SQL_LONGVARCHAR [2] SQL_WLONGVARCHAR [3]|  
|NUMBER (FieldSize = único)|EXCLUSIVO|SQL_REAL|  
|NUMBER (FieldSize = duplo)|DOUBLE|SQL_DOUBLE|  
|NUMBER (FieldSize = BYTE)|BYTE NÃO ASSINADO|SQL_TINYINT|  
|NUMBER (FieldSize = inteiro)|BAIXO|SQL_SMALLINT|  
|NUMBER (FieldSize = inteiro longo)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_VARCHAR [1] SQL_WVARCHAR [2]|  
|VARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] acesse apenas os aplicativos 4,0. Comprimento máximo de 4000 bytes. Comportamento semelhante a LONGBINARY.  
  
 [2] somente aplicativos ANSI.  
  
 [3] somente aplicativos Unicode e Access 4,0.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna tipos de dados ODBC. Ele não retornará todos os tipos de dados do Microsoft Access se mais de um tipo de acesso da Microsoft for mapeado para o mesmo tipo de dados ODBC do SQL. Todas as conversões no Apêndice D da *referência do programador de ODBC* têm suporte para os tipos de dados do SQL listados na tabela anterior.  
  
 A tabela a seguir mostra as limitações nos tipos de dados do Microsoft Access.  
  
|Tipo de dados|Descrição|  
|---------------|-----------------|  
|BINARY, VARBINARY e VARCHAR|Na verdade, a criação de uma coluna BINARY, VARBINARY ou VARCHAR de zero ou de comprimento não especificado retorna uma coluna de 510 bytes.|  
|BYTE|Embora um campo de número de acesso da Microsoft com um Fields igual a BYTE seja não assinado, um número negativo pode ser inserido no campo ao usar o driver do Microsoft Access.|  
|CHAR, LONGVARCHAR e VARCHAR|Um literal de cadeia de caracteres pode conter qualquer caractere ANSI (1-255 decimal). Use duas aspas simples consecutivas (' ') para representar uma aspa simples (').<br /><br /> Os procedimentos devem ser usados para passar dados de caracteres ao usar qualquer caractere especial em uma coluna de tipo de dados de caractere.|  
|DATE|Os valores de data devem ser delimitados de acordo com o formato de data canônico ODBC ou delimitados pelo delimitador de DateTime ("#"). Caso contrário, o Microsoft Access tratará o valor como uma expressão aritmética e não gerará um aviso ou erro.<br /><br /> Por exemplo, a data "5 de março de 1996" deve ser representada como {d ' 1996-03-05 '} ou #03/05/1996 #; caso contrário, se apenas 03/05/1993 for enviado, o Microsoft Access avaliará isso como 3 dividido por 5 dividido por 1996. Esse valor arredonda até o inteiro 0 e, uma vez que o dia zero é mapeado para 1899-12-31, essa é a data usada.<br /><br /> Um caractere de barra vertical (&#124;) não pode ser usado em um valor de data, mesmo se colocado entre aspas de fundo.|  
|GUID|Tipo de dados limitado ao Microsoft Access 4,0.|  
|NUMERIC|Tipo de dados limitado ao Microsoft Access 4,0.|  
  
 Mais limitações sobre tipos de dados podem ser encontradas em [limitações de tipo de dados](../../odbc/microsoft/data-type-limitations.md).
