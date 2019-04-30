---
title: Definindo o formato de texto (Driver de arquivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: 3af46dad-52cc-4d5c-a27e-6315d65a74e6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00d20f8a6dd4d79b3100549d9286e7534bc8ce6e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240378"
---
# <a name="defining-text-format-text-file-driver"></a>Definir o formato de texto (Driver de Arquivo de texto)
Quando o driver de texto é usado, você pode usar o **definir o formato de texto** caixa de diálogo para definir o formato para colunas em um arquivo selecionado. Essa caixa de diálogo permite que você especifique o esquema para cada tabela de dados. Essa informação é gravada em um arquivo Schema. ini no diretório de fonte de dados. Um arquivo Schema. ini separado é criado para cada diretório de fonte de dados de texto.  
  
> [!NOTE]  
>  O mesmo formato de arquivo padrão se aplica a todas as novas tabelas de dados de texto. Todos os arquivos criados pela instrução CREATE TABLE herdam esses mesmos valores de formato padrão, que são definidos, selecionando valores de formato de arquivo na **definir o formato de texto** caixa de diálogo com \<padrão > escolhido na **Tabelas** lista. O driver de texto não altera o formato de um arquivo de texto existente para corresponder ao formato definido na caixa de diálogo, mas retorna um erro quando ele usa o formato, como quando ele tenta recuperar dados do arquivo de texto.  
  
 As seguintes opções estão disponíveis na **definir o formato de texto** caixa de diálogo:  
  
|Opção|Informações|  
|------------|-----------------|  
|**Adicionar**|Adiciona uma coluna usando os valores na **tipo de dados**, **nome**, e **largura** na caixa de diálogo, e se aplicável, o separador de data do valor de Schema. ini.|  
|**Caracteres**|**ANSI** ou **OEM**. OEM Especifica um conjunto de caracteres não-ANSI. O padrão será OEM se o formato do item selecionado na **tabelas** lista não foi definida anteriormente por esta caixa de diálogo.|  
|**Cabeçalho da coluna**|Indica se as colunas da primeira linha da tabela selecionada devem ser usadas como nomes de coluna. Qualquer um dos **verdadeira** ou **falso**. O padrão é falso se o formato do item selecionado na **tabelas** lista não foi definida anteriormente por esta caixa de diálogo.|  
|**Colunas**|Lista os nomes de coluna para cada coluna na tabela selecionada. A ordem das colunas reflete a ordem das colunas na tabela. Essa lista estará habilitada se um arquivo tiver sido selecionado na **tabelas** lista.|  
|**Tipo de Dados**|Pode ser BIT, BYTE, CHAR, moeda, data, FLOAT, INTEGER, LONGCHAR, CURTO ou único. Tipos de dados de data podem ser nos seguintes formatos: "dd-mmm-aa", "mm-dd-aa", "mmm-dd-aa", "aaaa-mm-dd" ou "aaaa-mmm-dd". "mm" indica os números por meses. "mmm" refere letras para os meses.|  
|**delimitador**|Especifica o caractere delimitador personalizado a ser usado para separar as colunas. Habilitado quando o **personalizado delimitados** formato está selecionado. O delimitador pode ser somente um caractere de comprimento e aspas duplas (") não pode ser usadas como o caractere delimitador. (O delimitador não pode ser especificado em formato hexadecimal ou decimal).|  
|**Formato**|Comprimento fixo ou delimitado. Se estiver limitado, indica o tipo de delimitador usado: vírgula (CSV), tabulação ou caractere especial (personalizado). O padrão será **CSV delimitados** se o formato do item selecionado na **tabelas** lista não foi definida anteriormente por esta caixa de diálogo.<br /><br /> Se **formato** é o comprimento fixo e **cabeçalho da coluna** for TRUE, a primeira linha deve ser delimitada por vírgulas.|  
|**Estimativa**|Gera automaticamente os valores da coluna largura, nome e tipo de dados para as colunas na tabela selecionada, examinando o conteúdo da tabela de acordo com o **formato** caixa de seleção. Habilitado quando o formato de tabela é delimitado. Colunas em qualquer definidas anteriormente a **colunas** lista são limpas e substituídas por novas entradas. Se **cabeçalho da coluna** não é selecionada, os nomes de coluna são gerados automaticamente como "F1", "F2" e assim por diante. Nenhum valor padrão é mostrado na **tipo de dados** caixa.<br /><br /> Essa funcionalidade funciona apenas em colunas que são menos 64,513 bytes.|  
|**Modificar**|Modifica a coluna selecionada usando os valores na **tipo de dados**, **nome**, e **largura**.|  
|**Nome**|Exibe o nome da coluna selecionada. Pode ser usado para especificar um novo nome de coluna para uma coluna existente ou uma nova coluna.<br /><br /> Se **cabeçalho da coluna** for TRUE, a coluna nome exibido é ignorado.|  
|**Remover**|Exclui a coluna selecionada.|  
|**Linhas de varredura**|O número de linhas que a instalação ou o driver examinará ao definir as colunas e tipos de dados de coluna com base nos dados existentes.<br /><br /> Você pode inserir um número de 1 a 32767 para o número de linhas a serem examinadas. Esse padrão é 25 se o formato do item selecionado na **tabelas** lista não foi definida anteriormente por esta caixa de diálogo. (Um número fora do limite retornará um erro.)|  
|**Tabelas**|Contém uma lista de todos os arquivos no diretório selecionado na **configuração de texto** caixa de diálogo que correspondem à lista de extensões especificadas.<br /><br /> Quando \<padrão > estiver selecionada, e um dos seguintes for verdadeiro, os valores dos atributos na tabela o **tabelas** grupo são gravados no Schema. ini (não há outras entradas no Schema. ini são tocadas):<br /><br /> -Não há nenhum Schema. ini no diretório especificado.<br />-O arquivo Schema. ini existir, mas há uma seção no Schema. ini para um dos arquivos de texto (com a extensão especificada) no diretório.<br />-A seção para um arquivo de texto existe no Schema. ini, mas o corpo está vazio.<br /><br /> Quando \<padrão > estiver selecionada, o **colunas** grupo está desabilitado.|  
|**Width**|A largura da coluna pode ser alterada para colunas CHAR ou LONGCHAR. A largura padrão é 1 se o formato do item selecionado na **tabelas** lista não foi definida anteriormente por esta caixa de diálogo.<br /><br /> Para outros tipos de dados, o controle de largura é desabilitado e nenhum valor é exibido.|
