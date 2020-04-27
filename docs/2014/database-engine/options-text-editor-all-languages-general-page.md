---
title: Opções (página Editor de texto – todos os idiomas – geral) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: bf18907c-94e2-4c09-9b2b-0925ac04c627
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 385380e6e51c3b8519e7dbc6ec3d934e1ef14846
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089245"
---
# <a name="options-text-editor---all-languages---general-page"></a>Opções (página Editor de texto – Todos os idiomas – Geral)
  Use esta caixa de diálogo para definir as opções de edição gerais nos cinco editores no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Para exibir essas opções, clique em **Opções** no menu **Ferramentas** . Selecione a pasta **Editor de Texto**, expanda a pasta **Todos os Idiomas** e clique em **Geral**.  
  
## <a name="option-settings-by-editor"></a>Configurações de opção por editor  
 Use a caixa de diálogo **Todos os Idiomas** para definir opções para os editores DMX, MDX e SQL Server Compact. As opções definidas aqui também são aplicadas aos editores de Texto sem formatação, de Transact-SQL e de XML, mas você pode definir opções separadamente para esses editores, expandindo as subpastas para esses idiomas e selecionando as respectivas páginas de opção.  
  
> [!CAUTION]  
>  Se você definir uma opção que use essa caixa de diálogo, mas desejar uma configuração diferente para o editor de Texto sem Formatação, de Transact-SQL ou de XML, defina as opções para esses editores depois de aplicar suas seleções na caixa de diálogo **Todos os Idiomas**.  
  
 Alguns editores talvez não ofereçam suporte a todas as opções listadas nesta página. Uma marca de seleção sombreada é exibida quando uma opção foi selecionada na página **Geral** da caixa de diálogo **Opções** para algumas linguagens de programação, mas não para outras.  
  
## <a name="statement-completion"></a>Conclusão de instrução  
 **Listar membros automaticamente**  
 Exibe listas pop-up de membros, propriedades ou valores disponíveis enquanto se digita no editor. Escolha qualquer item na lista pop-up para inserir o item em seu código. Marcar essa caixa de seleção habilita a opção **Ocultar membros avançados**.  
  
 **Ocultar membros avançados**  
 Reduz as listas pop-up de instrução de conclusão exibindo apenas os itens mais usados. Os outros itens são filtrados da lista. Essa opção não estará disponível se nenhum membro for marcado como membros avançados.  
  
 **Informações sobre parâmetros**  
 Exibe a sintaxe completa da declaração ou procedimento atual à esquerda do ponto de inserção no editor com todos os seus parâmetros disponíveis. O próximo parâmetro que você pode atribuir é exibido em negrito.  
  
## <a name="settings"></a>Configurações  
 **Habilitar espaço virtual**  
 Posiciona comentários em um ponto consistente próximo ao seu código. Quando essa caixa de seleção é marcada, você pode posicionar o cursor além do último caractere na linha. Quando você digita, tabulações ou espaços são adicionados automaticamente para completar a linha para o ponto de inserção.  
  
 **Quebra automática de palavra**  
 Exiba na próxima linha qualquer parte de uma linha que ultrapasse horizontalmente a área do editor visível. Marcar essa caixa de seleção habilita a opção **Exibir marcas visuais nas quebras automáticas de linha** .  
  
 **Mostrar glifos visuais para quebra automática de linha**  
 Exibe um indicador de seta de retorno no ponto em que uma linha longa é quebrada em uma segunda linha.  
  
> [!NOTE]  
>  Essas setas indicadoras não são adicionadas ao seu código e não aparecem na impressão. Eles são somente para referência. Esse recurso não está disponível em todos os tipos de editores.  
  
 **Aplicar comandos Recortar/Copiar a linhas em branco quando não houver seleção**  
 Defina o comportamento do editor ao colocar o ponto de inserção em uma linha em branco, não selecione nada e clique em **Copiar** ou **Recortar**.  
  
 Quando essa caixa de seleção está marcada, a linha em branco é copiada ou recortada. Se você clicar em **Colar**, uma nova linha em branco será inserida.  
  
 Quando essa caixa de seleção é desmarcada, nada é copiado nem recortado. Se você clicar em **Colar**, o conteúdo mais recentemente copiado será colado. Se nada foi copiado, nada será colado.  
  
 Essa configuração não tem efeito sobre os comandos **Copiar** ou **Recortar** quando uma linha não está em branco. Se nada for selecionado, a linha inteira será copiada ou recortada. Se você clicar em **Colar**, o texto da linha inteira e seu caractere de término serão colados.  
  
## <a name="display"></a>Exibição  
 **Números de linha**  
 Exibe um número de linha próximo a cada linha de código.  
  
> [!NOTE]  
>  Esses números de linha não são adicionados ao seu código e não aparecem na impressão. Eles são somente para referência.  
  
 **Habilitar navegação de URL com um só clique**  
 Altera o cursor para um símbolo de mão apontando ao passar sobre uma URL no editor. Você pode clicar no URL para exibir a página indicada em seu navegador da Web.  
  
 **Barra de navegação**  
 Exibe uma barra de navegação no topo do Editor de Códigos. Use suas listas suspensas de **Objetos** e **Procedimentos** para escolher um objeto específico no código, selecionar em seus procedimentos e inserir uma instância do procedimento selecionado. A barra de navegação não está disponível para todos os tipos de código.  
  
  
