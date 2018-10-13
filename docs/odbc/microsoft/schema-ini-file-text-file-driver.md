---
title: Arquivo Schema ini (Driver de arquivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- schema.ini file [ODBC]
- text file driver [ODBC], schema.ini file
ms.assetid: 0c4625c4-c730-4984-b430-9051b7bc0451
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8afb8b22ae2c6563641491b3bfe4289aa86e73e2
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49169216"
---
# <a name="schemaini-file-text-file-driver"></a>Schema.ini File (Driver de Arquivo de texto)
Quando o driver de texto é usado, o formato do arquivo de texto é determinado por meio de um arquivo de informações de esquema. O arquivo de informações de esquema é sempre chamado Schema. ini e sempre é mantido no mesmo diretório que a fonte de dados de texto. O arquivo de informações de esquema fornece o IISAM com informações sobre o formato geral do arquivo, o nome da coluna e informações de tipo de dados e várias outras características de dados. Um arquivo Schema sempre é necessário para acessar dados de comprimento fixo. Você deve usar um arquivo Schema quando sua tabela de texto contém a data e hora, moeda, ou dados Decimal ou a qualquer momento que você quiser mais controle sobre a manipulação dos dados na tabela.  
  
> [!NOTE]  
>  O texto ISAM obterá valores iniciais do registro, não de Schema. ini. O mesmo formato de arquivo padrão se aplica a todas as novas tabelas de dados de texto. Todos os arquivos que foram criados pela instrução CREATE TABLE herdam esses mesmos valores de formato padrão, que são definidos, selecionando valores de formato de arquivo na **definir o formato de texto** caixa de diálogo com \<padrão > escolhido no  **Tabelas** lista. Se os valores no registro diferem dos valores no Schema. ini, os valores no registro serão substituídos pelos valores de Schema. ini.  
  
## <a name="understanding-schemaini-files"></a>Noções básicas sobre arquivos Schema. ini  
 Arquivos INI fornecem informações de esquema sobre os registros em um arquivo de texto. Cada entrada de Schema. ini especifica um dos cinco características da tabela:  
  
-   O nome do arquivo de texto  
  
-   O formato de arquivo  
  
-   Os nomes de campo, as larguras e tipos  
  
-   O conjunto de caracteres  
  
-   Conversões de tipo de dados especiais  
  
 As seções a seguir discutem essas características.  
  
## <a name="specifying-the-file-name"></a>Especificando o nome do arquivo  
 A primeira entrada no Schema. ini é sempre o nome do arquivo de origem de texto entre colchetes. O exemplo a seguir ilustra a entrada para o arquivo de exemplo. txt:  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>Especificando o formato de arquivo  
 O **formato** opção no Schema. ini especifica o formato do arquivo de texto. O texto IISAM pode ler o formato automaticamente de arquivos mais delimitados por caracteres. Você pode usar qualquer caractere único como um delimitador no arquivo, exceto a marca de aspas duplas ("). O **formato** no Schema. ini substituirá a configuração no registro do Windows, o arquivo por arquivo. A tabela a seguir lista os valores válidos para o **formato** opção.  
  
|Especificador de formato|Formato de tabela|Instrução de formato Schema. ini|  
|----------------------|------------------|---------------------------------|  
|**Delimitado por tabulação**|Campos no arquivo são delimitados por guias.|Formato = TabDelimited|  
|**Delimitado por vírgula**|Campos no arquivo são delimitados por vírgulas (valores separados por vírgula).|Formato = CSVDelimited|  
|**Personalizado**|Campos no arquivo são delimitados por qualquer caractere que você optar por inserir na caixa de diálogo. Todos, exceto as aspas duplas (") são permitidos, incluindo em branco.|Formato = delimitado (*caractere personalizado*)<br /><br /> -ou-<br /><br /> Com nenhum delimitador especificado:<br /><br /> Formato = delimitado (.)|  
|**Comprimento fixo**|Campos no arquivo são de comprimento fixo.|Formato = FixedLength|  
  
## <a name="specifying-the-fields"></a>Especifica os campos  
 Você pode especificar nomes de campo em um arquivo de texto delimitado por caracteres de duas maneiras:  
  
-   Inclua os nomes de campo na primeira linha da tabela e defina **ColNameHeader** para **True.**  
  
-   Especifique cada coluna por número e designar o tipo de dados e o nome de coluna.  
  
 Você deve especificar cada coluna por número e designar o nome da coluna, tipo de dados e largura para arquivos de comprimento fixo.  
  
> [!NOTE]  
>  O **ColNameHeader** configuração nas substituições de Schema. ini o **FirstRowHasNames** definição no registro do Windows, o arquivo por arquivo.  
  
 Os tipos de dados dos campos também podem ser determinados. Use o **MaxScanRows** opção para indicar quantas linhas devem ser verificadas para determinar os tipos de coluna. Se você definir **MaxScanRows** como 0, todo o arquivo é verificado. O **MaxScanRows** no Schema. ini substituirá a configuração no registro do Windows, o arquivo por arquivo.  
  
 A seguinte entrada indica que o Microsoft Jet deve usar os dados na primeira linha da tabela para determinar os nomes de campo e deve examinar todo o arquivo para determinar os dados usados de tipos:  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 A próxima entrada designa os campos em uma tabela usando o número da coluna (**Col**_n_) opção, que é necessário para arquivos de comprimento fixo e opcional para arquivos delimitados por caracteres. O exemplo mostra as entradas de Schema. ini para dois campos, um campo de texto CustomerNumber 10 caracteres e um campo de texto CustomerName 30 caracteres:  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 A sintaxe da **Col**_n_ é:  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir descreve cada parte do **Col * * * n* entrada.  
  
|Parâmetro|Description|  
|---------------|-----------------|  
|*ColumnName*|O nome da coluna de texto. Se o nome da coluna contiver espaços inseridos, você deverá colocá-lo entre aspas duplas.|  
|*type*|Tipos de dados são da seguinte maneira:<br /><br /> **Tipos de dados Microsoft Jet**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> Longo<br /><br /> CURRENCY<br /><br /> Single<br /><br /> Double<br /><br /> DateTime<br /><br /> Texto<br /><br /> Memorando<br /><br /> **Tipos de dados ODBC** Char (mesmo que o texto)<br /><br /> Float (mesmo que Double)<br /><br /> Inteiro (mesmo que Short)<br /><br /> LongChar (mesmo que o memorando)<br /><br /> Data *formato de data*|  
|**Width**|O valor de cadeia de caracteres literal `Width`. Indica que o número a seguir designa a largura da coluna (opcional para arquivos delimitados por caracteres; necessário para arquivos de comprimento fixo).|  
|*#*|O valor de inteiro que determina a largura da coluna (necessário se **largura** for especificado).|  
  
## <a name="selecting-a-character-set"></a>Selecionar um conjunto de caracteres  
 Você pode selecionar entre dois conjuntos de caracteres: ANSI e OEM. O **CharacterSet** no Schema. ini substituirá a configuração no registro do Windows, o arquivo por arquivo. O exemplo a seguir mostra a entrada de Schema. ini que define o conjunto de caracteres para ANSI:  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>Especificar formatos de tipo de dados e conversões  
 O arquivo Schema ini contém várias opções que você pode usar para especificar como os dados são convertidos ou exibidos. A tabela a seguir lista cada uma dessas opções.  
  
|Opção|Description|  
|------------|-----------------|  
|**DateTimeFormat**|Pode ser definido como uma cadeia de caracteres de formato que indica as datas e horas. Você deve especificar essa entrada se todos os campos de data/hora em que a importação/exportação são tratados com o mesmo formato. Todos os formatos do Microsoft Jet, exceto A.M. e horas. há suporte. Se não houver nenhuma cadeia de caracteres de formato, as opções de imagem e a hora de data abreviada do painel de controle do Windows são usadas.|  
|**DecimalSymbol**|Pode ser definido como qualquer caractere único que é usado para separar o inteiro da parte fracionária de um número.|  
|**NumberDigits**|Indica o número de dígitos decimais da parte fracionária de um número.|  
|**NumberLeadingZeros**|Especifica se um valor decimal menor que 1 e mais de – 1 deve conter os zeros à esquerda; Esse valor pode ser qualquer um dos False (sem zeros à esquerda) ou True.|  
|**CurrencySymbol**|Indica o símbolo de moeda que pode ser usado para valores de moeda no arquivo de texto. Exemplos incluem o sinal de cifrão ($) e o Dm.|  
|**CurrencyPosFormat**|Pode ser definido para qualquer um dos seguintes valores:<br /><br /> -Prefixo do símbolo da moeda sem separação ($1)<br />-Sufixo do símbolo da moeda sem separação (1$)<br />-Prefixo do símbolo da moeda com uma separação de caractere (US $ 1)<br />-Sufixo do símbolo da moeda com uma separação de caractere (1 $)|  
|**CurrencyDigits**|Especifica o número de dígitos usados para a parte fracionária de um valor de moeda.|  
|**CurrencyNegFormat**|Pode ser um dos seguintes valores:<br /><br /> -   ($1)<br />-   –$1<br />-   $–1<br />-   $1–<br />-   (1$)<br />-   –1$<br />-   1–$<br />-   1$–<br />-   –1 $<br />-   –$ 1<br />-   1 $–<br />-   $ 1–<br />-   $ –1<br />-   1– $<br />-   ($ 1)<br />-   (1 $)<br /><br /> Este exemplo mostra o símbolo de dólar, mas você deve substituí-lo com os devidos **CurrencySymbol** valor no programa.|  
|**CurrencyThousandSymbol**|Indica o símbolo de caractere único que pode ser usado para separar os valores de moeda no arquivo de texto por milhares.|  
|**CurrencyDecimalSymbol**|Pode ser definido como qualquer caractere único que é usado para separar toda a parte fracionária de um valor de moeda.|  
  
> [!NOTE]  
>  Se você omitir uma entrada, o valor padrão no painel de controle do Windows é usado.
