---
title: Janelas Localizar Resultados | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vs.findresults1
- findresultswindow
- vs.findresults2
helpviewer_keywords:
- Find Results Windows dialog box
ms.assetid: 3b68dbb7-26d6-4bc9-bd2c-c27e5dc385c3
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 721da2d2aa2731427455a30a1d691f1a644d95a0
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43067544"
---
# <a name="find-results-windows"></a>Janelas Localizar Resultados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  As duas janelas Localizar Resultados exibem correspondências encontradas usando a guia **Localizar em Arquivos** ou **Substituir em Arquivos** de caixa de diálogo **Localizar e Substituir** . O comando **Opções de Resultados** para **Localizar em Arquivos** e **Substituir em Arquivos** permite que você escolha a janela Localizar Resultados onde serão listadas as correspondências encontradas.  
  
 A janela Localizar Resultados selecionada abre automaticamente sempre que são encontradas correspondências. Para exibir uma janela Localizar Resultados manualmente, clique em **Outras Janelas** no menu **Exibir** e clique em **Localizar Resultados 1** ou **Localizar Resultados 2**.  
  
 Para exibir o arquivo de código e ir para a linha onde ocorre uma correspondência, clique duas vezes em qualquer linha na lista de resultados. O arquivo de origem é exibido no Editor de Códigos com o ponto de inserção localizado onde o texto correspondente começa. Um símbolo aparece na margem do indicador do editor para marcar a linha que inclui a correspondência, e a barra de status exibe o texto completo.  
  
## <a name="toolbar-buttons"></a>Botões da Barra de ferramentas  
 Os botões da barra de ferramentas a seguir estão disponíveis para ajudá-lo a examinar a lista de resultados e ir para linhas no seu código onde foram encontradas as correspondências.  
  
 **sinalizador de página + seta para cima**  
 Vá para a linha onde foi encontrada a correspondência selecionada.  
  
 **página + seta para a esquerda**  
 Vá para a linha da correspondência anterior.  
  
 **página + seta para a direita**  
 Vá para a linha da próxima correspondência.  
  
 **Limpar tudo**  
 Remova todas as correspondências da lista de **Resultados** .  
  
## <a name="shortcut-keys"></a>Teclas de atalho  
 As teclas de atalho a seguir estão disponíveis para ajudá-lo a navegar rapidamente nas correspondências encontradas.  
  
 CTRL+HOME  
 Role até a parte superior da janela Localizar Resultados.  
  
 CTRL+END  
 Role até a parte inferior da janela Localizar Resultados.  
  
 PAGE UP  
 Role para cima até o próximo grupo de correspondências.  
  
 PAGE DOWN  
 Role para baixo até o próximo grupo de correspondências.  
  
 SETA PARA CIMA  
 Selecione a correspondência anterior.  
  
 SETA PARA BAIXO  
 Selecione a próxima correspondência.  
  
## <a name="search-result-entries"></a>Pesquisar entradas de resultados  
 Cada entrada na lista de resultados fornece as seguintes informações:  
  
-   Caminho completo  
  
-   Nome do arquivo  
  
-   Line number  
  
-   O texto completo da linha que contém a correspondência  
  
> [!TIP]  
>  Você pode usar **Localização Rápida** para examinar uma longa lista de resultados. Abra e encaixe a janela Localizar Resultados e clique no botão triangular **Exibir** na guia **Localizar** e altere para **Localização Rápida**. Defina o campo **Examinar** da pesquisa como **Janela Ativa**, digite uma cadeia de caracteres em **Localizar** e clique em **Localizar Próximo**. Isso permite que você examine a lista de resultados para correspondências encontradas em pastas ou arquivos específicos ou correspondências em linhas de código onde outro termo importante também ocorre.  
  
## <a name="summary-lines"></a>Linhas de resumo  
 Cada conjunto de resultados de pesquisa começa com uma linha que informa os parâmetros da pesquisa e termina com uma linha de estatística. Por exemplo, a lista de resultados de uma pesquisa **Localizar em Arquivos** em todos os documentos abertos para todas as cadeias de caracteres correspondentes à expressão regular "`var[1-3]&par`" deve começar com essa linha de parâmetros de pesquisa:  
  
 `Find all "var[1-3]&par" Regular Expression, All Open Documents`  
  
 e pode encerrar com essa linha de estatística:  
  
 `Total found: 57  Matching files: 23  Total files searched: 59`  
  
 A lista de resultados de uma pesquisa **Substituir em Arquivos** em todos os documentos abertos que substituíram todas as cadeias de caracteres correspondentes à expressão regular "`var[1-3]&par`" com a cadeia de caracteres "`sample`" que pode começar com essa linha de parâmetros de pesquisa:  
  
 `Replace "var[1-3]&par", "sample", Regular Expression, All Open Documents`  
  
 e pode encerrar com essa linha de estatística:  
  
 `Total replaced: 57  Matching files: 23  Total files searched: 59`  
  
  
