---
title: Adicionar ou alterar uma expressão de propriedade | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- expressions [Integration Services], creating
- expressions [Integration Services], property expressions
ms.assetid: cb5da499-065f-4fa6-9f6d-5bc5f385241e
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 147daa2f1e58d636b460921f5a50a987e92a156e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187053"
---
# <a name="add-or-change-a-property-expression"></a>Adicionar ou alterar uma expressão de propriedade
  Você pode criar expressões de propriedade para pacotes, tarefas contêineres Loop Foreach, contêineres Loop For, contêineres de Sequência, manipuladores de eventos, gerenciadores de conexões de nível de pacote e projeto, e provedores de logs.  
  
 Para criar ou alterar expressões de propriedade, você pode usar o **Editor de Expressão de Propriedades** ou o **Construtor de Expressões**. O **Editor de Expressão de Propriedades** pode ser acessados dos editores personalizados que estão disponíveis para tarefas e contêineres ou da janela **Propriedades** . O**Construtor de Expressões** pode ser acessado de dentro do **Editor de Expressão de Propriedades**. Embora você possa gravar expressões no **Editor de Expressões de Propriedade** ou no **Construtor de Expressões**, o **Construtor de Expressões** oferece um conjunto gráfico de ferramentas que facilitam a criação de expressões complexas.  
  
 Para obter mais informações sobre a sintaxe, operadores e funções que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece, consulte [Operadores &#40; Expressão SSIS&#41;](operators-ssis-expression.md) e [Funções &#40;Expressão SSIS&#41;](functions-ssis-expression.md). Os tópicos sobre cada operador ou função incluem exemplos de como usar o operador ou a função em uma expressão. Para obter exemplos de expressões mais complexas, consulte [Usar expressões de propriedade em pacotes](use-property-expressions-in-packages.md).  
  
### <a name="to-create-or-change-a-property-expression"></a>Para criar ou alterar uma expressão de propriedade  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo e siga um destes procedimentos:  
  
    -   Se o item for uma tarefa ou um contêiner, clique duas vezes nele e clique em **Expressões** no editor.  
  
    -   Clique com o botão direito do mouse no item e clique em **Propriedades**.  
  
3.  Clique na caixa **Expressões** e clique nas reticências (...).  
  
4.  No **Editor de Propriedades de Expressões**, selecione uma propriedade na lista **Propriedade** e execute um dos seguintes procedimentos:  
  
    -   Digite ou altere a expressão de propriedade diretamente na coluna **Expressão** e clique em **OK**.  
  
         — ou —  
  
    -   Clique nas reticências (…) na linha de expressão da propriedade para abrir o **Construtor de Expressões**.  
  
5.  (Opcional) No **Construtor de Expressões**, execute qualquer uma das seguintes tarefas:  
  
    -   Para acessar variáveis de sistema e definidas pelo usuário, expanda **Variáveis**.  
  
    -   Para acessar as funções, as conversões e os operadores fornecidos pela linguagem de expressão do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , expanda **Funções Matemáticas**, **Funções de Cadeia de Caracteres**, **Funções de Data/Hora**, **Funções NULL**, **Conversões de Tipos**e **Operadores**.  
  
    -   Para criar ou alterar uma expressão no **Construtor de Expressões**, arraste variáveis, colunas, funções, operadores e conversões até a caixa **Expressão** ou digite a expressão na caixa.  
  
    -   Para exibir o resultado de avaliação da expressão, clique em **Avaliar Expressão** no **Construtor de Expressões**.  
  
         Se a expressão não for válida, será exibido um alerta descrevendo os erros de sintaxe na expressão.  
  
        > [!NOTE]  
        >  A avaliação de uma expressão não atribui o resultado da avaliação à propriedade.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Expressões do SSIS &#40;Integration Services&#41;](integration-services-ssis-expressions.md)   
 [Usar expressões de propriedade em pacotes](use-property-expressions-in-packages.md)   
 [Serviços de integração &#40;SSIS&#41; pacotes](../integration-services-ssis-packages.md)   
 [Contêineres do Integration Services](../control-flow/integration-services-containers.md)   
 [Tarefas do Integration Services](../control-flow/integration-services-tasks.md)   
 [Manipuladores de eventos do SSIS &#40;Integration Services&#41;](../integration-services-ssis-event-handlers.md)   
 [Conexões do SSIS &#40;Integration Services&#41;](../connection-manager/integration-services-ssis-connections.md)   
 [Registro em Log do SSIS &#40;Integration Services&#41;](../performance/integration-services-ssis-logging.md)  
  
  
