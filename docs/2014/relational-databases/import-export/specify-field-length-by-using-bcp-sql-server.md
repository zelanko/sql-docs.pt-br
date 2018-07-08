---
title: Especificar tamanho do campo usando bcp (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- native data format [SQL Server]
- default field lengths
- field length [SQL Server]
- data formats [SQL Server], field length
- bcp utility [SQL Server], field length
ms.assetid: 240f33ca-ef4a-413a-a4de-831885cb505b
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a3d4be0ba5a6b24174134fbef6f5dc2e87fa3af9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37158567"
---
# <a name="specify-field-length-by-using-bcp-sql-server"></a>Especificar tamanho do campo usando bcp (SQL Server)
  O tamanho do campo indica o número máximo de caracteres que são exigidos para representar dados em formato de caractere. O tamanho do campo já será conhecido se os dados forem armazenados no formato nativo; por exemplo, o tipo de dados `int` usa 4 bytes. Se você indicou 0 para o comprimento do prefixo, o **bcp** comando solicitará o comprimento de campo, os tamanhos de campo padrão e o impacto do tamanho do campo no armazenamento de dados em arquivos de dados que contêm `char` dados.  
  
## <a name="the-bcp-prompt-for-field-length"></a>O bcp solicita um tamanho de campo  
 Se um comando **bcp** interativo contiver a opção **in** ou **out** sem a opção do arquivo de formatos (**-f**) ou uma opção do formato de dados (**-n**, **-c**, **-w** ou **-N**), o comando solicitará o comprimento de campo de cada campo de dados, da seguinte maneira:  
  
 `Enter length of field <field_name> [<default>]:`  
  
 Para obter um exemplo que mostra esse prompt no contexto, veja [Especificar formatos de dados para compatibilidade usando bcp &#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
> [!NOTE]  
>  Depois que você especificar interativamente todos os campos em um comando **bcp**, o comando solicitará que salve suas respostas para cada campo em um arquivo de formato não XML. Para obter mais informações sobre arquivos de formato não XML, veja [Arquivos de formato não XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
 A solicitação do comprimento do campo pelo comando **bcp** depende de vários fatores:  
  
-   Quando você copiar tipos de dados que não são de comprimento fixo e especificar um comprimento de prefixo 0, o **bcp** solicitará um comprimento de campo.  
  
-   Quando dados que não contêm caracteres são convertidos em dados de caracteres, o **bcp** sugere um comprimento de campo padrão grande o suficiente para armazenar os dados.  
  
-   Se o tipo de armazenamento de arquivos for não caractere, o comando **bcp** não solicitará um comprimento de campo. Os dados são armazenados no formato de representação de dados nativo (formato nativo) do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="using-default-field-lengths"></a>Usando tamanhos de campo padrão  
 Geralmente, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você aceite os valores padrão sugeridos pelo **bcp**para o comprimento de campo. Quando um arquivo de dados de modo de caractere é criado, usar o tamanho do campo padrão assegura que os dados não serão truncados e que não ocorram erros de estouro numéricos.  
  
 Se você especificar um tamanho do campo incorreto, poderão ocorrer problemas. Por exemplo, se você copiar dados numéricos e especificar um tamanho do campo muito curto para obter os dados, o utilitário do **bcp** imprimirá uma mensagem de estouro e não copiará os dados. Além disso, se você exportar `datetime` dados e especificar um tamanho do campo menor que 26 bytes para a cadeia de caracteres, o **bcp** utilitário truncará os dados sem uma mensagem de erro.  
  
> [!IMPORTANT]  
>  Quando a opção de tamanho padrão é usada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espera ler uma cadeia de caracteres inteira. Em algumas situações, o uso de um tamanho do campo padrão pode conduzir a um erro "fim de arquivo inesperado". Normalmente, esse erro ocorre com o `money` e `datetime` tipos de dados quando apenas parte do campo esperado ocorre no arquivo de dados; por exemplo, quando um `datetime` valor de *mm*/*dd*  / *yy* é especificado sem o componente de tempo e é, portanto, menor do que o esperado 24 caracteres de comprimento de um `datetime` valor em `char` formato. Para evitar esse tipo de erro, use terminadores de campos ou campos de dados de comprimento fixo ou altere o tamanho do campo padrão especificando outro valor.  
  
### <a name="default-field-lengths-for-character-file-storage"></a>Tamanhos do campo padrão para armazenamento de arquivo de caractere  
 A tabela a seguir lista os tamanhos dos campos padrão para obter os dados a serem armazenados como armazenamento de arquivo de caractere. Dados anuláveis são do mesmo comprimento que dados de não anuláveis.  
  
|Tipo de dados|Comprimento padrão (caracteres)|  
|---------------|-----------------------------------|  
|`char`|Comprimento definido para a coluna|  
|`varchar`|Comprimento definido para a coluna|  
|`nchar`|Duas vezes o comprimento definido para a coluna|  
|`nvarchar`|Duas vezes o comprimento definido para a coluna|  
|`Text`|0|  
|`ntext`|0|  
|`bit`|1|  
|`binary`|Duas vezes o comprimento definido para a coluna + 1|  
|`varbinary`|Duas vezes o comprimento definido para a coluna + 1|  
|`image`|0|  
|`datetime`|24|  
|`smalldatetime`|24|  
|`float`|30|  
|`real`|30|  
|`int`|12|  
|`bigint`|19|  
|`smallint`|7|  
|`tinyint`|5|  
|`money`|30|  
|`smallmoney`|30|  
|`decimal`|41*|  
|`numeric`|41*|  
|`uniqueidentifier`|37|  
|`timestamp`|17|  
|`varchar(max)`|0|  
|`varbinary(max)`|0|  
|`nvarchar(max)`|0|  
|UDT|Comprimento da coluna UDT (termo definido pelo usuário)|  
|XML|0|  
  
 \*Para obter mais informações sobre o `decimal` e `numeric` tipos de dados, consulte [decimais e numéricos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/decimal-and-numeric-transact-sql).  
  
> [!NOTE]  
>  Uma coluna do tipo `tinyint` pode ter valores de 0 a 255; o número de máximo de caracteres necessários para representar qualquer número naquele intervalo é três (representando valores de 100 a 255).  
  
### <a name="default-field-lengths-for-native-file-storage"></a>Tamanhos do campo padrão para armazenamento de arquivo nativo  
 A tabela seguinte lista os tamanhos dos campos padrão para os dados a serem armazenados como um tipo de armazenamento de arquivo nativo. Dados anuláveis são do mesmo comprimento que dados de não anuláveis e os dados de caractere sempre são armazenados em formato de caractere.  
  
|Tipo de dados|Comprimento padrão (caracteres)|  
|---------------|-----------------------------------|  
|`bit`|1|  
|`binary`|Comprimento definido para a coluna|  
|`varbinary`|Comprimento definido para a coluna|  
|`image`|0|  
|`datetime`|8|  
|`smalldatetime`|4|  
|`float`|8|  
|`real`|4|  
|`int`|4|  
|`bigint`|8|  
|`smallint`|2|  
|`tinyint`|1|  
|`money`|8|  
|`smallmoney`|4|  
|`decimal` <sup>1</sup>|<sup>*</sup>|  
|`numeric` <sup>1</sup>|<sup>*</sup>|  
|`uniqueidentifier`|16|  
|`timestamp`|8|  
  
 <sup>1</sup> para obter mais informações sobre a `decimal` e `numeric` tipos de dados, consulte [decimal e numeric &#40;Transact-SQL&#41;](/sql/t-sql/data-types/decimal-and-numeric-transact-sql).  
  
 Em todos os casos anteriores, para criar um arquivo de dados para recarregar posteriormente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que mantenha o espaço de armazenamento em um mínimo, use um prefixo de comprimento com o tipo de armazenamento de arquivo padrão e o tamanho do campo padrão.  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Especificar terminadores de campo e linha &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)   
 [Especificar o tamanho de prefixo em arquivos de dados usando bcp &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)   
 [Especificar tipo de armazenamento de arquivo usando bcp &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)   
 [Manter valores nulos ou use os valores padrão durante a importação em massa &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
  
