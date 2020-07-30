---
title: Mapeando MySQL e SQL Server conjunto de caracteres (MySQLToSQL) | Microsoft Docs
description: Saiba como especificar um conjunto de caracteres para tipos de dados de caractere MySQL, expressões e literais a serem usados durante a conversão do tipo de dados de caractere pelo SSMA para MySQL.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: d7fe937b95049788f4b488df2d36451df67c4c09
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396395"
---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>Mapear o conjunto de caracteres do SQL Server e MySQL (MySQLToSQL)
Conjunto de caracteres (charset) pode ser especificado para tipos de dados de caractere MySQL, expressões e literais.  
  
## <a name="charset-mapping"></a>Mapeamento de charset  
O mapeamento de conjunto de caracteres é definido para cada conjunto de caracteres MySQL e usado durante a conversão do tipo de dados de caractere. Ele especifica como converter tipos de dados de cadeia de caracteres de um determinado conjunto de caracteres:  
  
-   Para os tipos de caracteres SQL Server nacionais (NCHAR/NVARCHAR) ou  
  
-   Para SQL Server tipos de caracteres regulares (CHAR/VARCHAR)  
  
1.  os tipos de dados de caracteres de destino **nacional** são:  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  os tipos de dados de caractere **de destino de** banco de dado são:  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  O mapeamento de tipo só permite o mapeamento para tipos de dados de caractere **nacional** . Depois que o tipo de dados de caractere do MySQL é convertido de acordo com o mapeamento de tipo, o mapeamento de charset é aplicado.  
  
> [!NOTE]  
> O mapeamento de charset pode ser definido em cada nível de nó do explorador de objetos de metadados e representa todos os conjuntos de caracteres lidos do MySQL.  
  
## <a name="charset-mapping-on-different-node-levels"></a>Mapeamento de conjunto de caracteres em diferentes níveis de nó  
O mapeamento de conjunto de caracteres varia em níveis de nó diferentes, ou seja:  
  
1.  No nível do nó de metadados raiz  
  
2.  No nível de nó de banco de dados, categoria e objeto  
  
> [!NOTE]  
> A guia selecionada para editar o mapeamento de conjunto de caracteres contém três botões, independentemente do mapeamento nos diferentes níveis de nó.  
>   
> Eles são:  
>   
> 1.  **Aplicar:** Aplica as alterações feitas pelo usuário, habilitadas somente quando o mapeamento de conjunto de caracteres é editado e ainda não foi salvo.  
> 2.  **Cancelar:** Cancela as alterações feitas pelo usuário. O botão é habilitado quando o mapeamento de conjunto de caracteres é editado, mas não é salvo.  
> 3.  **Redefinir para o padrão:** Redefine todos os mapeamentos para valores padrão.  
  
1.  **No nível do nó de metadados raiz:**  A grade de mapeamento de charset contém a grade charset com uma coluna separada para cada conjunto de caracteres. As colunas da grade são:  
  
    1.  A primeira coluna da grade denominada **nome** do conjunto de caracteres contém o nome do conjunto de caracteres.  
  
    2.  A segunda descrição do conjunto de **caracteres** nomeado contém a descrição do conjunto de caracteres.  
  
    3.  A terceira coluna intitulada, tipo de conjunto de **caracteres de destino** contém configurações de mapeamento para um conjunto de caracteres específico. Os valores desta coluna são:  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
    > [!IMPORTANT]  
    > Os valores padrão para um conjunto de caracteres específico têm o prefixo ' (padrão) ' após CHAR/VARCHAR ou NCHAR/NVARCHAR.  
  
    O mapeamento charset entre o banco de dados MySQL e o banco de dados de destino no nível do nó de metadados raiz é fornecido abaixo:  
  
    |Nome do conjunto de caracteres|Descrição do conjunto de caracteres|Tipo de conjunto de caracteres de destino (padrão)|  
    |-|-|-|  
    |Big5|Chinês tradicional Big5|NCHAR/NVARCHAR (padrão)|  
    |dec8|Europa Ocidental|CHAR/VARCHAR (padrão)|  
    |cp850|DOS ocidental europeu|CHAR/VARCHAR (padrão)|  
    |hp8|Europa Ocidental HP|CHAR/VARCHAR (padrão)|  
    |koi8r|KOI8-R Relcom russo|CHAR/VARCHAR (padrão)|  
    |latino 1|Europa Ocidental cp1252|CHAR/VARCHAR (padrão)|  
    |latin2|ISO 8859-2 Europa Central|CHAR/VARCHAR (padrão)|  
    |swe7|7bit Sueco|CHAR/VARCHAR (padrão)|  
    |ascii|US-ASCII|CHAR/VARCHAR (padrão)|  
    |ujis|EUC-JP japonês|NCHAR/NVARCHAR (padrão)|  
    |sjis|Shift-JIS japonês|NCHAR/NVARCHAR (padrão)|  
    |Hebraico|ISO 8859-8 Hebraico|CHAR/VARCHAR (padrão)|  
    |tis620|TIS620 tailandês|CHAR/VARCHAR (padrão)|  
    |euckr|EUC-KR coreano|NCHAR/NVARCHAR (padrão)|  
    |koi8u|KOI8-U ucraniano|CHAR/VARCHAR (padrão)|  
    |GB2312|GB2312 chinês simplificado|NCHAR/NVARCHAR (padrão)|  
    |grego|ISO 8859-7 Grego|CHAR/VARCHAR (padrão)|  
    |CP 1250|Europa Central do Windows|CHAR/VARCHAR (padrão)|  
    |simplificado GBK|Chinês simplificado do simplificado GBK|NCHAR/NVARCHAR (padrão)|  
    |latin5|ISO 8859-9 Turco|CHAR/VARCHAR (padrão)|  
    |armscii8|ARMSCII-8 armênio|CHAR/VARCHAR (padrão)|  
    |utf8|Unicode UTF-8|NCHAR/NVARCHAR (padrão)|  
    |ucs2|UCS-2 Unicode|NCHAR/NVARCHAR (padrão)|  
    |cp866|DOS russo|CHAR/VARCHAR (padrão)|  
    |keybcs2|DOS Kamenicky tcheco-eslovaco|CHAR/VARCHAR (padrão)|  
    |macce|Centro-Europeu Central|CHAR/VARCHAR (padrão)|  
    |mácron|Europa ocidental do Mac|CHAR/VARCHAR (padrão)|  
    |cp852|Centro-Europeu Central|CHAR/VARCHAR (padrão)|  
    |latin7|Báltico ISO 8859-13|CHAR/VARCHAR (padrão)|  
    |CP 1251|Windows cirílico|CHAR/VARCHAR (padrão)|  
    |CP 1256|Árabe do Windows|CHAR/VARCHAR (padrão)|  
    |CP 1257|Báltico do Windows|CHAR/VARCHAR (padrão)|  
    |binary|Pseudo-conjunto de caracteres binário|CHAR/VARCHAR (padrão)|  
    |geostd8|GEOSTD8 georgiano|CHAR/VARCHAR (padrão)|  
    |cp932|SJIS para Windows japonês|NCHAR/NVARCHAR (padrão)|  
    |eucjpms|UJIS para Windows japonês|NCHAR/NVARCHAR (padrão)|  
  
2.  **Nos níveis de banco de dados, categoria ou nó de objeto:** No nível de nó de banco de dados, categoria ou objeto, a grade de mapeamento de conjunto de caracteres contém as mesmas linhas que o no nível dos nós de metadados raiz, aula sobre visualização.:  
  
    1.  A primeira coluna da grade chamada, nome do **conjunto de caracteres** , contém o nome do charset.  
  
    2.  A segunda coluna intitulada, a **Descrição do conjunto de caracteres** contém a descrição do charset.  
  
    3.  A única diferença são os valores na terceira coluna da grade. A terceira coluna intitulada, **tipo de dados de destino** contém configurações de mapeamento para um conjunto de caracteres específico. Os valores para a coluna são:  
  
        -   Inherited (CHAR/VARCHAR ou NCHAR/NVARCHAR)  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
> [!IMPORTANT]  
> -   No mapeamento de conjunto de caracteres entre o banco de dados MySQL e o banco de dados de destino nos níveis de banco de dados, categoria e nó de objeto, os valores padrão para um conjunto de caracteres específico em cada nível diferente da raiz para o **tipo de dados de destino** da coluna devem ser ' Inherited '.  
> -   Na grade, o valor **herdado** é sufixado com ' (char/varchar) ' ou ' (nchar/nvarchar) ', dependendo de qual valor foi herdado do pai por esse conjunto de caracteres específico.  
  
