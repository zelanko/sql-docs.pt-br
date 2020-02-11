---
title: Tipos de dados de arquivo de texto | Microsoft Docs
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
ms.openlocfilehash: 829f924d8d4893d45a48c193cd27fdd7ac261e3d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67939719"
---
# <a name="text-file-data-types"></a>Tipos de dados de Arquivo de texto
A tabela a seguir mostra como os tipos de dados de texto são mapeados para tipos de dados ODBC do SQL. Observe que nem todos os tipos de dados SQL ODBC são suportados pelo driver de texto ODBC.  
  
|Tipo de dados text|Tipo de dados ODBC|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna tipos de dados ODBC. Todas as conversões no Apêndice D da *referência do programador de ODBC* têm suporte para os tipos de dados do SQL listados na tabela anterior.  
  
 A tabela a seguir mostra as limitações em tipos de dados de texto.  
  
|Tipo de dados|DESCRIÇÃO|  
|---------------|-----------------|  
|CHAR|Na verdade, a criação de uma coluna CHAR com comprimento zero ou não especificado retorna uma coluna de 255 bits.<br /><br /> Em arquivos delimitados, uma coluna CHAR pode ou não ter delimitadores de aspas duplas no início e no final; em arquivos de comprimento fixo, aspas duplas não são usadas como delimitadores.|  
|DATETIME|MM-DD-AA (por exemplo, 01-17-92)<br /><br /> MMM-DD-AA (por exemplo, Jan-17-92)<br /><br /> DD-MMM-AA (por exemplo, 17 de janeiro de 92)<br /><br /> AAAA-MM-DD (por exemplo, 1992-01-17)<br /><br /> AAAA-MMM-DD (por exemplo, 1992-Jan-17)<br /><br /> Separadores de datas mistas não são permitidos em uma tabela.<br /><br /> O texto ISAM formata um campo DATETIME no formato Estados Unidos ou Europeu, dependendo da configuração internacional no painel de controle do Windows.|  
|FLOAT|A largura máxima inclui o sinal e o ponto decimal. Em Schema. ini, a largura é denotada da seguinte maneira:<br /><br /> 14, 83 é a largura do FLOAT 6<br /><br /> -14, 83 é a largura do FLOAT 7<br /><br /> + 14, 83 é a largura do FLOAT 7<br /><br /> 14083. a largura do FLOAT é 6<br /><br /> O ODBC sempre retorna 8 para colunas FLOAT.<br /><br /> As colunas FLOAT também podem estar em notação científica, por exemplo:<br /><br /> -3.04 e + 2 é a largura do float 8<br /><br /> 25E4 é a largura do float 4<br /><br /> **Observação** A notação decimal e científica não pode ser misturada em uma coluna.<br /><br /> Os valores nulos são representados por uma cadeia de caracteres preenchida em branco em arquivos de comprimento fixo e são omitidos em arquivos delimitados.<br /><br /> Os dados float podem ser preenchidos com espaços em branco à esquerda.|  
|INTEGER|Os valores válidos para colunas de inteiros são 32767 a-32766.<br /><br /> Em Schema. ini, a largura é denotada da seguinte maneira:<br /><br /> 14083 é a largura do inteiro 5<br /><br /> 0 é a largura do inteiro 1<br /><br /> O ODBC sempre retorna 4 para colunas de inteiros.<br /><br /> A largura máxima inclui um sinal. A largura máxima de uma coluna de inteiros é 11, embora a largura possa ser maior devido a espaços em branco permitidos em tabelas de formato fixo.|  
|LONGCHAR|O limite teórico na largura de uma coluna LONGCHAR em uma tabela de comprimento fixo ou delimitado é 65500K. O texto ISAM tem mais probabilidade de fornecer suporte confiável para cerca de 32K.|  
  
 Mais limitações sobre tipos de dados podem ser encontradas em [limitações de tipo de dados](../../odbc/microsoft/data-type-limitations.md).
