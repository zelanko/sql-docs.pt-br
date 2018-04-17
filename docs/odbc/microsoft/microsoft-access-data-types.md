---
title: Tipos de dados do Microsoft Access | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], data types
- access data types [ODBC]
- data types [ODBC], Access driver
ms.assetid: b537348a-bea0-4bd6-84a4-52a75292957f
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: 8faac619846998c1be7bc0577761b94bf6dc27ba
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="microsoft-access-data-types"></a>Tipos de dados do Microsoft Access
A tabela a seguir mostra os tipos de dados do Microsoft Access, tipos de dados usados para criar tabelas e tipos de dados SQL ODBC.  
  
|Tipo de dados do Microsoft Access|Tipo de dados (CREATETABLE)|Tipo de dados ODBC SQL|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY [1]|LONGBINARY|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|CONTADOR|CONTADOR|SQL_INTEGER|  
|CURRENCY|CURRENCY|SQL_NUMERIC|  
|DATA/HORA|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|BINÁRIO LONGO|LONGBINARY|SQL_LONGVARBINARY|  
|TEXTO LONGO|LONGTEXT|SQL_WLONGVARCHAR SQL_LONGVARCHAR [2] [3]|  
|MEMORANDO|LONGTEXT|SQL_WLONGVARCHAR SQL_LONGVARCHAR [2] [3]|  
|NÚMERO (tamanho do campo = único)|ÚNICO|SQL_REAL|  
|NÚMERO (tamanho do campo = duplo)|DOUBLE|SQL_DOUBLE|  
|NÚMERO (tamanho do campo = BYTE)|BYTE NÃO ATRIBUÍDO|SQL_TINYINT|  
|NÚMERO (tamanho do campo = inteiro)|CURTO|SQL_SMALLINT|  
|NÚMERO (tamanho do campo = inteiro longo)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_WVARCHAR SQL_VARCHAR [1] [2]|  
ARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] somente aplicativos de acesso 4.0. Comprimento máximo de bytes 4000. Comportamento semelhante ao LONGBINARY.  
  
 [2] somente aplicativos ANSI.  
  
 [3] Unicode e acesso 4.0 aplicativos somente.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna tipos de dados ODBC. Ela não retornará todos os tipos de dados do Microsoft Access se mais de um tipo do Microsoft Access é mapeado para o mesmo tipo de dados SQL ODBC. Todas as conversões no Apêndice D do *referência do programador de ODBC* têm suporte para os tipos de dados SQL listados na tabela anterior.  
  
 A tabela a seguir mostra as limitações nos tipos de dados do Microsoft Access.  
  
|Tipo de dados|Description|  
|---------------|-----------------|  
|BINARY, VARBINARY e VARCHAR|Criar uma coluna BINARY, VARBINARY ou VARCHAR zero ou uma coluna 510 bytes realmente retorna um comprimento especificado.|  
|BYTE|Mesmo que um campo de número de acesso da Microsoft com um FieldSize igual a bytes é não assinado, um número negativo pode ser inserido no campo usando o driver do Microsoft Access.|  
|VARCHAR, LONGVARCHAR e CHAR|Um literal de cadeia de caracteres pode conter qualquer caractere ANSI (decimal de 1 a 255). Use duas aspas simples consecutivas (") para representar uma aspa simples (').<br /><br /> Procedimentos devem ser usados para passar dados de caractere ao usar caracteres especiais em uma coluna de tipo de dados de caractere.|  
|DATE|Valores de data devem ser delimitados de acordo com o formato de data canônica ODBC ou delimitados pelo delimitador de data/hora ("#"). Caso contrário, o Microsoft Access tratará o valor como uma expressão aritmética e não gerará um erro ou aviso.<br /><br /> Por exemplo, a data de "5 de março de 1996" devem ser representados como {d ' 1996-03-05'} ou # #03/05/1996; Caso contrário, se apenas 05/03/1993 é enviado, o Microsoft Access avaliará essa como 3 dividido por 5 dividido por 1996. Esse valor é arredondado para cima até o inteiro 0, e desde o dia zero mapeia para 1899-12-31, esta é a data usada.<br /><br /> Um caractere de pipe (&#124;) não pode ser usado em um valor de data, mesmo se atrás entre aspas.|  
|GUID|Tipo de dados limitado para o Microsoft Access 4.0.|  
|NUMERIC|Tipo de dados limitado para o Microsoft Access 4.0.|  
  
 Mais limitações nos tipos de dados podem ser encontradas no [limitações do tipo de dados](../../odbc/microsoft/data-type-limitations.md).
