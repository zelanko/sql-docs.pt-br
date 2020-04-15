---
title: Arquivo Schema.ini (Driver de arquivo de texto) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 365351724f27205e7d460c757f1268d042cefc76
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305507"
---
# <a name="schemaini-file-text-file-driver"></a>Schema.ini File (Driver de Arquivo de texto)
Quando o driver texto é usado, o formato do arquivo de texto é determinado usando um arquivo de informações de esquema. O arquivo de informações do esquema é sempre chamado de Schema.ini e sempre mantido no mesmo diretório que a fonte de dados de texto. O arquivo de informações do esquema fornece ao IISAM informações sobre o formato geral do arquivo, o nome da coluna e as informações do tipo de dados e várias outras características de dados. Um arquivo Schema.ini é sempre necessário para acessar dados de comprimento fixo. Você deve usar um arquivo Schema.ini quando sua tabela de texto contiver dados DateTime, Currency ou Decimal, ou a qualquer momento que você queira ter mais controle sobre o manuseio dos dados na tabela.  
  
> [!NOTE]  
>  O texto ISAM obterá valores iniciais do registro, não do Schema.ini. O mesmo formato de arquivo padrão se aplica a todas as novas tabelas de dados de texto. Todos os arquivos criados pela declaração CREATE TABLE herdam esses mesmos valores de formato padrão, que são definidos selecionando valores de formato de arquivo na caixa de diálogo **Definir formato de texto** com \<> padrão escolhidas na lista **Tabelas.** Se os valores no registro diferem dos valores em Schema.ini, os valores no registro serão substituídos pelos valores de Schema.ini.  
  
## <a name="understanding-schemaini-files"></a>Entendendo arquivos Schema.ini  
 Os arquivos Schema.ini fornecem informações sobre os registros em um arquivo de texto. Cada entrada do Schema.ini especifica uma das cinco características da tabela:  
  
-   O nome do arquivo de texto  
  
-   O formato do arquivo  
  
-   Os nomes de campo, larguras e tipos  
  
-   O conjunto de caracteres  
  
-   Conversões especiais do tipo de dados  
  
 As seções a seguir discutem essas características.  
  
## <a name="specifying-the-file-name"></a>Especificando o nome do arquivo  
 A primeira entrada em Schema.ini é sempre o nome do arquivo de origem de texto incluído em colchetes quadrados. O exemplo a seguir ilustra a entrada do arquivo Sample.txt:  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>Especificando o formato do arquivo  
 A opção **Formato** em Schema.ini especifica o formato do arquivo de texto. O Texto IISAM pode ler o formato automaticamente a partir da maioria dos arquivos delimitados por caracteres. Você pode usar qualquer caractere como um delimitador no arquivo, exceto a marca de cotação dupla ("). A configuração **de formato** em Schema.ini substitui a configuração no Registro do Windows, arquivo por arquivo. A tabela a seguir lista os valores válidos para a opção **Formato.**  
  
|Especificador de formato|Formato da tabela|Declaração de formato schema.ini|  
|----------------------|------------------|---------------------------------|  
|**Guia Delimitada**|Os campos no arquivo são delimitados por guias.|Formato=TabDelimited|  
|**CSV Delimitado**|Os campos no arquivo são delimitados por vírgulas (valores separados por vírgula).|Formato=CSVDelimited|  
|**Personalizado delimitado**|Os campos no arquivo são delimitados por qualquer caractere que você escolher para inserir na caixa de diálogo. Todas, exceto as aspas duplas (") são permitidas, incluindo em branco.|Formato=Delimitado *(caractere personalizado)*<br /><br /> -ou-<br /><br /> Sem delimitador especificado:<br /><br /> Formato=Delimitado( )|  
|**Comprimento fixo**|Os campos no arquivo são de um comprimento fixo.|Formato=Comprimento fixo|  
  
## <a name="specifying-the-fields"></a>Especificando os Campos  
 Você pode especificar nomes de campo em um arquivo de texto delimitado por caracteres de duas maneiras:  
  
-   Inclua os nomes de campo na primeira linha da tabela e defina **ColNameHeader** como **True.**  
  
-   Especifique cada coluna por número e designe o nome da coluna e o tipo de dados.  
  
 Você deve especificar cada coluna por número e designar o nome da coluna, o tipo de dados e a largura para arquivos de comprimento fixo.  
  
> [!NOTE]  
>  A configuração **ColNameHeader** em Schema.ini substitui a configuração **FirstRowHasNames** no Registro do Windows, arquivo por arquivo.  
  
 Os tipos de dados dos campos também podem ser determinados. Use a opção **MaxScanRows** para indicar quantas linhas devem ser digitalizadas ao determinar os tipos de coluna. Se você definir **MaxScanRows** como 0, todo o arquivo será digitalizado. A configuração **MaxScanRows** em Schema.ini substitui a configuração no Registro do Windows, arquivo por arquivo.  
  
 A entrada a seguir indica que o Microsoft Jet deve usar os dados na primeira linha da tabela para determinar nomes de campo e deve examinar todo o arquivo para determinar os tipos de dados usados:  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 A próxima entrada designa campos em uma tabela usando a opção número da coluna **(Col**_n),_ que é opcional para arquivos delimitados de caracteres e necessária para arquivos de comprimento fixo. O exemplo mostra as entradas Schema.ini para dois campos, um campo de texto CustomerNumber de 10 caracteres e um campo de texto CustomerName de 30 caracteres:  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 A sintaxe do **Coronel**_n_ é:  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir descreve cada parte da entrada **do Col**_n._  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*ColumnName*|O nome do texto da coluna. Se o nome da coluna contiver espaços incorporados, você deve inseri-lo entre aspas duplas.|  
|*type*|Os tipos de dados são os seguintes:<br /><br /> **Tipos de dados do Microsoft Jet**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> long<br /><br /> Moeda<br /><br /> Single<br /><br /> Double<br /><br /> Datetime<br /><br /> Texto<br /><br /> Memo<br /><br /> **Tipos de dados ODBC** Char (o mesmo que Texto)<br /><br /> Flutuar (o mesmo que Duplo)<br /><br /> Inteiro (o mesmo que Short)<br /><br /> LongChar (o mesmo que Memo)<br /><br /> Formato *da data*|  
|**Largura**|O valor `Width`da seqüência literal . Indica que o número a seguir designa a largura da coluna (opcional para arquivos delimitados de caracteres; necessário para arquivos de comprimento fixo).|  
|*#*|O valor inteiro que designa a largura da coluna (necessário se **a largura** for especificada).|  
  
## <a name="selecting-a-character-set"></a>Selecionando um conjunto de caracteres  
 Você pode selecionar entre dois conjuntos de caracteres: ANSI e OEM. A configuração **CharacterSet** em Schema.ini substitui a configuração no Registro do Windows, arquivo por arquivo. O exemplo a seguir mostra a entrada Schema.ini que define o caractere definido como ANSI:  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>Especificando formatos e conversões de tipos de dados  
 O arquivo Schema.ini contém várias opções que você pode usar para especificar como os dados são convertidos ou exibidos. A tabela a seguir lista cada uma dessas opções.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**DateTimeFormat**|Pode ser definido como uma seqüência de formato que indica datas e horários. Você deve especificar esta entrada se todos os campos de data/hora na importação/exportação forem tratados com o mesmo formato. Todos os formatos do Microsoft Jet, exceto A.M. e P.M. têm suporte. Se não houver seqüência de formato, as opções de data curta e de tempo do Painel de Controle do Windows serão usadas.|  
|**Símbolo decimal**|Pode ser definido para qualquer caractere que seja usado para separar o inteiro da parte fracionada de um número.|  
|**Dígitos numécis**|Indica o número de dígitos decimais na porção fracionada de um número.|  
|**NumberLeadingZeros**|Especifica se um valor decimal menor que 1 e mais de -1 deve conter zeros principais; este valor pode ser falso (sem zeros de liderança) ou True.|  
|**CurrencySymbol**|Indica o símbolo de moeda que pode ser usado para valores de moeda no arquivo de texto. Exemplos incluem o sinal de dólar ($) e Dm.|  
|**Formato CurrencyPos**|Pode ser definido como qualquer um dos seguintes valores:<br /><br /> - Prefixo do símbolo de moeda sem separação ($1)<br />- Sufixo do símbolo da moeda sem separação (1$)<br />- Prefixo de símbolo de moeda com uma separação de caracteres ($ 1)<br />- Sufixo de símbolo de moeda com uma separação de caracteres (1 $)|  
|**Dígitos de moedas**|Especifica o número de dígitos usados para a parte fracionada de uma moeda.|  
|**CurrencyNegFormat**|Pode ser um dos seguintes valores:<br /><br /> - ($1)<br />- -$1<br />- $-1<br />- $1-<br />- (1$)<br />- -1$<br />- 1-$<br />- 1$-<br />- -1 $<br />- -$ 1<br />- 1 dólar.<br />- 1 dólar.<br />- - $ - 1<br />- 1- $<br />- ($ 1)<br />- (1 $)<br /><br /> Este exemplo mostra o sinal do dólar, mas você deve substituí-lo pelo valor **de CurrencySymbol** apropriado no programa real.|  
|**CurrencyThousandSymbol**|Indica o símbolo de caractere único que pode ser usado para separar os valores da moeda no arquivo de texto por milhares.|  
|**Símbolo de moedaDecimal**|Pode ser definido para qualquer caractere único que é usado para separar o todo da parte fracionada de um valor de moeda.|  
  
> [!NOTE]  
>  Se você omitir uma entrada, o valor padrão no Painel de Controle do Windows será usado.
