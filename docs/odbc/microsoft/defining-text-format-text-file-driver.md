---
title: Definir o formato de texto (Driver de arquivo de texto) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: 3af46dad-52cc-4d5c-a27e-6315d65a74e6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ed4eb087a11db45f2e3841b6e65824f1076d3693
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="defining-text-format-text-file-driver"></a>Definir o formato de texto (Driver de arquivo de texto)
Quando o driver de texto é usado, você pode usar o **definir formato de texto** caixa de diálogo para definir o formato das colunas em um arquivo selecionado. Essa caixa de diálogo permite que você especifique o esquema para cada tabela de dados. Essas informações são gravadas em um arquivo Schema.ini no diretório de origem de dados. Um arquivo Schema.ini separado é criado para cada diretório de fonte de dados de texto.  
  
> [!NOTE]  
>  O mesmo formato de arquivo padrão se aplica a todas as novas tabelas de dados de texto. Todos os arquivos criados pela instrução CREATE TABLE herdam os mesmos valores de formato padrão, que são definidos, selecionando valores de formato de arquivo no **definir formato de texto** caixa de diálogo com \<padrão > escolhido no **Tabelas** lista. O driver de texto não altera o formato de um arquivo de texto existente para corresponder ao formato definido na caixa de diálogo, mas retorna um erro quando ele usa o formato, como quando ele tenta recuperar os dados do arquivo de texto.  
  
 As seguintes opções estão disponíveis no **definir formato de texto** caixa de diálogo:  
  
|Opção|Informações|  
|------------|-----------------|  
|**Adicionar**|Adiciona uma coluna usando os valores na **tipo de dados**, **nome**, e **largura** da caixa de diálogo e, se aplicável, o separador de data do valor de Schema.|  
|**Caracteres**|**ANSI** ou **OEM**. OEM Especifica um conjunto de caracteres não-ANSI. O padrão é OEM se o formato do item selecionado no **tabelas** lista não foi definida anteriormente por essa caixa de diálogo.|  
|**Cabeçalho da coluna**|Indica se as colunas da primeira linha da tabela selecionada serão usadas como nomes de coluna. O **TRUE** ou **FALSE**. Valor padrão é FALSE se o formato do item selecionado no **tabelas** lista não foi definida anteriormente por essa caixa de diálogo.|  
|**Colunas**|Lista os nomes de coluna para cada coluna na tabela selecionada. A ordem das colunas reflete a ordem das colunas na tabela. Essa lista estará habilitada se um arquivo tiver sido selecionado no **tabelas** lista.|  
|**Tipo de Dados**|Pode ser BIT, BYTE, CHAR, moeda, data, FLOAT, INTEGER, LONGCHAR, CURTO ou único. Tipos de dados de data podem ser nos seguintes formatos: "dd-mmm-aa", "mm-dd-aa", "mmm-dd-aa", "aaaa-mm-dd" ou "aaaa-mmm-dd". "mm" refere números para os meses. "mmm" refere letras para os meses.|  
|**Delimitador**|Especifica o caractere delimitador personalizado a ser usado para separar colunas. Habilitado quando o **personalizado delimitada** formato está selecionado. O delimitador pode ser somente um caractere de comprimento e aspas duplas (") não pode ser usadas como o caractere delimitador. (O delimitador não pode ser especificado em formato hexadecimal ou decimal).|  
|**Formato**|Comprimento fixo ou delimitado. Se delimitada, indica o tipo de delimitador usado: vírgula (CSV), tabulação ou caractere especial (personalizado). O padrão é **CSV delimitado** se o formato do item selecionado no **tabelas** lista não foi definida anteriormente por essa caixa de diálogo.<br /><br /> Se **formato** é de comprimento fixo e **cabeçalho da coluna** for TRUE, a primeira linha deve ser delimitada por vírgulas.|  
|**Estimativa**|Gera automaticamente os valores da coluna largura, nome e tipo de dados para as colunas na tabela selecionada, examinando o conteúdo da tabela de acordo com o **formato** caixa de seleção. Habilitado quando o formato de tabela é delimitado. Colunas em qualquer definidas anteriormente o **colunas** lista são limpas e substituídas por novas entradas. Se **cabeçalho da coluna** não é selecionada, os nomes de coluna são gerados automaticamente como "F1", "F2" e assim por diante. Nenhum valor padrão é mostrado no **tipo de dados** caixa.<br /><br /> Essa funcionalidade só funciona em colunas que são menores do que 64,513 bytes.|  
|**Modificar**|Modifica a coluna selecionada usando os valores na **tipo de dados**, **nome**, e **largura**.|  
|**Nome**|Exibe o nome da coluna selecionada. Pode ser usado para especificar um novo nome de coluna para uma coluna existente ou uma nova coluna.<br /><br /> Se **cabeçalho da coluna** for TRUE, a coluna nome exibido será ignorado.|  
|**Remover**|Exclui a coluna selecionada.|  
|**Linhas de varredura**|O número de linhas que o programa de instalação ou o driver examinará quando definir as colunas e tipos de dados de coluna com base em dados existentes.<br /><br /> Você pode inserir um número de 1 a 32767 para o número de linhas a serem examinadas. O padrão é 25 se o formato do item selecionado no **tabelas** lista não foi definida anteriormente por essa caixa de diálogo. (Um número fora do limite retornará um erro.)|  
|**Tabelas**|Contém uma lista de todos os arquivos no diretório selecionado no **texto instalação** caixa de diálogo que corresponde à lista de extensões especificadas.<br /><br /> Quando \<padrão > está selecionada, e um dos seguintes for verdadeiro, os valores dos atributos na tabela de **tabelas** grupo são gravados no Schema (sem outras entradas no Schema são tocadas):<br /><br /> -Não há nenhum Schema no diretório especificado.<br />-O arquivo Schema existe, mas não há uma seção Schema para um dos arquivos de texto (com a extensão especificada) no diretório.<br />-A seção de um arquivo de texto existe no Schema, mas o corpo está vazio.<br /><br /> Quando \<padrão > estiver selecionada, o **colunas** grupo está desabilitado.|  
|**Largura**|A largura da coluna pode ser alterada para colunas CHAR ou LONGCHAR. A largura padrão é 1 se o formato do item selecionado no **tabelas** lista não foi definida anteriormente por essa caixa de diálogo.<br /><br /> Para outros tipos de dados, o controle de largura é desabilitado e nenhum valor é exibido.|

