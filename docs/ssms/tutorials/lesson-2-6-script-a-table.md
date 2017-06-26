---
title: Gerar script de uma tabela | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ea88d736-849e-4368-b55d-06aeee097bf3
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 5db067d5a2fe5bbf9953484c9a999ed7b1fcddae
ms.openlocfilehash: 422a81da1656b9b5c72fdcf1e71979ff0c8c058f
ms.contentlocale: pt-br
ms.lasthandoff: 06/23/2017

---
# <a name="lesson-2-6---script-a-table"></a>Lição 2-6 – Gerar script de uma tabela
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] pode criar scripts para selecionar, inserir, atualizar e excluir tabelas, além de criar, alterar, remover ou executar procedimentos armazenados.  
  
Às vezes você pode querer um script que tenha várias opções, como remover um procedimento e depois criar um procedimento, ou criar uma tabela e alterá-la. Para criar scripts combinados, salve o primeiro script em uma janela do Editor de Consultas e o segundo na área de transferência para que você possa colá-lo na janela após o primeiro script.  
  
 
1.  No Pesquisador de Objetos, expanda o servidor, expanda **Bancos de Dados**, [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], **Tabelas**, clique com o botão direito do mouse em **HumanResources.Employee**e aponte para **Criar Script de Tabela Como**.  
  
2.  O menu de atalho tem sete opções de script disponíveis: **CREATE To**, **DROP To**, **DROP e CREATE To**, **SELECT To**, **INSERT To**, **UPDATE To**e **DELETE To**. Aponte para **UPDATE To**e clique em **Nova Janela do Editor de Consultas**.  
  
3.  Uma nova janela do Editor de Consultas é aberta, estabelece uma conexão e apresenta a instrução de atualização inteira.  
  
    Esse exercício demonstra como o recurso de script pode fazer mais do que simplesmente executar o script de criação de uma tabela ou procedimento armazenado. Esse novo recurso pode ajudá-lo a adicionar rapidamente scripts de manipulação de dados a seu projeto e a executar scripts de procedimento armazenados com facilidade. Isso pode economizar muito tempo em tabelas e procedimentos com vários campos.  
  
 
  
  
  

