---
title: Definindo o formato do texto (driver de arquivo de texto) | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307657"
---
# <a name="defining-text-format-text-file-driver"></a>Definir o formato de texto (Driver de Arquivo de texto)
Quando o driver texto é usado, você pode usar a caixa de diálogo **Definir formato** de texto para definir o formato das colunas em um arquivo selecionado. Esta caixa de diálogo permite que você especifique o esquema para cada tabela de dados. Essas informações são escritas em um arquivo Schema.ini no diretório de origem de dados. Um arquivo Schema.ini separado é criado para cada diretório de origem de dados de texto.  
  
> [!NOTE]  
>  O mesmo formato de arquivo padrão se aplica a todas as novas tabelas de dados de texto. Todos os arquivos criados pela declaração CREATE TABLE herdam esses mesmos valores de formato \<padrão, que são definidos selecionando valores de formato de arquivo na caixa de diálogo Definir formato de **texto** com> padrão escolhida na lista **Tabelas.** O driver Texto não altera o formato de um arquivo de texto existente para corresponder ao formato definido nesta caixa de diálogo, mas retorna um erro quando ele usa o formato, como quando ele tenta recuperar dados do arquivo de texto.  
  
 As seguintes opções estão disponíveis na caixa de diálogo **Definir formato de texto:**  
  
|Opção|Informações|  
|------------|-----------------|  
|**Adicionar**|Adiciona uma coluna usando os valores em **Tipo de Dados,** **Nome**e **Largura** da caixa de diálogo e, se aplicável, o valor separador de data saqueado de Schema.ini.|  
|**Caracteres**|**ANSI** ou **OEM**. OEM especifica um conjunto de caracteres não-ANSI. Isso é padrão para OEM se o formato do item selecionado na lista **Tabelas** não tiver sido definido anteriormente por esta caixa de diálogo.|  
|**Cabeçalho do nome da coluna**|Indica se as colunas da primeira linha da tabela selecionada devem ser usadas como nomes de coluna. **SEJA VERDADEIRO** OU **FALSO**. Padrão para FALSO se o formato do item selecionado na lista **Tabelas** não tiver sido definido anteriormente por esta caixa de diálogo.|  
|**Colunas**|Lista os nomes das colunas para cada coluna na tabela selecionada. A ordem das colunas reflete a ordem das colunas na tabela. Esta lista está ativada se um arquivo tiver sido selecionado na lista **Tabelas.**|  
|**Tipo de dados**|Pode ser BIT, BYTE, CHAR, CURRENCY, DATE, FLOAT, INTEGER, LONGCHAR, SHORT ou SINGLE. Os tipos de dados de data podem estar nos seguintes formatos: "dd-mmm-yy", "mm-dd-yy", "mmm-dd-yy", "yyyy-mm-dd" ou "yyyy-mmm-dd". "mm" denota números por meses; "mmm" denota cartas por meses.|  
|**Delimitador**|Especifica o caractere delimitador personalizado a ser usado para separar colunas. Ativado quando o formato **Personalizado Delimitado** for selecionado. O delimitador pode ser apenas um caractere de comprimento, e aspas duplas (") não podem ser usadas como o caractere delimitador. (O delimitador não pode ser especificado em formato hexadecimal ou decimal.)|  
|**Formato**|Comprimento delimitado ou fixo. Se delimitado, indica o tipo de delimitador usado: vírgula (CSV), guia ou caractere especial (personalizado). Isso é padrão para **CSV Delimitado** se o formato do item selecionado na lista **Tabelas** não tiver sido definido anteriormente por esta caixa de diálogo.<br /><br /> Se **o formato** for de comprimento fixo e o **cabeçalho do nome da coluna** for TRUE, a primeira linha deve ser delimitada por vírgulas.|  
|**Adivinhar**|Gera automaticamente os valores de tipo, nome e largura da coluna para as colunas na tabela selecionada, digitalizando o conteúdo da tabela de acordo com a seleção da caixa **Formato.** Ativado quando o formato da tabela é delimitado. Todas as colunas previamente definidas na lista Colunas são **limpas** e substituídas por novas entradas. Se **o Cabeçalho de Nome da Coluna** não estiver selecionado, os nomes das colunas serão gerados automaticamente como "F1", "F2" e assim por diante. Nenhum valor padrão é mostrado na caixa **Tipo de dados.**<br /><br /> Essa funcionalidade funciona apenas em colunas inferiores a 64.513 bytes.|  
|**Modificar**|Modifica a coluna selecionada usando os valores em **Tipo de Dados,** **Nome**e **Largura**.|  
|**Nome**|Exibe o nome da coluna selecionada. Pode ser usado para especificar um novo nome de coluna para uma coluna existente ou uma nova coluna.<br /><br /> Se **o cabeçalho de nome da coluna** for VERDADEIRO, o nome da coluna exibido será ignorado.|  
|**Remover**|Exclui a coluna selecionada.|  
|**Linhas para Escanear**|O número de linhas que configuram ou o driver serão escaneados ao definir as colunas e os tipos de dados da coluna com base nos dados existentes.<br /><br /> Você pode inserir um número de 1 a 32767 para o número de linhas a serem escaneadas. Isso é padrão para 25 se o formato do item selecionado na lista **Tabelas** não tiver sido definido anteriormente por esta caixa de diálogo. (Um número fora do limite retornará um erro.)|  
|**Tabelas**|Contém uma lista de todos os arquivos no diretório selecionados na caixa de diálogo **Configuração** de texto que correspondem à lista de extensões especificadas.<br /><br /> Quando \<o> padrão é selecionado e um dos seguintes é verdadeiro, os valores dos atributos de tabela no grupo **Tabelas** são escritos para Schema.ini (nenhuma outra entrada em Schema.ini é tocada):<br /><br /> - Não há nenhum Esquema.ini no diretório especificado.<br />- O arquivo Schema.ini existe, mas não há nenhuma seção em Schema.ini para um dos arquivos text (com a extensão especificada) no diretório.<br />- A seção de um arquivo texto existe em Schema.ini, mas o corpo está vazio.<br /><br /> Quando \<o> padrão é selecionado, o grupo **Colunas** é desativado.|  
|**Largura**|A largura da coluna pode ser alterada para colunas CHAR ou LONGCHAR. A largura é padrão para 1 se o formato do item selecionado na lista **Tabelas** não tiver sido definido anteriormente por esta caixa de diálogo.<br /><br /> Para outros tipos de dados, o controle de largura é desativado e nenhum valor é exibido.|
