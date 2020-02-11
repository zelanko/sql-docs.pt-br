---
title: Implementação da compactação de linha | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- compression [SQL Server], row
- row compression [Database Engine]
ms.assetid: dcd97ac1-1c85-4142-9594-9182e62f6832
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 626ab7363a264b47d7c907c56c0e6c6d4d208dba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62873007"
---
# <a name="row-compression-implementation"></a>Implementação da compactação de linha
  Este tópico resume como o [!INCLUDE[ssDE](../../includes/ssde-md.md)] implementa a compactação de linha. Este resumo fornece informações básicas para ajudar no planejamento do espaço de armazenamento exigido pelos dados.  
  
 A habilitação da compactação altera somente o formato de armazenamento físico dos dados associados a um tipo de dados, mas não sua sintaxe ou semântica. Não são exigidas alterações de aplicativo quando uma ou mais tabelas são habilitadas para compactação. O novo formato de armazenamento de registros apresenta estas alterações principais:  
  
-   Reduz a sobrecarga de metadados associados ao registro. Esses metadados são informações sobre colunas, seus comprimentos e deslocamentos. Em alguns casos, a sobrecarga de metadados pode ser maior do que o formato de armazenamento antigo.  
  
-   Usa o formato de armazenamento de comprimento variável para tipos numéricos (por exemplo, `integer`, `decimal` e `float`) e os tipos baseados em números (por exemplo, `datetime` e `money`).  
  
-   Armazena cadeias de caracteres fixas usando o formato de comprimento variável ao não armazenar caracteres em branco.  
  
> [!NOTE]  
>  Valores NULL e 0 de todos os tipos de dados são otimizados e não ocupam bytes.  
  
## <a name="how-row-compression-affects-storage"></a>Como a compactação de linha afeta o armazenamento  
 A tabela a seguir descreve como a compactação de linha afeta os tipos existentes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A tabela não inclui o aumento que pode ser gerado usando a compactação de página.  
  
|Tipo de dados|O armazenamento é afetado?|DESCRIÇÃO|  
|---------------|--------------------------|-----------------|  
|`tinyint`|Não|1 byte é o armazenamento mínimo necessário.|  
|`smallint`|Sim|Se o valor couber em 1 byte, apenas 1 byte será usado.|  
|`int`|Sim|Usa apenas os bytes necessários. Por exemplo, se um valor puder ser armazenado em 1 byte, o armazenamento ocupará apenas 1 byte.|  
|`bigint`|Sim|Usa apenas os bytes necessários. Por exemplo, se um valor puder ser armazenado em 1 byte, o armazenamento ocupará apenas 1 byte.|  
|`decimal`|Sim|Esse armazenamento é exatamente igual ao do formato de armazenamento vardecimal.|  
|`numeric`|Sim|Esse armazenamento é exatamente igual ao do formato de armazenamento vardecimal.|  
|`bit`|Sim|A sobrecarga dos metadados atinge 4 bits.|  
|`smallmoney`|Sim|Usa a representação de dados de número inteiro usando um número inteiro de 4 bytes. Os valores monetários são multiplicados por 10000 e o valor inteiro resultante é armazenado removendo os dígitos após a casa decimal. Esse tipo tem uma otimização de armazenamento semelhante à empregada para tipos de número inteiro.|  
|`money`|Sim|Usa a representação de dados de número inteiro usando um número inteiro de 8 bytes. Os valores monetários são multiplicados por 10000 e o valor inteiro resultante é armazenado removendo os dígitos após a casa decimal. Esse tipo tem um intervalo maior que `smallmoney`. Esse tipo tem uma otimização de armazenamento semelhante à empregada para tipos de número inteiro.|  
|`float`|Sim|Bytes menos significantes com zeros não são armazenados. A compactação `float` é aplicável principalmente a valores não fracionários em mantissa.|  
|`real`|Sim|Bytes menos significantes com zeros não são armazenados. A compactação `real` é aplicável principalmente a valores não fracionários em mantissa.|  
|`smalldatetime`|Não|Usa a representação de dados de número inteiro usando números inteiros de 2 bytes. A data ocupa 2 bytes. É o número de dias desde 1/1/1901. São necessários 2 bytes a partir de 1902. Portanto, não há aumento a partir desse ponto.<br /><br /> A hora é o número de minutos a partir da meia-noite. Os valores de hora logo após 4h começam a usar o segundo byte.<br /><br /> Se um `smalldatetime` for usado apenas para representar uma data (o caso comum), a hora será 0.0. A compactação salva 2 bytes armazenando a hora em um formato de byte mais significativo para compactação de linha.|  
|`datetime`|Sim|Usa a representação de dados de número inteiro usando números inteiros de 4 bytes. O valor de inteiro representa o número de dias com data base de 1/1/1900. Os primeiros 2 bytes podem representar até o ano 2079. A compactação sempre pode salvar 2 bytes aqui até esse ponto. Cada valor de inteiro representa 3,33 milissegundos. A compactação esvazia os primeiros 2 bytes nos primeiros cinco minutos e precisa do quarto byte após às 16h. Portanto, a compactação pode salvar apenas 1 byte depois das 16h. Quando `datetime` é compactado como qualquer outro inteiro, a compactação salva 2 bytes na data.|  
|`date`|Não|Usa a representação de dados inteiros usando 3 bytes. Representa a data a partir de 1/1/0001. Para datas contemporâneas, a compactação de linha usa todos os 3 bytes. Não gera nenhum aumento.|  
|`time`|Não|Usa a representação de dados de inteiro usando de 3 a 6 bytes. Há várias precisões que começam com 0 a 9 que podem ocupar de 3 a 6 bytes. Observe que não há nenhuma alteração no armazenamento para a compactação de linha. De modo geral, não se pode esperar muito aumento da compactação do tipo de dados `time`. O espaço compactado é usado como segue:<br /><br /> Precisão = 0. Bytes = 3. Cada valor de inteiro representa um segundo. A compactação pode representar a hora até 16h usando 2 bytes, salvando potencialmente 1 byte.<br /><br /> Precisão = 1. Bytes = 3. Cada valor de inteiro representa 1/10 segundos. A compactação usa o terceiro byte antes das 2h. Resulta em um pequeno aumento.<br /><br /> Precisão = 2. Bytes = 3. Como no caso anterior, é improvável gerar aumento.<br /><br /> Precisão = 3. Bytes = 4. Como os primeiros 3 bytes são usados às 5h, gera pouco aumento.<br /><br /> Precisão = 4. Bytes = 4. Os primeiros 3 bytes são ocupados nos primeiros 27 segundos. Nenhum aumento é esperado.<br /><br /> Precisão = 5, Bytes = 5. O quinto byte será usado depois do meio-dia.<br /><br /> Precisão = 6 e 7, Bytes = 5. Não gera nenhum aumento.<br /><br /> Precisão = 8, Bytes = 6. O sexto byte será usado depois das 3h.|  
|`datetime2`|Sim|Usa a representação de dados de inteiro usando de 6 a 9 bytes. Os primeiros 4 bytes representam a data. Os bytes ocupados pela hora dependem da precisão da hora que é especificada.<br /><br /> O valor de inteiro representa o número de dias desde 1/1/0001 com um limite superior de 31/12/9999. Para representar uma data no ano 2005, a compactação utiliza 3 bytes.<br /><br /> Não há aumento de hora porque é permitido de 2 a 4 bytes para várias precisões de hora. Portanto, para precisão de um segundo, a compactação usa 2 bytes para a hora, que ocupa o segundo byte depois de 255 segundos.|  
|`datetimeoffset`|Sim|Semelhante a `datetime2`, exceto pelo fato de que há 2 bytes de fuso horário do formato (HH:MM).<br /><br /> Como `datetime2`, a compactação pode salvar 2 bytes.<br /><br /> Para valores de fuso horário, o valor MM pode ser 0 na maioria dos casos. Portanto, a compactação pode salvar possivelmente 1 byte.<br /><br /> Não há alteração alguma no armazenamento para compactação de linha.|  
|`char`|Sim|Caracteres de preenchimento à direita são removidos. Observe que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] insere o mesmo caractere de preenchimento, independentemente da ordenação usada.|  
|`varchar`|Não|Sem efeito.|  
|`text`|Não|Sem efeito.|  
|`nchar`|Sim|Caracteres de preenchimento à direita são removidos. Observe que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] insere o mesmo caractere de preenchimento, independentemente da ordenação usada.|  
|`nvarchar`|Não|Sem efeito.|  
|`ntext`|Não|Sem efeito.|  
|`binary`|Sim|Zeros à direita são removidos.|  
|`varbinary`|Não|Sem efeito.|  
|`image`|Não|Sem efeito.|  
|`cursor`|Não|Nenhum efeito.|  
|`timestamp` / `rowversion`|Sim|Usa a representação de dados inteiros com 8 bytes. Há um contador de carimbo de data/hora mantido para cada banco de dados e seu valor começa em 0. Ele pode ser compactado como qualquer outro valor de inteiro.|  
|`sql_variant`|Não|Sem efeito.|  
|`uniqueidentifier`|Não|Sem efeito.|  
|`table`|Não|Nenhum efeito.|  
|`xml`|Não|Sem efeito.|  
|Tipos definidos pelo usuário|Não|É representado internamente como `varbinary`.|  
|FILESTREAM|Não|É representado internamente como `varbinary`.|  
  
## <a name="see-also"></a>Consulte Também  
 [Compactação de dados](data-compression.md)   
 [Implementação da compactação de página](page-compression-implementation.md)  
  
  
