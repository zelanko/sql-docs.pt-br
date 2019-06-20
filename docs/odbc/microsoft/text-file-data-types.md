---
title: Tipos de dados do arquivo de texto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], data types
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- text file data types [ODBC]
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: e113112e-ae42-469e-8e4b-a365a10d9071
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23416cb067507d821701e57255fdc6f81ee607c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62632999"
---
# <a name="text-file-data-types"></a>Tipos de dados de Arquivo de texto
A tabela a seguir mostra como os tipos de dados de texto são mapeados para tipos de dados SQL ODBC. Observe que nem todos os tipos de dados ODBC SQL têm suporte pelo driver ODBC de texto.  
  
|Tipo de dados de texto|Tipo de dados ODBC|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna tipos de dados ODBC. Todas as conversões no Apêndice D dos *referência do programador de ODBC* têm suporte para os tipos de dados SQL listados na tabela anterior.  
  
 A tabela a seguir mostra as limitações nos tipos de dados de texto.  
  
|Tipo de dados|Descrição|  
|---------------|-----------------|  
|CHAR|Criação de uma coluna CHAR igual a zero ou comprimento não especificado, na verdade, retorna uma coluna de bits de 255.<br /><br /> Em arquivos delimitados, uma coluna CHAR pode ou não ter delimitadores de aspas duplas no início e no final; em arquivos de comprimento fixo, aspas duplas não são usadas como delimitadores.|  
|DATETIME|MM-DD-AA (por exemplo, 01-17-92)<br /><br /> DD-MMM-AA (por exemplo, Jan-17-92)<br /><br /> DD-MMM-AA (por exemplo, 17 de janeiro de 92)<br /><br /> AAAA-MM-DD (por exemplo, 1992-01-17)<br /><br /> DD-MMM-AAAA (por exemplo, 1992-Jan-17)<br /><br /> Separadores de data misto não são permitidas dentro de uma tabela.<br /><br /> O texto ISAM formata um campo de data e hora no formato dos Estados Unidos ou na Europa, dependendo da configuração internacional no painel de controle do Windows.|  
|FLOAT|A largura máxima inclui a entrada e o ponto decimal. No Schema. ini, a largura é indicada da seguinte maneira:<br /><br /> 14.083 é FLOAT largura 6<br /><br /> -14.083 é FLOAT 7 de largura<br /><br /> +14.083 é FLOAT 7 de largura<br /><br /> 14083. é FLOAT largura 6<br /><br /> ODBC sempre retorna 8 para colunas FLOAT.<br /><br /> Colunas FLOAT também podem ser em notação científica, por exemplo:<br /><br /> -3.04E + 2 é 8 Float de largura<br /><br /> 25E4 é 4 de largura de Float<br /><br /> **Observação** notação científica e Decimal não pode ser combinada em uma coluna.<br /><br /> Valores nulos são representados por uma cadeia de caracteres preenchida em branco nos arquivos de comprimento fixo e são omitidos nos arquivos delimitados.<br /><br /> Dados float podem ser preenchidos com espaços em branco à esquerda.|  
|INTEGER|Os valores válidos para colunas de INTEIROS são 32767 para -32766.<br /><br /> No Schema. ini, a largura é indicada da seguinte maneira:<br /><br /> 14083 é 5 de largura de inteiro<br /><br /> 0 é o inteiro 1 de largura<br /><br /> ODBC sempre retorna 4 para colunas de INTEIROS.<br /><br /> A largura máxima inclui uma entrada. A largura máxima de uma coluna de INTEIROS é 11, embora a largura pode ser maior devido a espaços em branco que são permitidos em tabelas de formato fixo.|  
|LONGCHAR|Limita o teórica na largura de uma coluna LONGCHAR em qualquer um de comprimento fixo ou tabela delimitada 65500K. ISAM do texto é mais provável fornecer suporte confiável até aproximadamente 32 K.|  
  
 Mais limitações nos tipos de dados podem ser encontradas na [limitações do tipo de dados](../../odbc/microsoft/data-type-limitations.md).
