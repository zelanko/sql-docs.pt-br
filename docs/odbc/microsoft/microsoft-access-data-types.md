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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b99fd70e0119aa01d384066aaa2f3b91eed152b4
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54420171"
---
# <a name="microsoft-access-data-types"></a>Tipos de dados do Microsoft Access
A tabela a seguir mostra os tipos de dados do Microsoft Access, os tipos de dados usados para criar tabelas e tipos de dados SQL ODBC.  
  
|Tipo de dados do Microsoft Access|Tipo de dados (CREATETABLE)|Tipo de dados SQL do ODBC|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY[1]|LONGBINARY|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|CONTADOR|CONTADOR|SQL_INTEGER|  
|CURRENCY|CURRENCY|SQL_NUMERIC|  
|DATA/HORA|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|BINÁRIO LONGO|LONGBINARY|SQL_LONGVARBINARY|  
|TEXTO LONGO|LONGTEXT|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR[3]|  
|MEMORANDO|LONGTEXT|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR[3]|  
|NÚMERO (tamanho do campo = SOLTEIRO)|ÚNICO|SQL_REAL|  
|NÚMERO (tamanho do campo = dupla)|DOUBLE|SQL_DOUBLE|  
|NÚMERO (tamanho do campo = BYTE)|BYTE SEM SINAL|SQL_TINYINT|  
|NUMBER (FieldSize= INTEGER)|CURTO|SQL_SMALLINT|  
|NUMBER (FieldSize= LONG INTEGER)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_VARCHAR[1] SQL_WVARCHAR[2]|  
|VARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] somente aplicativos de acesso 4.0. Comprimento máximo de 4000 bytes. Comportamento semelhante ao LONGBINARY.  
  
 [2] somente aplicativos ANSI.  
  
 [3] Unicode e acesso 4.0 somente aplicativos.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna tipos de dados ODBC. Ele não retornará todos os tipos de dados do Microsoft Access, se mais de um tipo de Microsoft Access for mapeado para o mesmo tipo de dados SQL ODBC. Todas as conversões no Apêndice D dos *referência do programador de ODBC* têm suporte para os tipos de dados SQL listados na tabela anterior.  
  
 A tabela a seguir mostra as limitações nos tipos de dados do Microsoft Access.  
  
|Tipo de dados|Descrição|  
|---------------|-----------------|  
|BINÁRIO, VARBINARY e VARCHAR|Criação de uma coluna BINARY, VARBINARY ou VARCHAR igual a zero ou comprimento não especificado, na verdade, retorna uma coluna 510 bytes.|  
|BYTE|Mesmo que um campo de número de acesso da Microsoft com um FieldSize igual a BYTE não estiver assinado, um número negativo pode ser inserido no campo ao usar o driver do Microsoft Access.|  
|VARCHAR, LONGVARCHAR e CHAR|Um literal de cadeia de caracteres pode conter qualquer caractere ANSI (1 a 255 decimal). Use duas aspas simples consecutivas (") para representar uma marca de aspas simples (').<br /><br /> Procedimentos devem ser usados para passar dados de caractere ao usar qualquer caractere especial em uma coluna de tipo de dados de caractere.|  
|DATE|Valores de data devem ser delimitados de acordo com o formato de data canônica ODBC ou delimitadas pelo delimitador de data e hora ("#"). Caso contrário, o Microsoft Access tratará o valor como uma expressão aritmética e não gerará um aviso ou erro.<br /><br /> Por exemplo, a data em que "5 de março de 1996" deve ser representada como {1!d ' 1996-03-05'} ou # #03/05/1996; Caso contrário, se apenas 05/03/1993 for enviada, o Microsoft Access avaliará essa como 3 dividido por 5 dividido por 1996. Esse valor arredondado para cima para o inteiro de 0, e como o dia zero é mapeado para 1899-12-31, essa é a data usada.<br /><br /> Um caractere de barra vertical (&#124;) não pode ser usado em um valor de data, mesmo se os novamente entre aspas.|  
|GUID|Tipo de dados limitado para o Microsoft Access 4.0.|  
|NUMERIC|Tipo de dados limitado para o Microsoft Access 4.0.|  
  
 Mais limitações nos tipos de dados podem ser encontradas na [limitações do tipo de dados](../../odbc/microsoft/data-type-limitations.md).
