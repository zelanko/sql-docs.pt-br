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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7864dc81eaa3dd37f3d0053b2329c8842e445c8d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302654"
---
# <a name="text-file-data-types"></a>Tipos de dados de Arquivo de texto
A tabela a seguir mostra como os tipos de dados de texto são mapeados para os tipos de dados SQL do ODBC. Observe que nem todos os tipos de dados ODBC SQL são suportados pelo driver de texto ODBC.  
  
|Tipo de dados de texto|Tipo de dados ODBC|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|Longchar|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** retorna os tipos de dados ODBC. Todas as conversões no apêndice D da *Referência do Programador ODBC* são suportadas para os tipos de dados SQL listados na tabela anterior.  
  
 A tabela a seguir mostra limitações nos tipos de dados de texto.  
  
|Tipo de dados|Descrição|  
|---------------|-----------------|  
|CHAR|A criação de uma coluna CHAR de comprimento zero ou não especificado realmente retorna uma coluna de 255 bits.<br /><br /> Em arquivos delimitados, uma coluna CHAR pode ou não ter delimitadores de marca de cotação dupla no início e no final; em arquivos de comprimento fixo, aspas duplas não são usadas como delimitadores.|  
|DATETIME|MM-DD-YY (por exemplo, 01-17-92)<br /><br /> MMM-DD-YY (por exemplo, Jan-17-92)<br /><br /> DD-MMM-YY (por exemplo, 17-Jan-92)<br /><br /> YYYY-MM-DD (por exemplo, 1992-01-17)<br /><br /> YYYY-MMM-DD (por exemplo, 1992-Jan-17)<br /><br /> Separadores de datas mistas não são permitidos dentro de uma tabela.<br /><br /> O texto ISAM formata um campo DATETIME nos Estados Unidos ou formato europeu, dependendo da configuração internacional no Painel de Controle do Windows.|  
|FLOAT|A largura máxima inclui o sinal e o ponto decimal. Em Schema.ini, a largura é denotada da seguinte forma:<br /><br /> 14.083 é float largura 6<br /><br /> -14.083 é float largura 7<br /><br /> +14.083 é FLOAT Largura 7<br /><br /> 14083. é largura flutuante 6<br /><br /> ODBC sempre retorna 8 para colunas FLOAT.<br /><br /> Colunas FLOAT também podem estar em notação científica, por exemplo:<br /><br /> -3.04E+2 é largura de flutuação 8<br /><br /> 25E4 é largura de flutuação 4<br /><br /> **Nota** Notação decimal e científica não pode ser misturada em uma coluna.<br /><br /> Os valores NULL são representados por uma seqüência de cadeia sacada em branco em arquivos de comprimento fixo e são omitidos em arquivos delimitados.<br /><br /> Os dados flutuantes podem ser acolchoados com espaços em branco principais.|  
|INTEGER|Os valores válidos para as colunas INTEGER são de 32767 a -32766.<br /><br /> Em Schema.ini, a largura é denotada da seguinte forma:<br /><br /> 14083 é largura INTEGER 5<br /><br /> 0 é largura INTEGER 1<br /><br /> ODBC sempre retorna 4 para colunas INTEGER.<br /><br /> A largura máxima inclui um sinal. A largura máxima de uma coluna INTEGER é de 11, embora a largura possa ser maior devido a espaços em branco permitidos em tabelas de formato fixo.|  
|Longchar|O limite teórico na largura de uma coluna LONGCHAR em uma tabela de comprimento fixo ou delimitada é de 65500K. O texto ISAM é mais provável que forneça suporte confiável até cerca de 32K.|  
  
 Mais limitações nos tipos de dados podem ser encontradas nas [Limitações do Tipo de Dados](../../odbc/microsoft/data-type-limitations.md).
