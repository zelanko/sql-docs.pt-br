---
title: Mapeamento de caracteres do SQL Server e MySQL definido (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c9b3fc89548b10593cb16e2a70c93afe9b56350e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>Mapeamento de caracteres do SQL Server e MySQL definido (MySQLToSQL)
Conjunto de caracteres (Charset) pode ser especificado para tipos de dados MySQL, expressões e literais.  
  
## <a name="charset-mapping"></a>Mapeamento de conjunto de caracteres  
Mapeamento de conjunto de caracteres é definido para cada conjunto de caracteres do MySQL e usado durante a conversão de tipo de dados de caractere. Especifica como converter tipos de dados de cadeia de caracteres de um conjunto de caracteres em particular:  
  
-   Para tipos de caractere nacionais do SQL Server (NCHAR/NVARCHAR), ou  
  
-   Para tipos de caracteres regulares do SQL Server (CHAR/VARCHAR)  
  
1.  **National** são de tipos de dados de caracteres de banco de dados de destino:  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  **regular** são de tipos de dados de caracteres de banco de dados de destino:  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  Mapeamento de tipo só permite o mapeamento para **national** tipos de dados de caractere. Depois que o tipo de dados de caractere do MySQL é convertido de acordo com o mapeamento de tipo, o mapeamento de conjunto de caracteres é aplicado.  
  
> [!NOTE]  
> Mapeamento de conjunto de caracteres pode ser definida em cada nível de nó do Pesquisador de objetos de metadados e representam todos os conjuntos de caracteres lidos do MySQL.  
  
## <a name="charset-mapping-on-different-node-levels"></a>Mapeamento de conjunto de caracteres em diferentes níveis de nó  
Mapeamento de conjunto de caracteres varia em diferentes níveis de nó, ou seja:  
  
1.  No nível de nó de metadados da raiz  
  
2.  No banco de dados, categoria e nível de nó de objeto  
  
> [!NOTE]  
> A guia selecionada para editar o mapeamento de conjunto de caracteres, contém três botões, independentemente do mapeamento nos níveis de nó diferente.  
>   
> São eles:  
>   
> 1.  **Se aplicam:** aplica as alterações feitas pelo usuário, habilitado somente quando o mapeamento de conjunto de caracteres é editado e ainda não foi salvo.  
> 2.  **Cancelar:** cancela as alterações feitas pelo usuário. O botão obtém habilitado quando o mapeamento de conjunto de caracteres é editado mas não foi salvo.  
> 3.  **Redefinir para padrão:** redefine todos os mapeamentos para os valores padrão.  
  
1.  **No nível de nó de metadados de raiz:** grade de mapeamento de conjunto de caracteres contém a grade de conjunto de caracteres com uma coluna separada para cada conjunto de caracteres. As colunas da grade são:  
  
    1.  A primeira coluna da grade nomeada **nome do conjunto de caracteres** contém o nome do conjunto de caracteres.  
  
    2.  O outro denominado **descrição do conjunto de caracteres** contém a descrição do conjunto de caracteres.  
  
    3.  A terceira coluna intitulada **tipo de conjunto de caracteres de destino** contém as configurações de mapeamento de conjunto de caracteres específica. Os valores desta coluna são:  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
    > [!IMPORTANT]  
    > Os valores padrão para um determinado conjunto de caracteres têm o prefixo '(padrão)' após CHAR/VARCHAR ou NCHAR/NVARCHAR.  
  
    O mapeamento de conjunto de caracteres entre banco de dados MySQL e o banco de dados de destino no nível de nó raiz metadados é fornecido abaixo:  
  
    ||||  
    |-|-|-|  
    |**Nome do conjunto de caracteres**|**Descrição do conjunto de caracteres**|**Tipo de conjunto de caracteres de destino (padrão)**|  
    |Big5|Chinês tradicional Big5|NCHAR/NVARCHAR (padrão)|  
    |dec8|Europeu Ocidental DEC|CHAR/VARCHAR (padrão)|  
    |cp850|Oeste DOS Europeu|CHAR/VARCHAR (padrão)|  
    |hp8|HP oeste Europeu|CHAR/VARCHAR (padrão)|  
    |koi8r|KOI8-R Relcom russo|CHAR/VARCHAR (padrão)|  
    |Latino 1|CP1252 oeste Europeu|CHAR/VARCHAR (padrão)|  
    |latin2|Europeu Central ISO 8859-2|CHAR/VARCHAR (padrão)|  
    |swe7|7 bits sueco|CHAR/VARCHAR (padrão)|  
    |ASCII|US ASCII|CHAR/VARCHAR (padrão)|  
    |ujis|EUC-JP japonês|NCHAR/NVARCHAR (padrão)|  
    |SJIS|Japonês Shift JIS|NCHAR/NVARCHAR (padrão)|  
    |Hebraico|ISO 8859-8 Hebraico|CHAR/VARCHAR (padrão)|  
    |tis620|TIS620 tailandês|CHAR/VARCHAR (padrão)|  
    |euckr|Coreano EUC-KR|NCHAR/NVARCHAR (padrão)|  
    |koi8u|Ucraniano KOI8-U|CHAR/VARCHAR (padrão)|  
    |GB2312|GB2312 Chinês simplificado|NCHAR/NVARCHAR (padrão)|  
    |Grego|ISO 8859-7 Grego|CHAR/VARCHAR (padrão)|  
    |CP 1250|Europeu Central do Windows|CHAR/VARCHAR (padrão)|  
    |GBK|E chinês simplificado GBK|NCHAR/NVARCHAR (padrão)|  
    |latin5|ISO 8859-9 Turco|CHAR/VARCHAR (padrão)|  
    |armscii8|Armênio ARMSCII-8|CHAR/VARCHAR (padrão)|  
    |UTF8|Unicode UTF-8|NCHAR/NVARCHAR (padrão)|  
    |ucs2|Unicode UCS-2|NCHAR/NVARCHAR (padrão)|  
    |cp866|Russo DOS|CHAR/VARCHAR (padrão)|  
    |keybcs2|DOS Kamenicky tcheco-eslovaco|CHAR/VARCHAR (padrão)|  
    |macce|Europeu Central do Mac|CHAR/VARCHAR (padrão)|  
    |MacRoman|Mac oeste Europeu|CHAR/VARCHAR (padrão)|  
    |cp852|Europeu Central DOS|CHAR/VARCHAR (padrão)|  
    |latin7|ISO 8859-13 báltico|CHAR/VARCHAR (padrão)|  
    |CP 1251|Windows cirílico|CHAR/VARCHAR (padrão)|  
    |CP 1256|Árabe do Windows|CHAR/VARCHAR (padrão)|  
    |CP 1257|Windows báltico|CHAR/VARCHAR (padrão)|  
    |BINARY|Conjunto de caracteres binária pseudo|CHAR/VARCHAR (padrão)|  
    |geostd8|Georgiano GEOSTD8|CHAR/VARCHAR (padrão)|  
    |cp932|SJIS em japonês do Windows|NCHAR/NVARCHAR (padrão)|  
    |eucjpms|UJIS para japonês do Windows|NCHAR/NVARCHAR (padrão)|  
  
2.  **No banco de dados, categoria ou níveis de nó de objeto:** no nível do banco de dados, categoria ou nós de objeto, charset mapeamento grade contém as mesmas linhas como no nível de nó raiz metadados viz.:  
  
    1.  A primeira coluna da grade intitulado **nome de conjunto de caracteres** contém o nome do conjunto de caracteres.  
  
    2.  A segunda coluna intitulada **caractere definir descrição** contém a descrição do conjunto de caracteres.  
  
    3.  A única diferença é que os valores na terceira coluna da grade. A terceira coluna intitulada **tipo de dados de destino** contém as configurações de mapeamento de conjunto de caracteres específica. Os valores da coluna são:  
  
        -   Herdado (CHAR/VARCHAR ou NCHAR/NVARCHAR)  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
> [!IMPORTANT]  
> -   No mapeamento de conjunto de caracteres entre o banco de dados MySQL e o banco de dados de destino no banco de dados, categorias e níveis de nó de objeto, os valores padrão para um determinado conjunto de caracteres em cada nível diferente de raiz para a coluna **tipo de dados de destino** deve ser 'herdada'.  
> -   Na grade, o valor **herdadas** é o sufixo com o '(CHAR/VARCHAR)' ou '(NCHAR/NVARCHAR)' dependendo de qual valor foi herdado do pai, esse conjunto de caracteres específico.  
  
