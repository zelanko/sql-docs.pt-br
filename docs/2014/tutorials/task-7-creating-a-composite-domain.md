---
title: 'Tarefa 7: Criar um domínio composto | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ae778647-1df0-4952-9a69-0ef6177eea9c
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e88fa44fb4457a979dfa1236531ed8bfa61f88fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119816"
---
# <a name="task-7-creating-a-composite-domain"></a>Tarefa 7: Criando uma regra de domínio composto
  Nesta tarefa, você criará um domínio composto, **Address Validation**, que abrange **Address Line**, **City**, **estado**e  **ZIP** domínios. Um domínio composto permite definir uma regra entre domínios que envolve vários domínios em uma regra. Há outras vantagens para um domínio composto, como analisar um valor de campo em vários domínios.  Por exemplo, um valor para um campo Nome Completo pode ser analisado em domínios separados de Nome, Nome do Meio e Sobrenome. Neste tutorial, você define apenas uma regra entre domínios. Consulte [Gerenciando um domínio composto](http://msdn.microsoft.com/library/hh510399.aspx) para obter mais detalhes.  
  
1.  No painel esquerdo, clique em **criar um domínio composto** na barra de ferramentas.  
  
     ![Criar um botão de barra de ferramentas do domínio composto](../../2014/tutorials/media/et-creatingacompositedomain-01.jpg "criar um botão de barra de ferramentas do domínio composto")  
  
2.  Digite **endereço validação** para o **nome de domínio composto**.  
  
     ![O domínio composto de validação de endereço](../../2014/tutorials/media/et-creatingacompositedomain-02.jpg "domínio composto de validação de endereço")  
  
3.  Selecione a lista de domínio **Address Line**, **City**, **estado**, e **Zip** e clique em **seta para a direita** para adicioná-los para o **domínios no domínio composto** lista.  
  
4.  Clique em **OK** para fechar a caixa de diálogo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 8: Criando uma regra de domínio composto](../../2014/tutorials/task-8-creating-a-composite-domain-rule.md)  
  
  