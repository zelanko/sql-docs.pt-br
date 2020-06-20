---
title: 'Tarefa 7: Criando um domínio composto | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ae778647-1df0-4952-9a69-0ef6177eea9c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 42936d25e267bcad5ba8ae512750f9e12f041579
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064716"
---
# <a name="task-7-creating-a-composite-domain"></a>Tarefa 7: Criando uma regra de domínio composto
  Nesta tarefa, você cria um domínio composto, uma **validação de endereço**, que abrange os domínios de **linha de endereço**, **cidade**, **estado**e **zip** . Um domínio composto permite definir uma regra entre domínios que envolve vários domínios em uma regra. Há outras vantagens para um domínio composto, como analisar um valor de campo em vários domínios.  Por exemplo, um valor para um campo Nome Completo pode ser analisado em domínios separados de Nome, Nome do Meio e Sobrenome. Neste tutorial, você define apenas uma regra entre domínios. Consulte [Gerenciando um domínio de composição](https://msdn.microsoft.com/library/hh510399.aspx) para obter mais detalhes.  
  
1.  No painel esquerdo, clique no botão **criar um domínio composto** na barra de ferramentas.  
  
     ![Botão de barra de ferramentas Criar um Domínio Composto](../../2014/tutorials/media/et-creatingacompositedomain-01.jpg "Botão de barra de ferramentas Criar um Domínio Composto")  
  
2.  Insira a **validação de endereço** para o nome de **domínio composto**.  
  
     ![Domínio Composto de Validação de Endereço](../../2014/tutorials/media/et-creatingacompositedomain-02.jpg "Domínio Composto de Validação de Endereço")  
  
3.  Na lista de domínios, **selecione linha de endereço**, **cidade**, **estado**e **CEP** e clique na seta para a **direita** para adicioná-los aos **domínios na lista domínio composto** .  
  
4.  Clique em **OK** para fechar a caixa de diálogo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 8: Criando uma regra de domínio composto](../../2014/tutorials/task-8-creating-a-composite-domain-rule.md)  
  
  
