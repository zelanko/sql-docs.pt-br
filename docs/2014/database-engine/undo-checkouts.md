---
title: Desfazer check-outs | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VisualStudio.SourcControl.UndoCheckDialog
helpviewer_keywords:
- checking out files
- checkout source controls [SQL Server]
- undoing checkouts
ms.assetid: a6596b20-3aa5-4dc4-a4c5-3649f1f5a20e
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 00662ef396ff114e4b77d70aa2f60863e8f94bd3
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84927839"
---
# <a name="undo-checkouts"></a>Desfazer check-outs
  Você pode usar o comando **Desfazer check-out** para cancelar um check-out existente. Isso é particularmente útil quando você tiver modificado e salvado um arquivo, e depois precisar reverter as alterações.  
  
 Dependendo das opções definidas na caixa de diálogo **Opções Avançadas de Desfazer Check-Out** , o ambiente do Studio deixa a cópia de trabalho do item no disco local ou a substitui pela versão com controle do código-fonte mais recente. Se alguém tiver modificado o item fora do contexto do sistema de controle do código-fonte, a versão recuperada talvez não seja a mais recente.  
  
### <a name="to-undo-a-checkout"></a>Para desfazer um check-out  
  
1.  No Gerenciador de Soluções, selecione o projeto.  
  
2.  No menu **Arquivo** , aponte para **Controle do Código-Fonte**e clique em **Desfazer Check-out**.  
  
3.  Na caixa de diálogo **Desfazer Check-out** , selecione as opções apropriadas e clique no botão **Desfazer Check-out** .  
  
     **Colunas**  
     Identifique as colunas a serem exibidas e a ordem em que elas são exibidas.  
  
     **Exibição Simples**  
     Exiba os itens como listas simples com sua conexão de controle do código-fonte.  
  
     **Nome**  
     Exibe os nomes dos itens para os quais desfazer o check-out. Os itens aparecem com as caixas de seleção próximas a eles selecionadas. Se você não quiser desfazer a saída de um item, desmarque sua caixa de seleção.  
  
     **Opções**  
     Exibe opções de desfazer check-out específicas de plug-ins de controle do código-fonte quando é clicada a seta à direita do botão.  
  
     **Classificar**  
     Classifica a ordem das colunas exibidas.  
  
     **Exibição de árvore**  
     Exibe a pasta e hierarquia de item para itens que você está revertendo o check-out.  
  
     **Desfazer check-out**  
     Reverte o check-out, descartando qualquer alteração no arquivo onde foi feito o check-out.  
  
## <a name="see-also"></a>Consulte Também  
 [Fazer check-out de arquivos](../../2014/database-engine/check-out-files.md)   
 [Gerenciar check-outs](../../2014/database-engine/manage-checkouts.md)  
  
  
