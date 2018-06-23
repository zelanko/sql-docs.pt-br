---
title: Alterar controle do código-fonte | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- IDD_SCC_CONNECTION_DIALOG
helpviewer_keywords:
- Change Source Control dialog box
ms.assetid: e6a5d83c-5809-4c56-907a-73d0c7ccdd7a
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e2584a7981662bc96fff975d93dfd24ec79d5d77
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122708"
---
# <a name="change-source-control"></a>Alterar Controle do Código-Fonte
  Cria e gerencia as conexões e associações que vinculam uma solução ou projeto salvo localmente com uma pasta do banco de dados de controle do código fonte.  
  
## <a name="dialog-box-access"></a>Acesso à caixa de diálogo  
 No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], selecione um item no Gerenciador de Soluções. No menu **Arquivo** , clique em **Controle do Código Fonte**e em **Alterar Controle do Código Fonte**.  
  
> [!NOTE]  
>  Esta caixa de diálogo também está disponível clicando com o botão direito do mouse no item no Gerenciador de Soluções.  
  
## <a name="options"></a>Opções  
 **Ligação**  
 Associe itens selecionados com um local de servidor de controle do código fonte especificado. Por exemplo, você pode usar esse botão para associar à última pasta de servidor de controle do código fonte conhecida e ao banco de dados. Se uma pasta de servidor ou banco de dados recente não puder ser localizada, você será solicitado a especificar outra.  
  
 **Procurar**  
 Navegue até um novo local de servidor de controle do código fonte para o item especificado.  
  
 **Colunas**  
 Identifique colunas a serem exibidas e a ordem na qual elas são exibidas.  
  
 **Connect**  
 Crie uma conexão entre itens selecionados e o servidor de controle do código fonte.  
  
 **Conectado**  
 Exibe o status da conexão de uma solução ou projeto selecionado.  
  
 **Desconectar**  
 Desconecte a cópia local de uma solução ou projeto em seu computador a partir de sua cópia mestre no banco de dados. Use esse comando antes de desconectar seu computador do servidor de controle do código fonte, por exemplo, ao trabalhar offline no seu laptop.  
  
 **OK**  
 Aceite as alterações feitas na caixa de diálogo.  
  
 **Provedor**  
 Exibe o nome de seu plug-in de controle do código fonte.  
  
 **Atualizar**  
 Atualize as informações de conexão de todos os projetos listados nesta caixa de diálogo.  
  
 **Ligação de servidor**  
 Indica a associação do item com um servidor de controle do código fonte.  
  
 **Nome do servidor**  
 Exibe o nome do servidor de controle do código fonte ao qual a solução ou projeto correspondente está associado.  
  
 **Solução/projeto**  
 Exibe o nome de cada solução e projeto na seleção atual.  
  
 **Sort**  
 Classifique a ordem de colunas exibidas.  
  
 **Status**  
 Identifica o status da associação e da conexão de um item. Possíveis opções são:  
  
|**Opção**|**Descrição**|  
|----------------|---------------------|  
|Válido|O item está corretamente associado e conectado com a pasta de servidor à qual pertence.|  
|Inválido|O item está incorretamente associado com a pasta à qual pertence ou desconectado dela. Use o comando **Adicionar ao Controle do Código Fonte** em vez de **Associar** neste item.|  
|Unknown (desconhecido)|O status do item sob controle do código fonte ainda não foi determinado.|  
|Não Controlado|O item não foi colocado sob controle do código fonte.|  
  
 **Desvincular**  
 Exiba a caixa de diálogo **Controle do Código Fonte** para permitir que você remova itens selecionados do controle do código fonte e desassocie permanentemente os itens de suas pastas atuais.  
  
## <a name="see-also"></a>Consulte também  
 [Controle do código-fonte do Gerenciador de Soluções](../../2014/database-engine/solution-explorer-source-control.md)  
  
  