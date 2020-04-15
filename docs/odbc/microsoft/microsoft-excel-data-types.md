---
title: Tipos de dados do Microsoft Excel | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Excel driver
- Excel data types [ODBC]
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], data types
ms.assetid: 7b44c8e5-0bc3-4912-8a5d-56f4d5562fe6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8574985e10e5aaa3ae5431af7ee1245643e20b60
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283766"
---
# <a name="microsoft-excel-data-types"></a>Tipos de dados do Microsoft Excel
A tabela a seguir mostra como os tipos de dados do driver do Microsoft Excel são mapeados para os tipos de dados SQL do ODBC. O driver do Microsoft Excel atribui esses tipos de dados a colunas em tabelas do Microsoft Excel com base nos dados da coluna.  
  
|Tipo de dados do Microsoft Excel|Tipo de dados ODBC|  
|-------------------------------|--------------------|  
|CURRENCY|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|Lógico|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna os tipos de dados ODBC SQL. Todas as conversões no apêndice D da *Referência do Programador ODBC* são suportadas para os tipos de dados SQL ODBC listados anteriormente neste tópico.  
  
 A tabela a seguir mostra limitações nos tipos de dados do Microsoft Excel.  
  
|Tipo de dados|Descrição|  
|---------------|-----------------|  
|Dados criptografados|O driver do Microsoft Excel não pode ler dados criptografados.|  
|Strings de erro|O driver do Microsoft Excel não pode retornar uma seqüência de caracteres para os valores de erro do Microsoft Excel (#N/A!, #VALUE!, #REF!, #DIV/0!, #NUM!, #NAME?, e #NULL!), mas retorna um NULL em vez disso.|  
|Lógico|O valor em uma coluna LOGICAL é devolvido em um buffer SQL_C_CHAR como 0 ou 1.|  
|NUMBER|Se uma coluna inteira for criada, números muito grandes para o tipo de dados inteiros podem ser inseridos e dados contendo valores não inteiros podem ser inseridos, com o resultado de que a coluna pode ser convertida em SQL_DOUBLE.|  
|TEXT|Quando as linhas de uma coluna contêm mais de um tipo de dados do Microsoft Excel, o driver ODBC Microsoft Excel atribui o SQL_VARCHAR tipo de dados à coluna. Há uma exceção a isso: se a coluna contiver apenas dois ou três dos tipos de dados de data-hora (DATA, HORA e DATA), o driver ODBC Microsoft Excel atribui o SQL_TIMESTAMP tipo de dados à coluna.<br /><br /> A criação de uma coluna text de comprimento zero ou não especificado realmente retorna uma coluna de 255 bytes.<br /><br /> Uma seqüência de caracteres literal pode conter qualquer caractere ANSI (1-255 decimal). Use duas aspas únicas consecutivas (") para representar uma única marca de cotação (').<br /><br /> Inserir um NULL em uma coluna com um tipo de dados diferente SQL_VARCHAR fará com que o tipo de dados da coluna mude para SQL_VARCHAR.|  
  
 Mais limitações nos tipos de dados podem ser encontradas nas [Limitações do Tipo de Dados](../../odbc/microsoft/data-type-limitations.md).
