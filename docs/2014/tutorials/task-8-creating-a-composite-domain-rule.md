---
title: 'Tarefa 8: criando uma regra de domínio composto | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: cff3b662-7876-4445-9bdd-96be35b3ca0c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 4766a1206eb09e98bb20d3712a63762126b682b7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006239"
---
# <a name="task-8-creating-a-composite-domain-rule"></a>Tarefa 8: Criando uma regra de domínio composto
  Nesta tarefa, você cria uma regra para o domínio composto de **validação de endereço** . Você define uma regra de domínio cruzado: se **City** for **los Angeles**, o **estado** deverá ser **CA** em que **City** e **State** são dois domínios.  
  
1.  No painel direito, alterne para a guia **regras de CD** .  
  
2.  Clique em **Adicionar uma nova regra de domínio** na barra de ferramentas.  
  
3.  Digite **regra de Estado cidade** para **nome** e pressione **Enter**.  
  
4.  No painel **criar uma regra** , selecione **cidade** na lista domínio e selecione valor da condição **é igual a** e digite **los Angeles** para o valor.  
  
5.  No painel **em seguida** , selecione **estado** na lista domínio e selecione **valor é igual a**, digite **CA** para o valor e pressione **Tab**.  
  
     ![Regra Domínio Composto](../../2014/tutorials/media/et-creatingacompositedomainrule.jpg "Regra Domínio Composto")  
  
6.  Clique no botão **fechar** na parte inferior da página para alternar para a página principal do cliente do DQS. Você publicará a base de dados de conhecimento na próxima lição. Observe que a base de dados de conhecimento está no estado bloqueado (ícone de bloqueio).  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 9: Configurando um serviço de dados de referência](../../2014/tutorials/task-9-configuring-a-reference-data-service.md)  
  
  
