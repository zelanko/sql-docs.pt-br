---
title: Análise de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- parsing [Integration Services]
- data parsing [Integration Services]
ms.assetid: 8893ea9d-634c-4309-b52c-6337222dcb39
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 71582dbdccc331ec4b43d87071952879f304395c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71292270"
---
# <a name="parsing-data"></a>Análise de dados

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Os fluxos de dados em pacotes extraem e carregam dados entre armazenamentos de dados heterogêneos, que podem usar uma variedade de tipos de dados padrão e personalizados. Em um fluxo de dados, as fontes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fazem o trabalho de extração dos dados, análise dos dados da cadeia de caracteres e conversão de dados para um tipo de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . As transformações subsequentes podem analisar os dados para convertê-los em um tipo diferente de dados ou para criar cópias de coluna com tipos diferentes de dados. As expressões usadas em componentes também podem lançar argumentos e operandos para os tipos diferentes de dados. Finalmente, quando os dados são carregados no repositório de dados, o destino pode analisar os dados para convertê-los em um tipo de dados usado pelo destino. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="two-types-of-parsing"></a>Dois tipos de análise  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece dois tipos de análises para conversão de dados: Análise rápida e Análise padrão.  
  
-   A análise rápida é um conjunto simples de rotinas de análise que não oferece suporte a conversões de tipos de dados específicas de localidade, e só oferece suporte aos formatos de data e hora usados com mais frequência. 
  
-   A análise padrão é um conjunto rico de rotinas de análise que oferecem suporte a todas as conversões de tipos de dados fornecidas pelas APIs de conversão de tipos de dados de Automação, disponíveis no Oleaut32.dll e Ole2dsip.dll.   
  
## <a name="fast-parse"></a>Fast Parse
A análise rápida fornece um conjunto de rotinas simples e rápidas para analisar dados. Essas rotinas não são sensíveis à localidade e aceitam apenas um subconjunto de formatos de data, hora e inteiro.  
  
### <a name="requirements-and-limitations"></a>Requisitos e limitações  
 Ao se implementar a análise rápida, o pacote perde sua habilidade para interpretar data, hora e dados numéricos em formatos específicos à localidade e em formatos ISO 8601 básicos e estendidos, mas o pacote melhora seu desempenho. Por exemplo, a análise rápida oferece suporte somente aos formatos mais comuns utilizados para representar data como YYYYMMDD e YYYY-MM-DD, não executa análise específica do local, não reconhece caracteres especiais em dados de moeda e não pode converter representação hexadecimal ou científica de inteiros.  
  
 A análise rápida só está disponível quando você usa o fonte Arquivo Simples ou a transformação de Conversão de Dados. O aumento no desempenho pode ser significativo e você pode considerar o uso da análise rápida nesses componentes de fluxo de dados se desejar.  
  
 Se o fluxo de dados no pacote requer análise sensível a localidade, a análise padrão é recomendada em lugar da análise rápida. Por exemplo, a análise rápida não reconhece dados sensíveis ao local, que incluem símbolos decimais como a vírgula, formatos de data que não sejam ano-mês-dia e símbolos de moeda.  
  
 Representações truncadas que implicam em uma ou mais partes da data, como um século, um ano ou um mês, não são reconhecidas pela análise rápida. Por exemplo, a análise rápida não reconhece o formato ' **-YYMM**', que especifica um ano e um mês em um século implícito, nem ' **--MM**', que especifica um mês em um ano implícito. Porém, algumas representações com precisão reduzida são reconhecidas. Por exemplo, a análise rápida reconhece o formato 'hhmm;', que indica somente hora e minuto e '**YYYY**', que indica somente o ano.  
  
 A análise rápida é especificada ao nível de coluna. Na fonte Flat File e na transformação de Conversão de Dados, você pode especificar a Análise rápida nas colunas de saída. Entradas e saídas podem incluir colunas sensíveis a local e colunas não sensíveis a local.  
 
## <a name="numeric-data-formats-fast-parse"></a>Formatos de dados numéricos (análise rápida)
A análise rápida fornece uma análise de dados rápida e simples a um conjunto de rotinas sem diferenciação de localidade. A análise rápida suporta apenas um conjunto limitado de formatos para tipos de dados de números inteiros.  
  
### <a name="integer-data-type"></a>Tipo de dados inteiros
 Os tipos de dados de números inteiros que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece são DT_I1, DT_UI1, DT_I2, DT_UI2, DT_I4, DT_UI4, DT_I8 e DT_UI8. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 A análise rápida suporta os seguintes formatos para tipos de dados de números inteiros:  
  
-   Zero com espaços à esquerda e à direita ou paradas de tabulação. Por exemplo, o valor "  123  " é válido. Um valor com espaços é avaliado como zero.  
  
-   Um sinal de mais, menos ou nenhum sinal. Por exemplo, os valores +123, -123 e 123 são válidos.  
  
-   Um ou mais números hindu-árabes (0-9). Por exemplo, o valor 345 é válido. Outros dados numéricos do idioma não são suportados.  
  
 Entre os formatos de dados que não são suportados estão:  
  
-   Caracteres especiais. Por exemplo, o símbolo de cifrão ($) não é suportado e o valor $20 não pode ser analisado.  
  
-   Caracteres com espaço em branco como quebra de linha, retornos de carro e espaços que não indicam uma quebra. Por exemplo, o valor " 123" não pode ser analisado.  
  
-   Representações hexadecimais de números inteiros. Por exemplo, o valor 2EE não pode ser analisado.  
  
-   Representação de notação científica de números inteiros. Por exemplo, o valor 1E+10 não pode ser analisado.  
  
 Os seguintes formatos são formatos de dados de saída para números inteiros:  
  
-   Um sinal de menos para números negativos e nenhum sinal para números positivos.  
  
-   Nenhum espaço em branco.  
  
-   Um ou mais números hindu-árabes (0-9).  

## <a name="date-and-time-formats-fast-parse"></a>Formatos de data e hora (análise rápida)
A análise rápida fornece um conjunto de rotinas simples e rápidas para analisar dados. A análise rápida oferece suporte aos seguintes formatos de tipos de dados de data e hora.  
  
### <a name="date-data-type"></a>Tipo de dados de data 
 A análise rápida oferece suporte aos seguintes formatos de cadeia de caracteres para dados de data:  
  
-   Formatos de data que incluem espaços em branco à esquerda. Por exemplo, o valor " 2004- 02-03" é válido.  
  
-   Os formatos ISO 8601, como listados na seguinte tabela:  
  
    |Formatar|DESCRIÇÃO|  
    |------------|-----------------|  
    |AAAAMMDD<br /><br /> AAAA-MM-DD|Os formatos básico e estendido para um ano de quatro dígitos, um mês de dois dígitos e um dia de dois dígitos. No formato estendido, as datas são separadas por um hífen (-).|  
    |AAAA-MM|Os formatos básico e estendido de precisão reduzida para um ano de quatro dígitos e um mês de dois dígitos. No formato estendido, as datas são separadas por um hífen (-).|  
    |AAAA|O formato de precisão reduzida é um ano de quatro dígitos.|  
  
 A análise rápida não oferece suporte aos seguintes formatos para dados de data:  
  
-   Valores de meses alfabéticos. Por exemplo, o formato de data Oct-31-2003 não é válido.  
  
-   Formatos ambíguos como DD-MM-AAAA e MM-DD-AAAA. Por exemplo, as datas 03-04-1995 e 04-03-1995  não são válidas.  
  
-   Os formatos básico e estendido truncados para um ano de calendário de quatro dígitos e um dia de três dígitos em um ano, AAAADDD e AAAA-DDD.  
  
-   Os formatos básico e estendido para um ano de quatro dígitos, um número de dois dígitos para a semana do ano e um número de um dígito para o dia da semana, AAAASssD e AAAA-Sss-D.  
  
-   Os formatos básico e estendido truncados para uma data de um ano e semana são um ano de quatro dígitos e um número de dois dígitos para a semana, AAASss e AAAA-Sss.  
  
 A análise efetua a saída dos dados como DT_DBDATE. Os valores de data em formatos truncados são convertidos. Por exemplo, AAAA se torna AAAA0101.  
  
 Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
### <a name="time-data-type"></a>Tipos de dados de tempo
 A análise rápida oferece suporte aos seguintes formatos de cadeia de caracteres para dados de hora:  
  
-   Formatos de hora que incluem espaços em branco à esquerda. Por exemplo, o valor " 10:24" é válido.  
  
-   Formato de 24 horas. A análise rápida não oferece suporte à notação AM e PM.  
  
-   Os formatos de hora ISO 8601, como listados na seguinte tabela:  
  
    |Formatar|DESCRIÇÃO|  
    |------------|-----------------|  
    |HHMISS<br /><br /> HH:MI:SS|Os formatos básico e estendido para uma hora de dois dígitos, um minuto de dois dígitos e um segundo de dois dígitos. No formato estendido, a hora é separada por dois pontos (:).|  
    |HHMI<br /><br /> HH:MI|Os formatos básico e estendido truncados para uma hora de dois dígitos e um minuto de dois dígitos. No formato estendido, a hora é separada por dois pontos (:).|  
    |HH|Formato truncado para uma hora de dois dígitos.|  
    |00:00:00<br /><br /> 000000<br /><br /> 0000<br /><br /> 00<br /><br /> 240000<br /><br /> 24:00:00<br /><br /> 2400<br /><br /> 24|O formato para meia-noite.|  
  
-   Os formatos de hora que especificam um fuso horário, como listados na seguinte tabela:  
  
    |Formatar|DESCRIÇÃO|  
    |------------|-----------------|  
    |+HH:MI<br /><br /> +HHMI|Os formatos básico e estendido que indicam o número de horas e minutos que são adicionados ao tempo universal coordenado (UTC) para obter a hora local.|  
    |-HH:MI<br /><br /> -HHMI|Os formatos básico e estendido que indicam o número de horas e minutos que são subtraídos do UTC para obter a hora local.|  
    |+HH|O formato truncado que indica o número de horas que são adicionadas ao UTC para obter a hora local.|  
    |-HH|O formato truncado que indica o número de horas que são subtraídas do UTC para obter a hora local.|  
    |Z|Um valor 0 que indica a hora é representado no UTC.|  
  
     Os formatos para todos os dados de hora e data/hora podem incluir um elemento de fuso horário. Porém, o sistema ignora o valor do fuso horário, exceto quando os dados são do tipo DT_DBTIMESTAMPOFFSET. Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
     Nos formatos que incluem um elemento de fuso horário, não há espaço entre o elemento de hora e o de fuso horário, como mostrado no seguinte exemplo:  
  
     HH:MI:SS[+HH:MI]  
  
     As chaves no exemplo anterior indicam que o valor do fuso horário é opcional.  
  
-   Os formatos de hora que incluem uma fração decimal, como listados na seguinte tabela:  
  
    |Formatar|DESCRIÇÃO|  
    |------------|-----------------|  
    |HH [.nnnnnnn]|n é um valor entre 0 e 9999999 que representa uma fração de horas. As chaves indicam que esse valor é opcional.<br /><br /> Por exemplo, o valor 12.750 indica 12:45.|  
    |HHMI [.nnnnnnn]<br /><br /> HH:MI [.nnnnnnn]|n é um valor entre 0 e 9999999 que representa uma fração de minutos. As chaves indicam que esse valor é opcional.<br /><br /> Por exemplo, o valor 1220.500 indica 12:20:30.|  
    |HHMISS [.nnnnnnn]<br /><br /> HH:MI:SS[.nnnnnnn]|n é um valor entre 0 e 9999999 que representa uma fração de segundos. As chaves indicam que esse valor é opcional.<br /><br /> Por exemplo, o valor 122040.250 indica 12:20:40.15.|  
  
    > [!NOTE]  
    >  O separador de fração para os formatos de hora na tabela anterior pode ser um decimal ou uma vírgula.  
  
-   Os valores de hora que incluem um segundo, como mostrado nos seguintes exemplos:  
  
     23:59:60[.0000000]  
  
     235960[.0000000]  
  
 A análise rápida efetua a saída de cadeias de caracteres como DT_DBTIME e DT_DBTIME2. Os valores de hora em formatos truncados são convertidos. Por exemplo, HH:MI se torna HH:MM:00 .000.  
  
 Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
### <a name="datetime-data-type"></a>Tipo de dados de data/hora  
 A análise rápida oferece suporte aos seguintes formatos de cadeia de caracteres para dados de data/hora:  
  
-   Formatos que incluem espaços em branco à esquerda. Por exemplo, o valor "  2003-01-10T203910" é válido.  
  
-   As combinações de formatos de data e de hora válidos separados por um T maiúsculo, e os formatos de fuso horário válidos, como AAAAMMDDT[HHMISS][+HH:MI]. Os valores de hora e de fuso horário não são obrigatórios. Por exemplo, "2003-10-14" são válidos.  
  
 A análise rápida não oferece suporte a intervalos de tempo. Por exemplo, um intervalo de tempo identificado por uma data e hora iniciais e finais no formato AAAAMMDDThhmmss/AAAAMMDDThhmmss não pode ser analisado.  
  
 A análise rápida efetua saídas das cadeias de caracteres como DT_DATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2 e DT_DBTIMESTAMPOFFSET. Os valores de data/hora em formatos truncados são convertidos. A tabela a seguir lista os valores que são adicionados nas partes de data e hora ausentes.  
  
|Parte de data e hora|Preenchimento|  
|---------------------|-------------|  
|Segundos|Adicione 00.|  
|minutos|Adicionar 00:00.|  
|Hora|Adicione 00:00:00.|  
|Dia|Adicione 01 para o dia do mês.|  
|Month|Adicione 01 para o mês do ano.|  
  
 Para obter mais informações, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="enable-fast-parse"></a>Habilitar análise rápida
A propriedade de análise rápida deve ser definida para cada coluna da origem ou transformação que use a análise rápida. Para definir a propriedade, use o Editor avançado da fonte Flat File e da transformação de Conversão de Dados.  
  
1.  Clique com o botão direito do mouse na fonte Arquivo Simples ou na transformação de Conversão de Dados e clique em **Mostrar Editor Avançado**.  
  
2.  Na caixa de diálogo **Editor Avançado** , clique na guia **Propriedades de Entrada e Saída** .  
  
3.  No painel **Entradas e Saídas** , clique na coluna para a qual você quer ativar a análise rápida.  
  
4.  Na janela Propriedades, expanda o nó **Propriedades Personalizadas** e defina a propriedade **FastParse** como **True**.  
  
5.  Clique em **OK**.  

## <a name="standard-parse"></a>Standard Parse
A análise padrão é um conjunto de rotinas de análise com diferenciação de localidade que oferece suporte a todas as conversões de tipos de dados fornecidas pelas APIs de conversão de tipos de dados de Automação disponíveis no Oleaut32.dll e Ole2dsip.dll. A análise padrão é equivalente às APIs de análise de OLE DB.  
  
 Ela oferece suporte para a conversão de tipo de dados de dados internacionais e pode ser usada caso o formato de dados não seja suportado pela análise rápida. Para obter mais informações sobre a API de conversão de tipo de dados de Automação, consulte "APIs de conversão de tipos de sados" na [Biblioteca MSDN](https://go.microsoft.com/fwlink/?LinkId=79427). 
 
