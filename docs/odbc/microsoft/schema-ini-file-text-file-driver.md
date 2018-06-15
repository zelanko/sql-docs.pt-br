---
title: Arquivo Schema (Driver de arquivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- schema.ini file [ODBC]
- text file driver [ODBC], schema.ini file
ms.assetid: 0c4625c4-c730-4984-b430-9051b7bc0451
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 604dccbbb139cd72f8952fdd604a55d1d9af11c6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32904581"
---
# <a name="schemaini-file-text-file-driver"></a>Arquivo Schema (Driver de arquivo de texto)
Quando o driver de texto é usado, o formato do arquivo de texto é determinado por meio de um arquivo de informações de esquema. O arquivo de informações de esquema é sempre chamado Schema e sempre é mantido no mesmo diretório como a fonte de dados de texto. O arquivo de informações de esquema fornece IISAM com informações sobre o formato geral do arquivo, o nome da coluna e informações de tipo de dados e várias outras características de dados. Um arquivo Schema.ini é sempre necessário para acessar dados de comprimento fixo. Você deve usar um arquivo Schema quando sua tabela de texto contém a data e hora, moeda, ou dados decimais ou sempre que quiser mais controle sobre a manipulação de dados na tabela.  
  
> [!NOTE]  
>  O texto ISAM obterá valores iniciais do registro, não de Schema. O mesmo formato de arquivo padrão se aplica a todas as novas tabelas de dados de texto. Todos os arquivos que foram criados pela instrução CREATE TABLE herdam os mesmos valores de formato padrão, que são definidos, selecionando valores de formato de arquivo no **definir formato de texto** caixa de diálogo com \<padrão > escolhido no  **Tabelas** lista. Se os valores do registro são diferentes dos valores no Schema, os valores do registro serão substituídos pelos valores de Schema.  
  
## <a name="understanding-schemaini-files"></a>Noções básicas sobre arquivos de Schema  
 Arquivos Schema fornecem informações de esquema sobre os registros em um arquivo de texto. Cada entrada Schema Especifica um dos cinco características da tabela:  
  
-   O nome do arquivo de texto  
  
-   O formato de arquivo  
  
-   Os nomes de campo, larguras e tipos  
  
-   O conjunto de caracteres  
  
-   Conversões de tipo de dados especiais  
  
 As seções a seguir discutem essas características.  
  
## <a name="specifying-the-file-name"></a>Especificando o nome do arquivo  
 A primeira entrada na Schema sempre é o nome do arquivo de origem de texto entre colchetes. O exemplo a seguir ilustra a entrada para o arquivo txt:  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>Especificar o formato de arquivo  
 O **formato** opção Schema Especifica o formato do arquivo de texto. O texto IISAM pode ler o formato automaticamente de arquivos mais delimitados por caracteres. Você pode usar qualquer caractere único como um delimitador de arquivo, exceto as aspas duplas ("). O **formato** no Schema substituirá a configuração no registro do Windows, o arquivo por arquivo. A tabela a seguir lista os valores válidos para o **formato** opção.  
  
|Especificador de formato|Formato de tabela|Instrução de formato Schema|  
|----------------------|------------------|---------------------------------|  
|**Delimitado por tabulação**|Campos no arquivo são delimitados por tabulações.|Formato = TabDelimited|  
|**CSV delimitado**|Campos no arquivo são delimitados por vírgulas (CSV).|Formato = CSVDelimited|  
|**Personalizar delimitado**|Campos no arquivo são delimitados por qualquer caractere que você escolher a entrada na caixa de diálogo. Tudo, exceto as aspas duplas (") são permitidos, incluindo em branco.|Formato = delimitado (*caractere personalizado*)<br /><br /> -ou-<br /><br /> Com nenhum delimitador especificado:<br /><br /> Formato = delimitado (.)|  
|**Comprimento fixo**|Campos no arquivo são de comprimento fixo.|Formato = FixedLength|  
  
## <a name="specifying-the-fields"></a>Especifica os campos  
 Você pode especificar nomes de campo em um arquivo de texto separado por caracteres de duas maneiras:  
  
-   Incluir nomes de campo na primeira linha da tabela e defina **ColNameHeader** para **True.**  
  
-   Especifique cada coluna de número e designar o coluna Nome e tipo de dados.  
  
 Você deve especificar cada coluna de número e designar o nome da coluna, tipo de dados e largura para arquivos de comprimento fixo.  
  
> [!NOTE]  
>  O **ColNameHeader** configuração nas substituições Schema o **FirstRowHasNames** configuração no registro do Windows, o arquivo por arquivo.  
  
 Os tipos de dados dos campos também podem ser determinados. Use o **MaxScanRows** opção para indicar quantas linhas devem ser verificadas para determinar os tipos de coluna. Se você definir **MaxScanRows** como 0, o arquivo inteiro será examinado. O **MaxScanRows** no Schema substituirá a configuração no registro do Windows, o arquivo por arquivo.  
  
 A seguinte entrada indica que o Microsoft Jet deve usar os dados na primeira linha da tabela para determinar os nomes de campo e deve examinar todo o arquivo para determinar os dados de tipos usados:  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 A próxima entrada designa os campos em uma tabela usando o número da coluna (**Col * n*) opção, que é necessário para arquivos de comprimento fixo e opcional para arquivos delimitados por caracteres. O exemplo mostra as entradas Schema para dois campos, um campo de texto CustomerNumber 10 caracteres e um campo de texto CustomerName 30 caracteres:  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 A sintaxe de **Col * n* é:  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>Remarks  
 A tabela a seguir descreve cada parte do **Col * n* entrada.  
  
|Parâmetro|Description|  
|---------------|-----------------|  
|*ColumnName*|O nome do texto da coluna. Se o nome de coluna contiver espaços, você deve colocá-la entre aspas duplas.|  
|*type*|Tipos de dados são os seguintes:<br /><br /> **Tipos de dados do Microsoft Jet**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> Longo<br /><br /> Moeda<br /><br /> Single<br /><br /> Double<br /><br /> DateTime<br /><br /> Texto<br /><br /> Memorando<br /><br /> **Tipos de dados ODBC** Char (o mesmo como texto)<br /><br /> Float (o mesmo que Double)<br /><br /> Inteiro (o mesmo que Short)<br /><br /> LongChar (mesmo memorando)<br /><br /> Data *formato de data*|  
|**Largura**|O valor de cadeia de caracteres literal `Width`. Indica que o seguinte número designa a largura da coluna (opcional para arquivos delimitados por caracteres; necessário para arquivos de comprimento fixo).|  
|*#*|O valor inteiro que designa a largura da coluna (obrigatório se **largura** for especificado).|  
  
## <a name="selecting-a-character-set"></a>Selecionar um conjunto de caracteres  
 Você pode selecionar dois conjuntos de caracteres: ANSI e OEM. O **CharacterSet** no Schema substituirá a configuração no registro do Windows, o arquivo por arquivo. O exemplo a seguir mostra a entrada de Schema que define o conjunto de caracteres para ANSI:  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>Especificar formatos de tipo de dados e conversões  
 O arquivo Schema contém várias opções que você pode usar para especificar como os dados são convertidos ou exibidos. A tabela a seguir lista cada uma dessas opções.  
  
|Opção|Description|  
|------------|-----------------|  
|**DateTimeFormat**|Pode ser definido como uma cadeia de caracteres de formato que indica as datas e horas. Se todos os campos de data/hora em que a importação/exportação são tratados com o mesmo formato, você deve especificar essa entrada. Todos os formatos do Microsoft Jet exceto A.M. e. há suporte. Se não houver nenhuma cadeia de caracteres de formato, as opções de imagem e a hora de data abreviada do painel de controle do Windows são usadas.|  
|**DecimalSymbol**|Pode ser definido como qualquer caractere único que é usado para separar o inteiro da parte fracionária de um número.|  
|**NumberDigits**|Indica o número de dígitos decimais da parte fracionária de um número.|  
|**NumberLeadingZeros**|Especifica se um valor decimal menor que 1 e mais de – 1 deve conter zeros à esquerda; Esse valor pode ser False (sem zeros à esquerda) ou True.|  
|**CurrencySymbol**|Indica o símbolo de moeda que pode ser usado para valores de moeda no arquivo de texto. Exemplos incluem o sinal de cifrão ($) e Dm.|  
|**CurrencyPosFormat**|Pode ser definida para qualquer um dos seguintes valores:<br /><br /> -Prefixo do símbolo da moeda sem separação ($1)<br />-Sufixo do símbolo da moeda sem separação (1$)<br />-Prefixo do símbolo da moeda com uma separação de caractere ($ 1)<br />-Sufixo do símbolo da moeda com uma separação de caractere (1 $)|  
|**CurrencyDigits**|Especifica o número de dígitos usados para a parte fracionária de um valor de moeda.|  
|**CurrencyNegFormat**|Pode ser um dos seguintes valores:<br /><br /> -   ($1)<br />-   –$1<br />-   $–1<br />-   $1–<br />-   (1$)<br />-   –1$<br />-   1–$<br />-   1$–<br />-   –1 $<br />-   –$ 1<br />-   1 $–<br />-   $ 1–<br />-   $ –1<br />-   1– $<br />-   ($ 1)<br />-   (1 $)<br /><br /> Este exemplo mostra o símbolo de dólar, mas você deve substituí-lo com as **CurrencySymbol** valor no programa.|  
|**CurrencyThousandSymbol**|Indica o símbolo de caractere único que pode ser usado para separar os valores de moeda no arquivo de texto por milhares.|  
|**CurrencyDecimalSymbol**|Pode ser definido como qualquer caractere único que é usado para separar toda a parte fracionária de um valor de moeda.|  
  
> [!NOTE]  
>  Se você omitir uma entrada, o valor padrão no painel de controle do Windows será usado.
