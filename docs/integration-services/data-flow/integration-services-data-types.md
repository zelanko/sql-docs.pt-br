---
title: Tipos de dados do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- modifying data types
- data types [Integration Services], listed
- data types [Integration Services]
- column data types [Integration Services]
- SSIS, data types
- Integration Services, data types
- SQL Server Integration Services, data types
ms.assetid: 896fc3e8-3aa6-4396-ba82-5d7741cffa56
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 64fb0e9310230634c36ee0c1bca0cf9c89914bab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65726878"
---
# <a name="integration-services-data-types"></a>Tipos de dados do Integration Services

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Quando dados entram em um fluxo de dados em um pacote, a fonte que extrai esses dados converte-os em um tipo de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Dados numéricos são atribuídos a um tipo de dados numéricos, dados de cadeia são atribuídos a um tipo de dados de caractere e datas são atribuídas a um tipo de dados de data. Outros dados, como GUIDs e BLOBs, também são atribuídos aos tipos de dados apropriados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Se dados tiverem um tipo de dados que não pode ser convertido em um tipo de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , ocorrerá um erro.  
  
 Alguns componentes de fluxo de dados convertem tipos de dados entre os tipos de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e os tipos de dados gerenciados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Para obter mais informações sobre o mapeamento entre [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e tipos de dados gerenciados, consulte [Trabalhando com tipos de dados no fluxo de dados](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md).  
  
 A tabela a seguir lista os tipos de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Alguns dos tipos de dados na tabela têm informações de precisão e escala que se aplicam a eles. Para obter mais informações sobre precisão e escala, consulte [Precisão, escala e comprimento &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
|Tipo de dados|Descrição|  
|---------------|-----------------|  
|DT_BOOL|Um valor booliano.|  
|DT_BYTES|Um valor de dados binários. O comprimento é variável e o comprimento de máximo é 8000 bytes.|  
|DT_CY|Um valor de moeda. Este tipo de dados é um inteiro assinado de oito bytes com uma escala de 4 e precisão máxima de 19 dígitos.|  
|DT_DATE|Uma estrutura de data que consiste em ano, mês, dia, hora, minuto, segundos e segundos fracionários.  Os segundos fracionários têm uma escala fixa de 7 dígitos.<br /><br /> O tipo de dados DT_DATE é implementado com o uso de um número de ponto flutuante de 8 bytes. Dias são representados por incrementos de números inteiros, iniciando em 30 de dezembro de 1899 e meia-noite como zero hora. Valores de hora são expressos como o valor absoluto da parte fracionária do número. No entanto, um valor de ponto flutuante não pode representar todos os valores reais, portanto, há limites no intervalo de datas que podem ser apresentados em DT_DATE.<br /><br /> Por outro lado, DT_DBTIMESTAMP é representado por uma estrutura que internamente tem campos individuais para ano, mês, dia, horas, minutos, segundos e milissegundos. Este tipo de dados tem limites maiores em intervalos de datas que pode apresentar.|  
|DT_DBDATE|Uma estrutura de data que consiste em ano, mês e dia.|  
|DT_DBTIME|Uma estrutura de hora que consiste em hora, minuto e segundo.|  
|DT_DBTIME2|Uma estrutura de hora que consiste em hora, minuto, segundo e segundos fracionários. Os segundos fracionários têm uma escala máxima de 7 dígitos.|  
|DT_DBTIMESTAMP|Uma estrutura de carimbo de hora que consiste em ano, mês, dia, hora, minuto, segundo e segundos fracionários. Os segundos fracionários têm uma escala máxima de 3 dígitos.|  
|DT_DBTIMESTAMP2|Uma estrutura de carimbo de hora que consiste em ano, mês, dia, hora, minuto, segundo e segundos fracionários. Os segundos fracionários têm uma escala máxima de 7 dígitos.|  
|DT_DBTIMESTAMPOFFSET|Uma estrutura de carimbo de hora que consiste em ano, mês, dia, hora, minuto, segundo e segundos fracionários. Os segundos fracionários têm uma escala máxima de 7 dígitos.<br /><br /> Diferente dos tipos de dados DT_DBTIMESTAMP e DT_DBTIMESTAMP2, o tipo de dados DT_DBTIMESTAMPOFFSET tem um deslocamento de fuso horário. Esse deslocamento especifica o número de horas e minutos que o horário é deslocado do tempo universal coordenado (UTC). O deslocamento de fuso horário é usado pelo sistema para obter a hora local.<br /><br /> O deslocamento de fuso horário deve incluir um sinal de soma ou subtração para indicar se esse deslocamento é somado ou subtraído do UTC. O número válido de deslocamento de horas está entre -14 e +14. O sinal para o deslocamento de minutos depende do sinal para o deslocamento de hora:<br /><br /> Se o sinal do deslocamento de hora for negativo, o deslocamento de minuto deverá ser negativo ou zero.<br /><br /> Se o sinal para o deslocamento de hora for positivo, o deslocamento de minuto deverá ser positivo ou zero.<br /><br /> Se o sinal para o deslocamento de hora for zero, o deslocamento de minuto poderá ser qualquer valor do negativo 0.59 ao positivo 0.59.|  
|DT_DECIMAL|Um valor numérico exato com uma precisão fixa e uma escala fixa. Esse tipo de dados é um inteiro não assinado de 12 bytes com um sinal separado, uma escala de 0 a 28 e uma precisão máxima de 29.|  
|DT_FILETIME|Um valor de 64 bits que representa o número de intervalos de 100 nanossegundos desde 1 de janeiro de 1601. Os segundos fracionários têm uma escala máxima de 3 dígitos.|  
|DT_GUID|Um identificador global exclusivo (GUID).|  
|DT_I1|Um inteiro assinado de um byte.|  
|DT_I2|Um inteiro assinado de dois bytes.|  
|DT_I4|Um inteiro assinado de quatro bytes.|  
|DT_I8|Um inteiro assinado de oito bytes.|  
|DT_NUMERIC|Um valor numérico exato com precisão e escala fixas. Esse tipo de dados é um inteiro não assinado de 16 bytes com um sinal separado, uma escala de 0 a -38 e uma precisão máxima de 38.|  
|DT_R4|Um valor de ponto flutuante de precisão única.|  
|DT_R8|Um valor de ponto flutuante de precisão dupla.|  
|DT_STR|Uma cadeia de caracteres [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/MBCS com terminação nula com um comprimento máximo de 8000 caracteres. (Se um valor de coluna contiver terminadores nulos adicionais, a cadeia será truncada na ocorrência do primeiro nulo.)|  
|DT_UI1|Um inteiro não assinado de um byte.|  
|DT_UI2|Um inteiro não assinado de dois bytes.|  
|DT_UI4|Um inteiro não assinado de quatro bytes.|  
|DT_UI8|Um inteiro não assinado de oito bytes.|  
|DT_WSTR|Uma cadeia de caracteres Unicode com terminação nula com um comprimento máximo de 4000 caracteres. (Se um valor de coluna contiver terminadores nulos adicionais, a cadeia será truncada na ocorrência do primeiro nulo.)|  
|DT_IMAGE|Um valor binário com um tamanho máximo de 2^31-1 (2.147.483.647) bytes. .|  
|DT_NTEXT|Uma cadeia de caracteres Unicode com um comprimento máximo de 2^30–1 (1.073.741.823) caracteres.|  
|DT_TEXT|Uma cadeia de caracteres [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/MBCS com um comprimento máximo de 2^31–1 (2.147.483.647) caracteres.|  
  
## <a name="conversion-of-data-types"></a>Conversão de tipos de dados  
 Se os dados em uma coluna não exigirem a largura total alocada pelo tipo de dados de origem, talvez você queira alterar o tipo de dados da coluna. Tornar cada linha de dados mais estreita possível ajuda você a otimizar o desempenho ao transferir dados porque quanto mais estreita a linha, mais rápido os dados são transferidos da origem para o destino.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui um conjunto completo de tipos de dados numéricos para que você possa corresponder o tipo de dados que mais de aproxima do tamanho dos dados. Por exemplo, se os valores em uma coluna com um tipo de dados DT_UI8 forem sempre inteiros entre 0 e 3000, você poderá alterar o tipo de dados para DT_UI2. De modo semelhante, se uma coluna com o tipo de dados DT_CY puder corresponder aos requisitos de dados de pacote usando um tipo de dados inteiro, você poderá alterar o tipo de dados para DT_I4.  
  
 Você pode alterar o tipo de dados de uma coluna das seguintes formas:  
  
-   Use uma expressão para converter tipos de dados implicitamente. Para obter mais informações, consulte [Tipos de dados do Integration Services em expressões](../../integration-services/expressions/integration-services-data-types-in-expressions.md), [Tipos de dados do Integration Services em expressões](../../integration-services/expressions/integration-services-data-types-in-expressions.md) e [Expressões do Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
-   Use o operador cast para converter tipos de dados. Para obter mais informações, consulte [Cast &#40;Expressão do SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
-   Use a transformação Conversão de Dados para converter o tipo de dados de uma coluna de um tipo para um tipo de dados diferente. Para obter mais informações, consulte [Data Conversion Transformation](../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
-   Use a transformação Coluna Derivada para criar uma cópia de uma coluna que tenha um tipo de dados diferente da coluna original. Para obter mais informações, consulte [Derived Column Transformation](../../integration-services/data-flow/transformations/derived-column-transformation.md).  
  
### <a name="converting-between-strings-and-datetime-data-types"></a>Conversão entre cadeias de caracteres e tipos de dados de data/hora  
 A tabela a seguir lista os resultados da conversão entre tipos de dados de data/hora e cadeias de caracteres:  
  
-   Ao usar o operador cast ou a transformação Conversão de Dados, o tipo de dados de data ou hora é convertido no formato de cadeia de caracteres correspondente. Por exemplo, o tipo de dados DT_DBTIME será convertido em uma cadeia de caracteres que tem o formato “hh:mm:ss”.  
  
-   Quando desejar converter de uma cadeia de caracteres em um tipo de dados de data ou hora, a cadeia de caracteres deve usar o formato que corresponde ao tipo de dados de data ou hora apropriado. Por exemplo, para converter algumas cadeias de caracteres de data com êxito no tipo de dados DT_DBDATE, essas cadeias de caracteres devem estar no formato “aaaa-mm-dd”.  
  
    |Tipo de dados|Formato da cadeia de caracteres|  
    |---------------|-------------------|  
    |DT_DBDATE|aaaa-mm-dd|  
    |DT_FILETIME|aaaa-mm-dd hh:mm:ss:fff|  
    |DT_DBTIME|hh:mm:ss|  
    |DT_DBTIME2|hh:mm:ss[.fffffff]|  
    |DT_DBTIMESTAMP|aaaa-mm-dd hh:mm:ss[.fff]|  
    |DT_DBTIMESTAMP2|aaaa-mm-dd hh:mm:ss[.fffffff]|  
    |DT_DBTIMESTAMPOFFSET|aaaa-mm-dd hh:mm:ss[.fffffff] [{+&#124;-} hh:mm]|  
  
 No formato de DT_FILETIME e DT_DBTIMESTAMP, fff é um valor entre 0 e 999 que representa segundos fracionários.  
  
 No formato de data de DBTIMESTAMP2, DT_DBTIME2 e DT_DBTIMESTAMPOFFSET, fffffff é um valor entre 0 e 9999999 que representa segundos fracionários.  
  
 O formato de data de DT_DBTIMESTAMPOFFSET também inclui um elemento de fuso horário. Há um espaço entre o elemento de hora e o elemento de fuso horário.  
  
### <a name="converting-datetime-data-types"></a>Convertendo tipos de dados de data e hora  
 Você pode alterar o tipo de dados em uma coluna com dados de data e hora para extrair a parte de data ou hora dos dados. As tabelas seguintes listam os resultados da alteração de um tipo de dados de data e hora para outro tipo de dados de data e hora.  
  
#### <a name="converting-from-dtfiletime"></a>Convertendo a partir de DT_FILETIME  
  
|Converter DT_FILETIME para|Resultado|  
|-----------------------------|------------|  
|DT_FILETIME|Nenhuma alteração.|  
|DT_DATE|Converte o tipo de dados.|  
|DT_DBDATE|Remove o valor de hora.|  
|DT_DBTIME|Remove o valor de data.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos fracionários que o tipo de dados DT_DBTIME pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIME2|Remove o valor de data representado pelo tipo de dados DT_FILETIME.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIME2 pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Converte o tipo de dados.|  
|DT_DBTIMESTAMP2|Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIMESTAMP2 pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Define o campo de fuso horário no tipo de dados DT_DBTIMESTAMPOFFSET como zero.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIMESTAMPOFFSET pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
  
#### <a name="converting-from-dtdate"></a>Convertendo a partir de DT_DATE  
  
|Converter DT_DATE em|Resultado|  
|-------------------------|------------|  
|DT_FILETIME|Converte o tipo de dados.|  
|DT_DATE|Nenhuma alteração.|  
|DT_DBDATE|Remove o valor de hora representado pelo tipo de dados DT_DATA.|  
|DT_DBTIME|Remove o valor de data representado pelo tipo de dados DT_DATE.|  
|DT_DBTIME2|Remove o valor de data representado pelo tipo de dados DT_DATE.|  
|DT_DBTIMESTAMP|Converte o tipo de dados.|  
|DT_DBTIMESTAMP2|Converte o tipo de dados.|  
|DT_DBTIMESTAMPOFFSET|Define o campo de fuso horário no tipo de dados DT_DBTIMESTAMPOFFSET como zero.|  
  
#### <a name="converting-from-dtdbdate"></a>Convertendo a partir de DT_DBDATE  
  
|Converter DT_DBDATE para|Resultado|  
|---------------------------|------------|  
|DT_FILETIME|Define os campos de hora no tipo de dados DT_FILETIME como zero.|  
|DT_DATE|Define os campos de hora no tipo de dados DT_DATE como zero.|  
|DT_DBDATE|Nenhuma alteração.|  
|DT_DBTIME|Define os campos de hora no tipo de dados DT_DBTIME como zero.|  
|DT_DBTIME2|Define os campos de hora no tipo de dados DT_DBTIME2 como zero.|  
|DT_DBTIMESTAMP|Define os campos de hora no tipo de dados DT_DBTIMESTAMP como zero.|  
|DT_DBTIMESTAMP2|Define os campos de hora no tipo de dados DT_DBTIMESTAMP como zero.|  
|DT_DBTIMESTAMPOFFSET|Define os campos de hora e fuso horário no tipo de dados DT_DBTIMESTAMPOFFSET como zero.|  
  
#### <a name="converting-from-dtdbtime"></a>Convertendo a partir de DT_DBTIME  
  
|Converter DT_DBTIME para|Resultado|  
|---------------------------|------------|  
|DT_FILETIME|Define o campo de data no tipo de dados DT_FILETIME como a data atual.|  
|DT_DATE|Define o campo de data no tipo de dados DT_DATE como a data atual.|  
|DT_DBDATE|Define o campo de data no tipo de dados DT_DBDATE como a data atual.|  
|DT_DBTIME|Nenhuma alteração.|  
|DT_DBTIME2|Converte o tipo de dados.|  
|DT_DBTIMESTAMP|Define o campo de data no tipo de dados DT_DBTIMESTAMP como a data atual.|  
|DT_DBTIMESTAMP2|Define o campo de data no tipo de dados DT_DBTIMESTAMP2 como a data atual.|  
|DT_DBTIMESTAMPOFFSET|Define os campos de data e fuso horário no tipo de dados DT_DBTIMESTAMPOFFSET como a data atual e como zero, respectivamente.|  
  
#### <a name="converting-from-dtdbtime2"></a>Convertendo a partir de DT_DBTIME2  
  
|Converter DT_DBTIME2 para|Resultado|  
|----------------------------|------------|  
|DT_FILETIME|Define o campo de data no tipo de dados DT_FILETIME como a data atual.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_FILETIME pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DATE|Define o campo de data do tipo de dados DT_DATE como a data atual.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DATE pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBDATE|Define o campo de data do tipo de dados DT_DBDATE como a data atual.|  
|DT_DBTIME|Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIME pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIME2|Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIME2 de destino pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Define o campo de data no tipo de dados DT_DBTIMESTAMP como a data atual.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIMESTAMP pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP2|Define o campo de data no tipo de dados DT_DBTIMESTAMP2 como a data atual.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIMESTAMP2 pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Define os campos de data e fuso horário no tipo de dados DT_DBTIMESTAMPOFFSET como a data atual e como zero, respectivamente.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIMESTAMPOFFSET pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
  
#### <a name="converting-from-dtdbtimestamp"></a>Convertendo a partir de DT_DBTIMESTAMP  
  
|Converter DT_DBTIMESTAMP para|Resultado|  
|--------------------------------|------------|  
|DT_FILETIME|Converte o tipo de dados.|  
|DT_DATE|Se um valor representado pelo tipo de dados DT_DBTIMESTAMP ultrapassar o intervalo do tipo de dados DT_DATE, o erro DB_E_DATAOVERFLOW será retornado. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBDATE|Remove o valor de hora representado pelo tipo de dados DT_DBTIMESTAMP.|  
|DT_DBTIME|Remove o valor de data representado pelo tipo de dados DT_DBTIMESTAMP.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIME pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIME2|Remove o valor de data representado pelo tipo de dados DT_DBTIMESTAMP.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIME2 pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Nenhuma alteração.|  
|DT_DBTIMESTAMP2|Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIMESTAMP2 pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Define o campo de fuso horário no tipo de dados DT_DBTIMESTAMPOFFSET como zero.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIMESTAMPOFFSET pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
  
#### <a name="converting-from-dtdbtimestamp2"></a>Convertendo a partir de DT_DBTIMESTAMP2  
  
|Converter DT_DBTIMESTAMP2 para|Resultado|  
|---------------------------------|------------|  
|DT_FILETIME|Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_FILETIME pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DATE|Se um valor representado pelo tipo de dados DT_DBTIMESTAMP2 ultrapassar o intervalo do tipo de dados DT_DATE, o erro DB_E_DATAOVERFLOW será retornado. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DATE pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBDATE|Remove o valor de hora representado pelo tipo de dados DT_DBTIMESTAMP2.|  
|DT_DBTIME|Remove o valor de data representado pelo tipo de dados DT_DBTIMESTAMP2.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIME pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIME2|Remove o valor de data representado pelo tipo de dados DT_DBTIMESTAMP2.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIME2 pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Se um valor representado pelo tipo de dados DT_DBTIMESTAMP2 ultrapassar o intervalo do tipo de dados DT_DBTIMESTAMP, o erro DB_E_DATAOVERFLOW será retornado.<br /><br /> DT_DBTIMESTAMP2 é mapeado para um tipo de dados do SQL Server, datetime2, com um intervalo de 1º de janeiro do ano 1 DC a 31 de dezembro de 9999 DT_DBTIMESTAMP é mapeado para um tipo de dados do SQL Server, datetime, com um intervalo menor de 1 de janeiro, 1753 a 31 de dezembro de 9999.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIMESTAMP pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados.<br /><br /> Para obter mais informações sobre erros, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP2|Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIMESTAMP2 de destino pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Define o campo de fuso horário no tipo de dados DT_DBTIMESTAMPOFFSET como zero.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIMESTAMPOFFSET pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
  
#### <a name="converting-from-dtdbtimestampoffset"></a>Convertendo a partir de DT_DBTIMESTAMPOFFSET  
  
|Converter DT_DBTIMESTAMPOFFSET para|Resultado|  
|--------------------------------------|------------|  
|DT_FILETIME|Altera o valor de hora representado pelo tipo de dados DT_DBTIMESTAMPOFFSET para o tempo universal coordenado (UTC).<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_FILETIME pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DATE|Altera o valor de hora representado pelo tipo de dados DT_DBTIMESTAMPOFFSET para UTC.<br /><br /> Se um valor representado pelo tipo de dados DT_DBTIMESTAMPOFFSET ultrapassar o intervalo do tipo de dados DT_DATE, o erro DB_E_DATAOVERFLOW será retornado.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DATE pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados.<br /><br /> Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBDATE|Altera o valor de hora representado pelo tipo de dados DT_DBTIMESTAMPOFFSET para UTC, que pode afetar o valor da data. O valor de hora é então removido.|  
|DT_DBTIME|Altera o valor de hora representado pelo tipo de dados DT_DBTIMESTAMPOFFSET para UTC.<br /><br /> Remove o valor de dados representado pelo tipo de dados DT_DBTIMESTAMPEOFFSET.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIME pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIME2|Altera o valor de hora representado pelo tipo de dados DT_DBTIMESTAMPOFFSET para UTC.<br /><br /> Remove o valor de data representado pelo tipo de dados DT_DBTIMESTAMPOFFSET.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIME2 pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Altera o valor de hora representado pelo tipo de dados DT_DBTIMESTAMPOFFSET para UTC.<br /><br /> Se um valor representado pelo tipo de dados DT_DBTIMESTAMPOFFSET ultrapassar o intervalo do tipo de dados DT_DBTIMESTAMP, o erro DB_E_DATAOVERFLOW será retornado.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIMESTAMP pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados.<br /><br /> Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMP2|Altera o valor de hora representado pelo tipo de dados DT_DBTIMESTAMPOFFSET para UTC.<br /><br /> Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIMESTAMP2 pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Remove o valor de segundo fracionário quando sua escala é maior que o número de dígitos de segundos fracionários que o tipo de dados DT_DBTIMESTAMPOFFSET de destino pode conter. Após a remoção do valor de segundo fracionário, gera um relatório sobre esse truncamento de dados. Para obter mais informações, consulte [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).|  
  
## <a name="mapping-of-integration-services-data-types-to-database-data-types"></a>Mapeamento de tipos de dados do Integration Services para tipos de dados de bancos de dados  
 A tabela a seguir fornece orientações sobre como mapear os tipos de dados usados por determinados bancos de dados para tipos de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Esses mapeamentos são resumidos dos arquivos de mapeamento usados pelo Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao importar dados dessas fontes. Para obter mais informações sobre esses arquivos de mapeamento, consulte [Assistente de Importação e Exportação do SQL Server](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md).  
  
> [!IMPORTANT]  
>  Tais mapeamentos não pretendem representar uma equivalência exata, mas apenas orientar. Em determinadas situações, você pode precisar usar um tipo de dados diferente do tipo mostrado nesta tabela.  
  
> [!NOTE]  
>  Você pode usar os tipos de dados do SQL Server para estimar o tamanho dos tipos de dados de data e hora do Integration Services correspondente.  
  
|Tipo de Dados|SQL Server<br /><br /> (SQLOLEDB; SQLNCLI10)|SQL Server (SqlClient)|Jet|Oracle<br /><br /> (OracleClient)|DB2<br /><br /> (DB2OLEDB)|DB2<br /><br /> (IBMDADB2)|  
|---------------|--------------------------------------------|------------------------------|---------|---------------------------------|--------------------------|--------------------------|  
|DT_BOOL|bit|bit|bit||||  
|DT_BYTES|binary, varbinary, timestamp|binary, varbinary, timestamp|BigBinary, VarBinary|RAW|||  
|DT_CY|smallmoney, money|smallmoney, money|CURRENCY||||  
|DT_DATE|||||||  
|DT_DBDATE|[date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)|[date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)||Data|Data|Data|  
|DT_DBTIME||||timestamp|time|time|  
|DT_DBTIME2|[time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)(p)|[time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md) (p)|||||  
|DT_DBTIMESTAMP|[datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md), [smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)|[datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md), [smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)|DateTime|TIMESTAMP, DATE, INTERVAL|TIME, TIMESTAMP, DATE|TIME, TIMESTAMP, DATE|  
|DT_DBTIMESTAMP2|[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)|[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)||timestamp|timestamp|timestamp|  
|DT_DBTIMESTAMPOFFSET|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)(p)|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md) (p)||timestampoffset|timestamp,<br /><br /> varchar|timestamp,<br /><br /> varchar|  
|DT_DECIMAL|||||||  
|DT_FILETIME|||||||  
|DT_GUID|UNIQUEIDENTIFIER|UNIQUEIDENTIFIER|GUID||||  
|DT_I1|||||||  
|DT_I2|SMALLINT|SMALLINT|Short||smallint|SMALLINT|  
|DT_I4|INT|INT|Longo||INTEGER|INTEGER|  
|DT_I8|BIGINT|BIGINT|||bigint|bigint|  
|DT_NUMERIC|decimal, numeric|decimal, numeric|Decimal|NUMBER, INT|decimal, numeric|decimal, numeric|  
|DT_R4|REAL|REAL|Single||real|real|  
|DT_R8|FLOAT|FLOAT|Double|FLOAT, REAL|FLOAT, DOUBLE|FLOAT, DOUBLE|  
|DT_STR|char, varchar||varchar||char, varchar|char, varchar|  
|DT_UI1|TINYINT|TINYINT|Byte||||  
|DT_UI2|||||||  
|DT_UI4|||||||  
|DT_UI8|||||||  
|DT_WSTR|nchar, nvarchar, sql_variant, xml|char, varchar, nchar, nvarchar, sql_variant, xml|LongText|CHAR, ROWID, VARCHAR2, NVARCHAR2, NCHAR|GRAPHIC, VARGRAPHIC|GRAPHIC, VARGRAPHIC|  
|DT_IMAGE|image|image|LongBinary|LONG RAW, BLOB, LOBLOCATOR, BFILE, VARGRAPHIC, LONG VARGRAPHIC, definido pelo usuário|CHAR () FOR BIT DATA, VARCHAR () FOR BIT DATA|CHAR () FOR BIT DATA, VARCHAR () FOR BIT DATA, BLOB|  
|DT_NTEXT|ntext|text, ntext||LONG, CLOB, NCLOB, NVARCHAR, TEXT|LONG VARCHAR, NCHAR, NVARCHAR, TEXT|LONG VARCHAR, DBCLOB, NCHAR, NVARCHAR, TEXT|  
|DT_TEXT|text||||LONG VARCHAR FOR BIT DATA|LONG VARCHAR FOR BIT DATA, CLOB|  
  
 Para obter informações sobre o mapeamento de tipos de dados no fluxo de dados, consulte [Trabalhando com tipos de dados no fluxo de dados](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md).  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Entrada de blog, [Comparação de desempenho entre as técnicas de conversão de tipo de dados no SSIS 2008](https://go.microsoft.com/fwlink/?LinkId=220823), em blogs.msdn.com.  
  
## <a name="see-also"></a>Consulte Também  
 [Dados em fluxos de dados](../../integration-services/data-flow/data-in-data-flows.md)  
  
  
