---
title: Fazer check-in de arquivos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VisualStudio.SourceControl.CheckInDialog
helpviewer_keywords:
- checking in files
ms.assetid: 0657a387-8411-4406-bef9-d262a5bfa269
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5debb7c80e7365e67d8661709b09b16f5d25b7b9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62812541"
---
# <a name="check-in-files"></a>Fazer check-in de arquivos
  Para tornar arquivos com controle do código-fonte disponíveis para outros usuários, você deve fazer o check-in dos arquivos no controle do código-fonte. Quando você faz check-in de um arquivo, essa versão é salva no provedor de controle do código-fonte e torna-se a versão mais recente do arquivo.  
  
 É possível usar o comando **Check-in** para fazer check-in dos arquivos. Se você usar esse comando para fazer check-in de uma solução ou projeto, todos os arquivos da solução ou do projeto também farão check-in. Entretanto, fazer o check-in de um arquivo de código-fonte individual não resulta no check-in do projeto ou da solução a que ele pertence.  
  
### <a name="to-check-in-a-file"></a>Para fazer check-in de um arquivo  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse no arquivo de check-in e clique em **Check-in**.  
  
2.  Se a caixa de diálogo **Check-in** for exibida, selecione as opções apropriadas e clique em **OK**.  
  
     **Check-in**  
     Efetua check-in de todos os itens selecionados.  
  
     **Colunas**  
     Identifique as colunas a serem exibidas e a ordem em que elas são exibidas.  
  
     **Comentários**  
     Adiciona um comentário a associar com a operação de check-in.  
  
     **Não mostrar caixa de diálogo Fazer Check-in ao fazer check-in dos itens**  
     Suprime a caixa de diálogo durante operações de check-in.  
  
     **Exibição Simples**  
     Exibe os arquivos dos quais está fazendo check-in como listas simples na conexão de controle do código fonte.  
  
     **Nome**  
     Exibe os nomes dos itens dos quais fazer check-in. Os itens aparecem com as caixas de seleção próximas a eles selecionadas. Se não quiser fazer check-in de um item em particular, desmarque sua caixa de seleção.  
  
     **Opções**  
     Exibe opções de check-in específico de plug-ins de controle do código fonte quando se clica na seta à direita do botão.  
  
     **Classificar**  
     Classifica a ordem das colunas exibidas.  
  
     **Exibição de Árvore**  
     Exibe a hierarquia de pastas e arquivos dos itens dos quais está fazendo check-in.  
  
 Se o arquivo com check-in não fizer parte de uma saída compartilhada, o ambiente do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] fará imediatamente o check-in do arquivo. Caso contrário, você pode ser solicitado a mesclar sua versão com versões criadas por outros usuários.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir uma lista de arquivos modificados](../../2014/database-engine/view-a-list-of-modified-files.md)   
 [Gerenciar check-ins](../../2014/database-engine/manage-checkins.md)  
  
  
