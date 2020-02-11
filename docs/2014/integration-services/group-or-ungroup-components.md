---
title: Agrupar ou desagrupar componentes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- grouping containers
- tasks [Integration Services], grouping
- containers [Integration Services], grouping
- grouping tasks
ms.assetid: 34320838-c271-4f8c-90b3-1254690890bb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f9ba8c8ce532621a44ac8a7ab58cb712a97934e4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62768118"
---
# <a name="group-or-ungroup-components"></a>Agrupa ou desagrupa componentes
  As guias **Fluxo de Controle**, **Fluxo de dados**e **Manipuladores de Eventos** no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] dão suporte a agrupamento recolhível. Se um pacote tem muitos componentes, as guias podem ficar cheias, tornando difícil visualizar todos os componentes ao mesmo tempo e localizar o item com o qual você quer trabalhar. O recurso de agrupamento desmontável, que pode conservar espaço na superfície de trabalho, e assim tornar mais fácil o trabalho com pacotes grandes.  
  
 Você seleciona os componentes que deseja agrupar, então os agrupa e, depois, expande ou recolhe os grupos para se adequarem ao seu trabalho. Expandir um grupo lhe dá acesso às propriedades dos componentes no grupo. As restrições de precedência que conectam tarefas e contêineres são automaticamente incluídas no grupo.  
  
 As seguintes são considerações para agrupar componentes.  
  
-   Para agrupar componentes, o fluxo de controle, fluxo de dados ou manipulador de eventos deverá conter mais de um componente.  
  
-   Os grupos também podem ser aninhados, tornando possível criar grupos dentro de grupos. A superfície do design pode implementar vários grupos não aninhados, mas um componente pode pertencer somente a um grupo, exceto se os grupos estiverem aninhados.  
  
-   Quando um pacote é salvo, o [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer salva o agrupamento, mas o agrupamento não tem nenhum efeito na execução de pacote. A habilidade de agrupar componentes é um recurso de tempo de design, ela não afeta o comportamento de tempo de execução do pacote.  
  
### <a name="to-group-components"></a>Para agrupar componentes  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle**, **Fluxo de Dados**ou **Manipuladores de Eventos** .  
  
4.  Na superfície de design da guia, selecione os componentes que você deseja agrupar, clique com o botão direito do mouse no componente selecionado e clique em **Agrupar**.  
  
5.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### <a name="to-ungroup-components"></a>Para desagrupar componentes  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle**, **Fluxo de Dados**ou **Manipuladores de Eventos** .  
  
4.  Na superfície de design da guia, selecione o grupo que contém o componente que você deseja desagrupar, clique com o botão direito do mouse no componente selecionado e clique em **Desagrupar**.  
  
5.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
     
 [Como conectar tarefas e contêineres por meio de uma restrição de precedência padrão](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)  
  
  
