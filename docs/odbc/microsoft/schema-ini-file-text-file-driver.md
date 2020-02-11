---
title: Arquivo Schema. ini (driver de arquivo de texto) | Microsoft Docs
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
ms.openlocfilehash: dd95329c91c69af38b1ffc7951191498fcc40479
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67987940"
---
# <a name="schemaini-file-text-file-driver"></a>Schema.ini File (Driver de Arquivo de texto)
Quando o driver de texto é usado, o formato do arquivo de texto é determinado usando um arquivo de informações de esquema. O arquivo de informações de esquema sempre é denominado Schema. ini e sempre é mantido no mesmo diretório que a fonte de dados de texto. O arquivo de informações de esquema fornece o IISAM com informações sobre o formato geral do arquivo, o nome da coluna e informações de tipo de dados e várias outras características de dados. Um arquivo Schema. ini sempre é necessário para acessar dados de comprimento fixo. Você deve usar um arquivo Schema. ini quando sua tabela de texto contiver dados DateTime, de moeda ou decimais, ou sempre que desejar mais controle sobre a manipulação dos dados na tabela.  
  
> [!NOTE]  
>  O texto ISAM obterá os valores iniciais do registro, não de Schema. ini. O mesmo formato de arquivo padrão se aplica a todas as novas tabelas de dados de texto. Todos os arquivos que foram criados pela instrução CREATE TABLE herdam os mesmos valores de formato padrão, que são definidos selecionando-se os valores de formato de arquivo na \<caixa de diálogo **definir formato de texto** com o padrão> escolhido na lista **tabelas** . Se os valores no registro forem diferentes dos valores em Schema. ini, os valores no registro serão substituídos pelos valores de Schema. ini.  
  
## <a name="understanding-schemaini-files"></a>Noções básicas sobre arquivos Schema. ini  
 Os arquivos Schema. ini fornecem informações de esquema sobre os registros em um arquivo de texto. Cada entrada Schema. ini especifica uma das cinco características da tabela:  
  
-   O nome do arquivo de texto  
  
-   O formato do arquivo  
  
-   Os nomes de campo, as larguras e os tipos  
  
-   O conjunto de caracteres  
  
-   Conversões de tipo de dados especiais  
  
 As seções a seguir discutem essas características.  
  
## <a name="specifying-the-file-name"></a>Especificando o nome do arquivo  
 A primeira entrada em Schema. ini é sempre o nome do arquivo de origem de texto entre colchetes. O exemplo a seguir ilustra a entrada para o arquivo Sample. txt:  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>Especificando o formato de arquivo  
 A opção **Format** em Schema. ini especifica o formato do arquivo de texto. O texto IISAM pode ler o formato automaticamente da maioria dos arquivos delimitados por caractere. Você pode usar qualquer caractere único como um delimitador no arquivo, exceto o sinal de aspas duplas ("). A configuração de **formato** em Schema. ini substitui a configuração no registro do Windows, file by file. A tabela a seguir lista os valores válidos para a opção **Format** .  
  
|Especificador de formato|Formato de tabela|Instrução de formato Schema. ini|  
|----------------------|------------------|---------------------------------|  
|**Delimitado por tabulação**|Os campos no arquivo são delimitados por guias.|Formato = TabDelimited|  
|**Delimitado por CSV**|Os campos no arquivo são delimitados por vírgulas (valores separados por vírgula).|Formato = CSVDelimited|  
|**Personalizado**|Os campos no arquivo são delimitados por qualquer caractere que você escolher para inserir na caixa de diálogo. Todos, exceto as aspas duplas ("), são permitidas, incluindo em branco.|Formato = delimitado (*caractere personalizado*)<br /><br /> -ou-<br /><br /> Sem delimitador especificado:<br /><br /> Formato = delimitado ()|  
|**Comprimento fixo**|Os campos no arquivo têm um comprimento fixo.|Formato = Cadeia|  
  
## <a name="specifying-the-fields"></a>Especificando os campos  
 Você pode especificar nomes de campo em um arquivo de texto delimitado por caractere de duas maneiras:  
  
-   Inclua os nomes de campo na primeira linha da tabela e defina **ColNameHeader** como **true.**  
  
-   Especifique cada coluna por número e designe o nome da coluna e o tipo de dados.  
  
 Você deve especificar cada coluna por número e designar o nome da coluna, o tipo de dados e a largura para arquivos de comprimento fixo.  
  
> [!NOTE]  
>  A configuração **ColNameHeader** em Schema. ini substitui a configuração **FirstRowHasNames** no registro do Windows, file by file.  
  
 Os tipos de dados dos campos também podem ser determinados. Use a opção **MaxScanRows** para indicar quantas linhas devem ser verificadas ao determinar os tipos de coluna. Se você definir **MaxScanRows** como 0, o arquivo inteiro será verificado. A configuração **MaxScanRows** em Schema. ini substitui a configuração no registro do Windows, file by file.  
  
 A entrada a seguir indica que o Microsoft Jet deve usar os dados na primeira linha da tabela para determinar os nomes de campo e deve examinar o arquivo inteiro para determinar os tipos de dados usados:  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 A próxima entrada designa campos em uma tabela usando a opção número de coluna (**Col**_n_), que é opcional para arquivos delimitados por caractere e é necessária para arquivos de comprimento fixo. O exemplo mostra as entradas de Schema. ini para dois campos, um campo de texto CustomerNumber de 10 caracteres e um campo de texto CustomerName de 30 caracteres:  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 A sintaxe da **coluna**_n_ é:  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir descreve cada parte da entrada da **coluna**_n_ .  
  
|Parâmetro|DESCRIÇÃO|  
|---------------|-----------------|  
|*ColumnName*|O nome de texto da coluna. Se o nome da coluna contiver espaços inseridos, você deverá colocá-los entre aspas duplas.|  
|*tipo*|Os tipos de dados são os seguintes:<br /><br /> **Tipos de dados do Microsoft Jet**<br /><br /> bit<br /><br /> Byte<br /><br /> Curto<br /><br /> long<br /><br /> Moeda<br /><br /> Single<br /><br /> DOUBLE<br /><br /> DateTime<br /><br /> Texto<br /><br /> Campos<br /><br /> **Tipos de dados ODBC** Char (o mesmo que Text)<br /><br /> Float (igual a Double)<br /><br /> Inteiro (igual a curto)<br /><br /> LongChar (o mesmo que Memo)<br /><br /> *Formato de data* /data|  
|**Width**|O valor `Width`da cadeia de caracteres literal. Indica que o número a seguir designa a largura da coluna (opcional para arquivos delimitados por caractere; necessário para arquivos de comprimento fixo).|  
|*#*|O valor inteiro que designa a largura da coluna (obrigatório se a **largura** for especificada).|  
  
## <a name="selecting-a-character-set"></a>Selecionando um conjunto de caracteres  
 Você pode selecionar entre dois conjuntos de caracteres: ANSI e OEM. A configuração **CharacterSet** em Schema. ini substitui a configuração no registro do Windows, file by file. O exemplo a seguir mostra a entrada Schema. ini que define o conjunto de caracteres como ANSI:  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>Especificando formatos e conversões de tipo de dados  
 O arquivo Schema. ini contém várias opções que você pode usar para especificar como os dados são convertidos ou exibidos. A tabela a seguir lista cada uma dessas opções.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**DateTimeFormat**|Pode ser definido como uma cadeia de caracteres de formato que indica datas e horas. Você deve especificar essa entrada se todos os campos de data/hora na importação/exportação forem manipulados com o mesmo formato. Todos os formatos do Microsoft Jet, exceto A.M. e P.M. têm suporte. Se não houver nenhuma cadeia de caracteres de formato, as opções de imagem e hora da data abreviada do painel de controle do Windows serão usadas.|  
|**DecimalSymbol**|Pode ser definido como qualquer caractere único que é usado para separar o inteiro da parte fracionária de um número.|  
|**NumberDigits**|Indica o número de dígitos decimais na parte fracionária de um número.|  
|**NumberLeadingZeros**|Especifica se um valor decimal menor que 1 e maior que-1 deve conter zeros à esquerda; Esse valor pode ser false (sem zeros à esquerda) ou true.|  
|**CurrencySymbol**|Indica o símbolo de moeda que pode ser usado para valores de moeda no arquivo de texto. Os exemplos incluem o cifrão ($) e o DM.|  
|**CurrencyPosFormat**|Pode ser definido como qualquer um dos seguintes valores:<br /><br /> -Prefixo do símbolo de moeda sem separação ($1)<br />-Sufixo do símbolo de moeda sem separação ($1)<br />-Prefixo do símbolo de moeda com uma separação de caracteres ($1)<br />-Sufixo do símbolo de moeda com uma separação de caracteres ($1)|  
|**CurrencyDigits**|Especifica o número de dígitos usados para a parte fracionária de um valor de moeda.|  
|**CurrencyNegFormat**|Pode ser um dos seguintes valores:<br /><br /> -($1)<br />--$1<br />-US $-1<br />-$1-<br />-($1)<br />--$1<br />-1-$<br />-$1-<br />--$1<br />--$1<br />-$1-<br />-$1-<br />-US $-1<br />-1-$<br />-($1)<br />-($1)<br /><br /> Este exemplo mostra o sinal de dólar, mas você deve substituí-lo pelo valor **CurrencySymbol** apropriado no programa real.|  
|**CurrencyThousandSymbol**|Indica o símbolo de caractere único que pode ser usado para separar valores de moeda no arquivo de texto por milhares.|  
|**CurrencyDecimalSymbol**|Pode ser definido como qualquer caractere único que é usado para separar o todo da parte fracionária de um valor de moeda.|  
  
> [!NOTE]  
>  Se você omitir uma entrada, o valor padrão no painel de controle do Windows será usado.
