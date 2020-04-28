---
title: Definindo o formato de texto (driver de arquivo de texto) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 29dc46525f3c81e5abffe5076988716a01df06df
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307657"
---
# <a name="defining-text-format-text-file-driver"></a>Definir o formato de texto (Driver de Arquivo de texto)
Quando o driver de texto é usado, você pode usar a caixa de diálogo **definir formato de texto** para definir o formato das colunas em um arquivo selecionado. Essa caixa de diálogo permite que você especifique o esquema para cada tabela de dados. Essas informações são gravadas em um arquivo Schema. ini no diretório de fonte de dados. Um arquivo Schema. ini separado é criado para cada diretório de fonte de dados de texto.  
  
> [!NOTE]  
>  O mesmo formato de arquivo padrão se aplica a todas as novas tabelas de dados de texto. Todos os arquivos criados pela instrução CREATE TABLE herdam os mesmos valores de formato padrão, que são definidos selecionando-se os valores de formato de arquivo na \<caixa de diálogo **definir formato de texto** com o padrão> escolhido na lista **tabelas** . O driver de texto não altera o formato de um arquivo de texto existente para corresponder ao formato definido nessa caixa de diálogo, mas retorna um erro quando ele usa o formato, como quando ele tenta recuperar dados do arquivo de texto.  
  
 As opções a seguir estão disponíveis na caixa de diálogo **definir formato de texto** :  
  
|Opção|Informações|  
|------------|-----------------|  
|**Adicionar**|Adiciona uma coluna usando os valores em **tipo de dados**, **nome**e **largura** da caixa de diálogo e, se aplicável, o valor do separador de data de Schema. ini.|  
|**Personagens**|**ANSI** ou **OEM**. O OEM especifica um conjunto de caracteres não-ANSI. O padrão será o OEM se o formato do item selecionado na lista **tabelas** não tiver sido definido anteriormente por essa caixa de diálogo.|  
|**Cabeçalho de nome de coluna**|Indica se as colunas da primeira linha da tabela selecionada devem ser usadas como nomes de coluna. **True** ou **false**. O padrão será FALSE se o formato do item selecionado na lista **tabelas** não tiver sido definido anteriormente por essa caixa de diálogo.|  
|**Colunas**|Lista os nomes de coluna para cada coluna na tabela selecionada. A ordem das colunas reflete a ordem das colunas na tabela. Essa lista será habilitada se um arquivo tiver sido selecionado na lista **tabelas** .|  
|**Tipo de dados**|Pode ser BIT, BYTE, CHAR, CURRENCY, DATE, FLOAT, inteiro, LONGCHAR, SHORT ou SINGLE. Os tipos de dados de data podem estar nos seguintes formatos: "dd-mmm-aa", "mm-dd-aa", "Mmm-dd-aa", "aaaa-mm-dd" ou "aaaa-Mmm-dd". "mm" denota números de meses; "Mmm" denota letras para meses.|  
|**Delimitador**|Especifica o caractere delimitador personalizado a ser usado para separar colunas. Habilitado quando o formato **delimitado personalizado** é selecionado. O delimitador pode ter apenas um caractere de comprimento e aspas duplas (") não podem ser usadas como caractere delimitador. (O delimitador não pode ser especificado no formato hexadecimal ou Decimal.)|  
|**Ao**|Comprimento delimitado ou fixo. Se delimitado, indica o tipo de delimitador usado: vírgula (CSV), tabulação ou caractere especial (personalizado). O padrão será **delimitado por CSV** se o formato do item selecionado na lista **tabelas** não tiver sido definido anteriormente por essa caixa de diálogo.<br /><br /> Se o **formato** for de comprimento fixo e o **cabeçalho de nome de coluna** for true, a primeira linha deverá ser delimitada por vírgula.|  
|**Só**|Gera automaticamente os valores de tipo de dados, nome e largura da coluna para as colunas na tabela selecionada examinando o conteúdo da tabela de acordo com a seleção da caixa de **formato** . Habilitado quando o formato de tabela é delimitado. Todas as colunas definidas anteriormente na lista **colunas** são limpas e substituídas por novas entradas. Se o **cabeçalho de nome de coluna** não for selecionado, os nomes de coluna serão gerados automaticamente como "F1", "F2" e assim por diante. Nenhum valor padrão é mostrado na caixa **tipo de dados** .<br /><br /> Essa funcionalidade funciona apenas em colunas com menos de 64.513 bytes.|  
|**Modificar**|Modifica a coluna selecionada usando os valores em **tipo de dados**, **nome**e **largura**.|  
|**Nome**|Exibe o nome da coluna selecionada. Pode ser usado para especificar um novo nome de coluna para uma coluna existente ou para uma nova coluna.<br /><br /> Se o **cabeçalho do nome da coluna** for true, o nome da coluna exibido será ignorado.|  
|**Remover**|Exclui a coluna selecionada.|  
|**Linhas a serem verificadas**|O número de linhas que o programa de instalação ou o driver verificará ao definir as colunas e os tipos de dados de coluna com base nos dados existentes.<br /><br /> Você pode inserir um número de 1 a 32767 para o número de linhas a serem verificadas. O padrão é 25 se o formato do item selecionado na lista **tabelas** não tiver sido definido anteriormente por essa caixa de diálogo. (Um número fora do limite retornará um erro.)|  
|**Tabelas**|Contém uma lista de todos os arquivos no diretório selecionado na caixa de diálogo **configuração de texto** que correspondem à lista de extensões especificadas.<br /><br /> Quando \<a> padrão é selecionada e uma das seguintes opções é verdadeira, os valores dos atributos de tabela no grupo **tabelas** são gravados em Schema. ini (nenhuma outra entrada em Schema. ini é tocadas):<br /><br /> -Não há nenhum Schema. ini no diretório especificado.<br />-O arquivo Schema. ini existe, mas não há nenhuma seção em Schema. ini para um dos arquivos de texto (com a extensão especificada) no diretório.<br />-A seção de um arquivo de texto existe em Schema. ini, mas o corpo está vazio.<br /><br /> Quando \<a> padrão é selecionada, o grupo **colunas** é desabilitado.|  
|**Largura**|A largura da coluna pode ser alterada para colunas CHAR ou LONGCHAR. A largura padrão será 1 se o formato do item selecionado na lista **tabelas** não tiver sido definido anteriormente por essa caixa de diálogo.<br /><br /> Para outros tipos de dados, o controle de largura é desabilitado e nenhum valor é exibido.|
