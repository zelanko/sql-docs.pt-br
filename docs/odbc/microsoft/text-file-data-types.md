---
title: Tipos de dados do arquivo de texto | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], data types
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- text file data types [ODBC]
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: e113112e-ae42-469e-8e4b-a365a10d9071
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d3ac713de27efa4ddc41ec52285231dde7518402
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="text-file-data-types"></a>Tipos de dados do arquivo de texto
A tabela a seguir mostra como os tipos de dados de texto são mapeados para tipos de dados SQL ODBC. Observe que nem todos os tipos de dados SQL ODBC são suportados pelo driver ODBC texto.  
  
|Tipo de dados de texto|Tipo de dados ODBC|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna tipos de dados ODBC. Todas as conversões no Apêndice D do *referência do programador de ODBC* têm suporte para os tipos de dados SQL listados na tabela anterior.  
  
 A tabela a seguir mostra as limitações nos tipos de dados de texto.  
  
|Tipo de dados|Description|  
|---------------|-----------------|  
|CHAR|Criar uma coluna CHAR zero ou comprimento especificado, na verdade, retorna uma coluna de bits de 255.<br /><br /> Nos arquivos delimitados, uma coluna CHAR pode ou não ter delimitadores de aspas duplas no início e final; nos arquivos de comprimento fixo, aspas duplas não são usadas como delimitadores.|  
|DATETIME|MM-DD-AA (por exemplo, 01-17-92)<br /><br /> MMM-DD-AA (por exemplo, Jan-17-92)<br /><br /> DD-MMM-AA (por exemplo, 17-Jan-92)<br /><br /> AAAA-MM-DD (por exemplo, 1992-01-17)<br /><br /> AAAA-MMM-DD (por exemplo, 1992-Jan-17)<br /><br /> Separadores de data misto não são permitidas dentro de uma tabela.<br /><br /> O texto ISAM formata um campo de data e hora no formato dos Estados Unidos ou europeu, dependendo da configuração internacional no painel de controle do Windows.|  
|FLOAT|A largura máxima inclui o sinal e o ponto decimal. No Schema, a largura é indicada como segue:<br /><br /> 14.083 é FLOAT 6 de largura<br /><br /> -14.083 é FLOAT largura 7<br /><br /> +14.083 é FLOAT largura 7<br /><br /> 14083. é a largura FLOAT 6<br /><br /> ODBC sempre retorna 8 para colunas FLOAT.<br /><br /> Colunas FLOAT também podem ser em notação científica, por exemplo:<br /><br /> -3.04E + 2 é Float largura 8<br /><br /> 25E4 é Float 4 de largura<br /><br /> **Observação** notação científica e Decimal não pode ser combinada em uma coluna.<br /><br /> Valores nulos são representados por uma cadeia de caracteres preenchida em branco em arquivos de comprimento fixo e forem omitidos em arquivos delimitados.<br /><br /> Dados float podem ser preenchidos com espaços em branco à esquerda.|  
|INTEGER|Os valores válidos para colunas de INTEIROS são 32767 para -32766.<br /><br /> No Schema, a largura é indicada como segue:<br /><br /> 14083 é 5 de largura de inteiro<br /><br /> 0 é 1 de largura de inteiro<br /><br /> ODBC sempre retorna 4 para colunas de INTEIROS.<br /><br /> A largura máxima inclui uma entrada. A largura máxima de uma coluna de inteiro é 11, embora a largura poderá ser maior devido a espaços em branco que são permitidos em tabelas de formato fixo.|  
|LONGCHAR|Limita o teórico na largura de uma coluna LONGCHAR no comprimento fixo ou tabela delimitada 65500K. ISAM do texto é mais provável oferecer suporte confiável até aproximadamente 32 K.|  
  
 Mais limitações nos tipos de dados podem ser encontradas no [limitações do tipo de dados](../../odbc/microsoft/data-type-limitations.md).
