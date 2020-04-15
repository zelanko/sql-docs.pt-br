---
title: Tipos de dados de acesso da Microsoft | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307725"
---
# <a name="microsoft-access-data-types"></a>Tipos de dados do Microsoft Access
A tabela a seguir mostra os tipos de dados do Microsoft Access, os tipos de dados usados para criar tabelas e os tipos de dados SQL do ODBC.  
  
|Tipo de dados do Microsoft Access|Tipo de dados (CREATETABLE)|Tipo de dados ODBC SQL|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY[1]|LONGBINARY|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|Counter|Counter|SQL_INTEGER|  
|CURRENCY|CURRENCY|SQL_NUMERIC|  
|DATA/HORA|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|BINÁRIO LONGO|LONGBINARY|SQL_LONGVARBINARY|  
|TEXTO LONGO|Longtext|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR[3]|  
|Memorando|Longtext|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR[3]|  
|NÚMERO (FieldSize= SINGLE)|Único|SQL_REAL|  
|NÚMERO (Tamanho de campo= DUPLO)|DOUBLE|SQL_DOUBLE|  
|NÚMERO (FieldSize= BYTE)|BYTE NÃO ASSINADO|SQL_TINYINT|  
|NÚMERO (FieldSize= INTEIRO)|SHORT|SQL_SMALLINT|  
|NÚMERO (FieldSize= INTEIRO LONGO)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_VARCHAR[1] SQL_WVARCHAR[2]|  
|VARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] Acesse apenas os aplicativos 4.0. Comprimento máximo de 4000 bytes. Comportamento semelhante ao LONGBINARY.  
  
 [2] Somente aplicações ANSI.  
  
 [3] Somente aplicativos Unicode e Access 4.0.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna os tipos de dados ODBC. Ele não retornará todos os tipos de dados do Microsoft Access se mais de um tipo de Microsoft Access for mapeado para o mesmo tipo de dados SQL do ODBC. Todas as conversões no apêndice D da *Referência do Programador ODBC* são suportadas para os tipos de dados SQL listados na tabela anterior.  
  
 A tabela a seguir mostra limitações nos tipos de dados do Microsoft Access.  
  
|Tipo de dados|Descrição|  
|---------------|-----------------|  
|BINÁRIO, VARBINÁRIO e VARCHAR|A criação de uma coluna BINÁRIA, VARBINARY ou VARCHAR de comprimento zero ou não especificado realmente retorna uma coluna de 510 bytes.|  
|BYTE|Embora um campo número de acesso do Microsoft com um FieldSize igual ao BYTE não esteja assinado, um número negativo pode ser inserido no campo ao usar o driver Microsoft Access.|  
|CHAR, LONGVARCHAR e VARCHAR|Uma seqüência de caracteres literal pode conter qualquer caractere ANSI (1-255 decimal). Use duas aspas únicas consecutivas ('') para representar uma única marca de cotação (').<br /><br /> Os procedimentos devem ser usados para passar dados de caracteres ao usar qualquer caractere especial em uma coluna de tipo de dados de caracteres.|  
|DATE|Os valores das datas devem ser delimitados de acordo com o formato de data canônica da ODBC ou delimitados pelo delimitador de data ("#"). Caso contrário, o Microsoft Access tratará o valor como uma expressão aritmética e não levantará um aviso ou erro.<br /><br /> Por exemplo, a data "5 de março de 1996" deve ser representada como {d '1996-03-05'} ou #03/05/1996#; caso contrário, se apenas 03/05/1993 for submetido, o Microsoft Access avaliará isso como 3 dividido por 5 dividido por 1996. Este valor é de até o inteiro 0, e desde os mapas do dia zero para 1899-12-31, esta é a data utilizada.<br /><br /> Um caractere de tubo (&#124;) não pode ser usado em um valor de data, mesmo se fechado em aspas traseiras.|  
|GUID|Tipo de dados limitado ao Microsoft Access 4.0.|  
|NUMERIC|Tipo de dados limitado ao Microsoft Access 4.0.|  
  
 Mais limitações nos tipos de dados podem ser encontradas nas [Limitações do Tipo de Dados](../../odbc/microsoft/data-type-limitations.md).
