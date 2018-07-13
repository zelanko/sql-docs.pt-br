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
ms.topic: conceptual
ms.assetid: ae778647-1df0-4952-9a69-0ef6177eea9c
caps.latest.revision: 7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e6f1ee787a51b8417ad3de37b74075df8782c722
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153287"
---
# <a name="task-7-creating-a-composite-domain"></a>Tarefa 7: Criando uma regra de domínio composto
  Nesta tarefa, você criará um domínio composto, **Address Validation**, que inclui **Address Line**, **Cidade**, **estado**e  **ZIP** domínios. Um domínio composto permite definir uma regra entre domínios que envolve vários domínios em uma regra. Há outras vantagens para um domínio composto, como analisar um valor de campo em vários domínios.  Por exemplo, um valor para um campo Nome Completo pode ser analisado em domínios separados de Nome, Nome do Meio e Sobrenome. Neste tutorial, você define apenas uma regra entre domínios. Ver [Gerenciando um domínio composto](http://msdn.microsoft.com/library/hh510399.aspx) para obter mais detalhes.  
  
1.  No painel esquerdo, clique em **criar um domínio composto** na barra de ferramentas.  
  
     ![Criar um botão de barra de ferramentas do domínio composto](../../2014/tutorials/media/et-creatingacompositedomain-01.jpg "criar um botão de barra de ferramentas do domínio composto")  
  
2.  Insira **validação de endereço** para o **nome de domínio composto**.  
  
     ![Validação de domínio composto de endereço](../../2014/tutorials/media/et-creatingacompositedomain-02.jpg "domínio composto de validação de endereço")  
  
3.  Selecione a lista de domínio **Address Line**, **City**, **estado**, e **Zip** e clique em **seta para a direita** para adicioná-los para o **domínios no domínio composto** lista.  
  
4.  Clique em **OK** para fechar a caixa de diálogo.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 8: Criando uma regra de domínio composto](../../2014/tutorials/task-8-creating-a-composite-domain-rule.md)  
  
  
