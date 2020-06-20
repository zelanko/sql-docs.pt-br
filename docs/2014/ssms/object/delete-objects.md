---
title: Excluir objetos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.deleteobjects.f1
helpviewer_keywords:
- Delete Objects dialog box
ms.assetid: 49541441-179c-40d3-ba0c-01bcae545984
author: stevestein
ms.author: sstein
ms.openlocfilehash: e7b20d1eee3e48c5531b6b788e125b943f7606d1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067327"
---
# <a name="delete-objects"></a>Excluir Objetos
  Use essa caixa de diálogo para excluir um banco de dados ou objeto de banco de dados.  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
 **Objeto a ser excluído**  
 Exibe os nomes, os tipos, os proprietários e o status dos objetos a serem excluídos, bem como qualquer mensagem sobre erros durante a execução.  
  
> [!NOTE]  
>  Executar **Excluir** em um banco de dados é equivalente a emitir DROP DATABASE em [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Mostrar Dependências**  
 Clique para exibir os objetos que são dependentes do objeto selecionado atualmente e os objetos dos quais o objeto selecionado é dependente (dependência ascendente e descendente). As informações exibidas na caixa de diálogo **Mostrar Dependências** são somente leitura.  
  
> [!NOTE]  
>  O botão **Mostra Dependências** não aparece para todos os tipos de objetos de banco de dados. Para exibir as dependências quando o botão **Mostrar Dependências** não está disponível, clique com o botão direito do mouse no Pesquisador de Objetos e em **Exibir Dependências**.  
  
 **Exclua informações de backup e de histórico de restauração para os bancos de dados**  
 Aparece somente quando um banco de dados é excluído, essa caixa de seleção faz com que o backup e o histórico de restauração do banco de dados de assunto sejam excluídos do banco de dados **msdb** .  
  
 **Encerre as conexões existentes**  
 Aparece somente quando um banco de dados é excluído, essa caixa de seleção encerra as conexões com o banco de dados de assunto.  
  
  
