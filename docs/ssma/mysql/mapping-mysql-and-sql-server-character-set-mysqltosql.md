---
title: Mapeamento de caracteres do SQL Server e MySQL definida (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: cebdf2ed28287a59ec9d4f0daaa1d0c200f8fe20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312367"
---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>Mapear o conjunto de caracteres do SQL Server e MySQL (MySQLToSQL)
O conjunto de caracteres (Charset) pode ser especificado para tipos de dados de caractere do MySQL, expressões e literais.  
  
## <a name="charset-mapping"></a>Mapeamento de conjunto de caracteres  
Mapeamento de conjunto de caracteres é definido para cada conjunto de caracteres do MySQL e usado durante a conversão de tipo de dados de caractere. Especifica como converter tipos de dados de cadeia de caracteres de um conjunto de caracteres em particular:  
  
-   Para tipos de caracteres nacionais do SQL Server (NCHAR/NVARCHAR), ou  
  
-   Para tipos de caracteres regulares do SQL Server (CHAR/VARCHAR)  
  
1.  **National** são tipos de dados de caracteres de banco de dados de destino:  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  **regular** são tipos de dados de caracteres de banco de dados de destino:  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  Mapeamento de tipo só permite o mapeamento para **national** tipos de dados de caractere. Depois que o tipo de dados de caractere do MySQL é convertido de acordo com o mapeamento de tipo, o mapeamento de conjunto de caracteres é aplicado.  
  
> [!NOTE]  
> Mapeamento de conjunto de caracteres podem ser definidas em cada nível de nó do Pesquisador de objetos de metadados e representam todos os conjuntos de caracteres lidos do MySQL.  
  
## <a name="charset-mapping-on-different-node-levels"></a>Mapeamento de conjunto de caracteres em diferentes níveis de nó  
Mapeamento de conjunto de caracteres varia em diferentes níveis de nó, ou seja:  
  
1.  No nível de nó de metadados da raiz  
  
2.  No banco de dados, categoria e nível de nó de objeto  
  
> [!NOTE]  
> A guia selecionada para edição o mapeamento de conjunto de caracteres, contém três botões, independentemente do mapeamento nos níveis de nó diferente.  
>   
> São eles:  
>   
> 1.  **Apply:** Aplica as alterações feitas pelo usuário, habilitado apenas quando o mapeamento de conjunto de caracteres é editado e ainda não foi salvo.  
> 2.  **Cancelar:** Cancela as alterações feitas pelo usuário. O botão é habilitado quando o mapeamento de conjunto de caracteres é editado, mas não salvo.  
> 3.  **Redefinir para padrão:** Redefine todos os mapeamentos para os valores padrão.  
  
1.  **No nível de nó de metadados da raiz:**  Grade de mapeamento de conjunto de caracteres contém a grade de conjunto de caracteres com uma coluna separada para cada conjunto de caracteres. As colunas da grade são:  
  
    1.  A primeira coluna da grade chamado **nome do conjunto de caracteres** contém o nome do conjunto de caracteres.  
  
    2.  O segundo é denominado **descrição do conjunto de caracteres** contém a descrição do conjunto de caracteres.  
  
    3.  A terceira coluna intitulada **tipo de conjunto de caracteres de destino** contém as configurações de mapeamento para determinado conjunto de caracteres. Os valores desta coluna são:  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
    > [!IMPORTANT]  
    > Os valores padrão para um determinado conjunto de caracteres têm o prefixo '(padrão)' após CHAR/VARCHAR ou NCHAR/NVARCHAR.  
  
    O mapeamento de conjunto de caracteres entre o banco de dados MySQL e o banco de dados de destino no nível de nó de metadados raiz é fornecido abaixo:  
  
    ||||  
    |-|-|-|  
    |**Nome do conjunto de caracteres**|**Descrição do conjunto de caracteres**|**Tipo de conjunto de caracteres de destino (padrão)**|  
    |Big5|Chinês tradicional de Big5|NCHAR/NVARCHAR (padrão)|  
    |dec8|DEC oeste Europeu|CHAR/VARCHAR (padrão)|  
    |cp850|DOS oeste Europeu|CHAR/VARCHAR (padrão)|  
    |hp8|HP West European|CHAR/VARCHAR (padrão)|  
    |koi8r|KOI8-R Relcom russo|CHAR/VARCHAR (padrão)|  
    |Latino 1|cp1252 West European|CHAR/VARCHAR (padrão)|  
    |latin2|ISO 8859-2 Central European|CHAR/VARCHAR (padrão)|  
    |swe7|7 bits sueco|CHAR/VARCHAR (padrão)|  
    |ascii|US ASCII|CHAR/VARCHAR (padrão)|  
    |ujis|Japonês EUC-JP|NCHAR/NVARCHAR (padrão)|  
    |sjis|Japonês Shift-JIS|NCHAR/NVARCHAR (padrão)|  
    |Hebraico|ISO 8859-8 Hebraico|CHAR/VARCHAR (padrão)|  
    |tis620|TIS620 Thai|CHAR/VARCHAR (padrão)|  
    |euckr|Coreano Coreia EUC|NCHAR/NVARCHAR (padrão)|  
    |koi8u|Ucraniano KOI8-U|CHAR/VARCHAR (padrão)|  
    |gb2312|GB2312 Chinês simplificado|NCHAR/NVARCHAR (padrão)|  
    |Grego|ISO 8859-7 Grego|CHAR/VARCHAR (padrão)|  
    |cp 1250|Europeu Central do Windows|CHAR/VARCHAR (padrão)|  
    |gbk|E chinês simplificado GBK|NCHAR/NVARCHAR (padrão)|  
    |latin5|ISO 8859-9 Turco|CHAR/VARCHAR (padrão)|  
    |armscii8|Armênio ARMSCII-8|CHAR/VARCHAR (padrão)|  
    |utf8|Unicode UTF-8|NCHAR/NVARCHAR (padrão)|  
    |ucs2|Unicode UCS-2|NCHAR/NVARCHAR (padrão)|  
    |cp866|Russo DOS|CHAR/VARCHAR (padrão)|  
    |keybcs2|DOS Kamenicky Czech-Slovak|CHAR/VARCHAR (padrão)|  
    |macce|Europeu Central do Mac|CHAR/VARCHAR (padrão)|  
    |MacRoman|Mac oeste Europeu|CHAR/VARCHAR (padrão)|  
    |cp852|Europeu Central DOS|CHAR/VARCHAR (padrão)|  
    |latin7|ISO 8859-13 Baltic|CHAR/VARCHAR (padrão)|  
    |cp 1251|Windows cirílico|CHAR/VARCHAR (padrão)|  
    |cp 1256|Árabe do Windows|CHAR/VARCHAR (padrão)|  
    |cp 1257|Windows báltico|CHAR/VARCHAR (padrão)|  
    |binary|Binary pseudo charset|CHAR/VARCHAR (padrão)|  
    |geostd8|Georgiano GEOSTD8|CHAR/VARCHAR (padrão)|  
    |cp932|SJIS para japonês do Windows|NCHAR/NVARCHAR (padrão)|  
    |eucjpms|UJIS para japonês do Windows|NCHAR/NVARCHAR (padrão)|  
  
2.  **No banco de dados, categoria ou níveis de nó de objeto:** No nível de banco de dados, categoria ou nós de objeto, grade de mapeamento de conjunto de caracteres contém as mesmas linhas como um no nível do nó de metadados de raiz, sobre visualização.:  
  
    1.  A primeira coluna da grade intitulada **nome do conjunto de caracteres** contém o nome do conjunto de caracteres.  
  
    2.  A segunda coluna intitulada **caractere definir descrição** contém a descrição do conjunto de caracteres.  
  
    3.  A única diferença é que os valores na terceira coluna da grade. A terceira coluna intitulada **tipo de dados de destino** contém as configurações de mapeamento para determinado conjunto de caracteres. Os valores da coluna são:  
  
        -   Herdado (CHAR/VARCHAR ou NCHAR/NVARCHAR)  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
> [!IMPORTANT]  
> -   No mapeamento de conjunto de caracteres entre o banco de dados MySQL e banco de dados de destino no banco de dados, categoria e níveis de nó de objeto, os valores padrão para um determinado conjunto de caracteres em cada nível que não seja a raiz para a coluna **tipo de dados de destino** deve ser ' Herdado '.  
> -   Na grade, o valor **Inherited** é sufixado com qualquer um '(CHAR/VARCHAR)' ou '(NCHAR/NVARCHAR)', dependendo de qual valor estava herdado do pai, esse conjunto de caracteres específico.  
  
