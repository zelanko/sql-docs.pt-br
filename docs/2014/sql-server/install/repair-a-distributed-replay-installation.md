---
title: Reparar uma instalação do Distributed Replay | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6fcd8ca8-1ceb-457d-9545-096c74e274d7
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8adf917831b33c1603b3c0c4a1e7b678900cf7dd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115151"
---
# <a name="repair-a-distributed-replay-installation"></a>Reparar uma instalação do Distributed Replay
  A reparação de um componente do Distributed Replay (controlador ou cliente) fará o seguinte:  
  
1.  Instalará todos os arquivos associados em disco novamente e substituirá os arquivos existentes.  
  
2.  Recriará a conta de serviço do Windows se a conta de serviço correspondente for removida.  
  
 Você não pode usar a operação Reparar para adicionar ou remover componentes. Para adicionar ou remover componentes, marque ou desmarque o componente correspondente na árvore de Recurso na página **Seleção de Recurso** na Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="to-repair-a-failed-installation-of-distributed-replay"></a>Para reparar uma instalação com falha do Distributed Replay  
  
1.  No menu **Iniciar** , clique em **Painel de Controle**e clique duas vezes em **Adicionar ou Remover Programas**.  
  
2.  Selecione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] na janela **Desinstalar ou alterar um programa** e, na caixa de diálogo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , clique em **Reparar**.  
  
3.  Siga as etapas no assistente do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e, na página **Selecionar Recursos** , selecione os componentes do Distributed Replay que você deseja reparar e clique em **Avançar**.  
  
4.  Conclua o Assistente de Instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para reparar os recursos selecionados de Distributed Replay.  
  
  