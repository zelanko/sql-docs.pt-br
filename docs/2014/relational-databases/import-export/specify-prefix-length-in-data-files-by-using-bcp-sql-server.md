---
title: Especificar o tamanho de prefixo em arquivos de dados usando bcp (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- bcp utility [SQL Server], prefix length
- prefix length [SQL Server]
- lengths [SQL Server], prefix characters
- data formats [SQL Server], prefix length
ms.assetid: ce32dd1a-26f1-4f61-b9fa-3f1feea9992e
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 338a19bca2f465d6af1b4f409d0563caeb71738f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020032"
---
# <a name="specify-prefix-length-in-data-files-by-using-bcp-sql-server"></a>Especificar o tamanho de prefixo em arquivos de dados usando bcp (SQL Server)
  Para fornecer o armazenamento de arquivos mais compacto para a exportação de dados em massa no formato nativo para um arquivo de dados, o comando **bcp** precede cada campo com um ou mais caracteres que indicam o comprimento do campo. Esses caracteres são chamados *caracteres de prefixo de comprimento*.  
  
## <a name="the-bcp-prompt-for-prefix-length"></a>O prompt bcp para tamanho de prefixo  
 Se um comando **bcp** interativo contiver a opção **in** ou **out** sem a opção do arquivo de formatos (**-f**) ou uma opção do formato de dados (**-n**, **-c**, **-w**ou **-N**), o comando solicitará o tamanho do prefixo de cada campo de dados, da seguinte maneira:  
  
 `Enter prefix length of field <field_name> [<default>]:`  
  
 Se você especificar 0, o **bcp** solicitará o tamanho do campo (para um tipo de dados de caractere) ou um terminador do campo (para um tipo de não caractere nativo).  
  
> [!NOTE]  
>  Depois que você especificar interativamente todos os campos em um comando **bcp**, o comando solicitará que salve suas respostas para cada campo em um arquivo de formato não XML. Para obter mais informações sobre arquivos de formato não XML, veja [Arquivos de formato não XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
## <a name="overview-of-prefix-length"></a>Visão geral de tamanho de prefixo  
 Para armazenar o comprimento do prefixo de um campo, você precisa de bytes suficientes para representar o comprimento máximo do campo. O número de bytes que também são necessários depende do tipo de armazenamento de arquivo, da nulidade de uma coluna e do fato de os dados serem armazenados no arquivo de dados em seu nativo ou no formato de caractere. Por exemplo, um `text` ou `image` tipo de dados requer quatro caracteres de prefixo para armazenar o comprimento do campo, mas um `varchar` tipo de dados requer dois caracteres. No arquivo de dados, estes caracteres de prefixo de comprimento são armazenados no formato de dados binário interno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Quando você usa formato nativo usa prefixos de comprimento em vez de terminadores de campo. Dados de formato nativo podem conflitar com terminadores porque um arquivo de dados de formato nativo é armazenado no formato de dados binário interno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="PrefixLengthsExport"></a> Comprimentos do prefixo para exportação em massa  
  
> [!NOTE]  
>  O valor padrão que é fornecido ao prompt de comprimento do prefixo quando você exporta um campo indica o comprimento do prefixo mais eficiente para o campo.  
  
 Valores nulos são representados como um campo vazio. Para indicar que o campo está vazio (representado por NULL), o prefixo de campo contém o valor -1; ou seja, ele necessita de pelo menos 1 byte. Note que se uma coluna da tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permitir valores nulos, a coluna necessitará um tamanho de prefixo 1 ou maior, dependendo do tipo de armazenamento de arquivo.  
  
 Quando você exportar dados em massa e armazená-los em tipos de dados nativos ou formato de caractere, use os comprimentos do prefixo mostrados na tabela a seguir.  
  
|SQL Server<br /><br /> tipo de dados|Formato nativo<br /><br /> NOT NULL|Formato nativo<br /><br /> NULL|Formato de caractere<br /><br /> NOT NULL|Formato de caractere<br /><br /> NULL|  
|------------------------------|--------------------------------|----------------------------|-----------------------------------|-------------------------------|  
|`char`|2|2|2|2|  
|`varchar`|2|2|2|2|  
|`nchar`|2|2|2|2|  
|`nvarchar`|2|2|2|2|  
|`text` <sup>1</sup>|4|4|4|4|  
|`ntext` <sup>1</sup>|4|4|4|4|  
|`binary`|2|2|2|2|  
|`varbinary`|2|2|2|2|  
|`image` <sup>1</sup>|4|4|4|4|  
|`datetime`|0|1|0|1|  
|`smalldatetime`|0|1|0|1|  
|`decimal`|1|1|1|1|  
|`numeric`|1|1|1|1|  
|`float`|0|1|0|1|  
|`real`|0|1|0|1|  
|`int`|0|1|0|1|  
|`bigint`|0|1|0|1|  
|`smallint`|0|1|0|1|  
|`tinyint`|0|1|0|1|  
|`money`|0|1|0|1|  
|`smallmoney`|0|1|0|1|  
|`bit`|0|1|0|1|  
|`uniqueidentifier`|1|1|0|1|  
|`timestamp`|1|1|1|1|  
|`varchar(max)`|8|8|8|8|  
|`varbinary(max)`|8|8|8|8|  
|UDT (um tipo de dados definido pelo usuário)|8|8|8|8|  
|XML|8|8|8|8|  
  
 <sup>1</sup> o `ntext`, `text`, e `image` tipos de dados serão removidos em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esses tipos de dados em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que os utilizam atualmente. Use `nvarchar(max)`, `varchar(max)`, e `varbinary(max)` em vez disso.  
  
##  <a name="PrefixLengthsImport"></a> Comprimentos do prefixo para importação em massa  
 Quando dados são importados em massa, o comprimento do prefixo é o valor que foi especificado quando o arquivo de dados foi criado originalmente. Se o arquivo de dados não foi criado por um comando **bcp** , os caracteres de prefixo do comprimento provavelmente não existirão. Nessa instância, especifique 0 para o comprimento do prefixo.  
  
> [!NOTE]  
>  Para especificar um tamanho do prefixo em um arquivo de dados que não foi criado usando o **bcp**, use os tamanhos fornecidos em [Tamanhos do Prefixo para a Exportação em Massa](#PrefixLengthsExport), anteriormente neste tópico.  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Especificar tamanho do campo usando bcp &#40;SQL Server&#41;](specify-field-length-by-using-bcp-sql-server.md)   
 [Especificar terminadores de campo e linha &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)   
 [Especificar tipo de armazenamento de arquivo usando bcp &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
  
