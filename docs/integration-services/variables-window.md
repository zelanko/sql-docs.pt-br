---
title: "Janela variáveis | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.variables.f1
- sql13.dts.designer.variableoptionswindow.f1
helpviewer_keywords:
- Variables Window dialog box
ms.assetid: f405e5ce-ef69-4c58-8c7d-a3d44dfe9ab0
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a87438f0f702a46b88b350ee32b734f64b1c6ad2
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="variables-window"></a>Janela Variáveis
  Use a janela **Variáveis** para criar e modificar as variáveis definidas pelo usuário e para exibir as variáveis do sistema.  
  
 Por padrão, a janela **Variáveis** está localizada abaixo da área **Gerenciadores de Conexões** no Designer SSIS, no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Se não aparecer a janela **Variáveis** , clique em **Variáveis** no menu **SSIS** para exibir a janela.  
  
 Além disso, você pode exibir a janela **Variáveis** mapeando o comando View.Variables para uma combinação de teclas de sua escolha na página **Teclado** da caixa de diálogo **Opções** .  
  
> [!NOTE]  
>  Os valores das propriedades **Name** e **Namespace** devem começar com uma letra de caractere alfabético, conforme definido pelo Unicode Standard 2.0 ou um sublinhado (_). Os caracteres subsequentes podem ser letras ou números conforme definido no padrão Unicode Standard 2.0 ou o sublinhado (\_).  
  
## <a name="options"></a>Opções  
 **Adicionar Variável**  
 Adicione uma variável definida pelo usuário.  
  
 **Mover variável**  
 Clique em uma variável na lista e, em seguida, clique **Mover Variável** para alterar o escopo da variável. Na caixa de diálogo **Selecionar Novo Escopo** , selecione o pacote ou um contêiner, tarefa ou manipulador de eventos no pacote, para alterar o escopo variável.  
  
 Para obter mais informações sobre escopo variável, consulte [Variáveis do SSIS &#40;Integration Services&#41;](../integration-services/integration-services-ssis-variables.md).  
  
 **Excluir Variável**  
 Selecione uma variável na lista e clique em **Excluir Variável**.  
  
 **Opções de grade**  
 Clique para abrir a caixa de diálogo **Opções de Grade Variáveis** em que é possível alterar a seleção de colunas e aplique filtros à janela **Variáveis** . Para obter mais informações, consulte [Opções de Grade Variáveis](../integration-services/variable-grid-options.md).  
  
 **Name**  
 Exiba o nome da variável. Você pode atualizar o nome para as variáveis definidas pelo usuário.  
  
 **Escopo**  
 Exiba o escopo da variável. Uma variável tem o escopo do pacote inteiro ou o escopo de um contêiner ou tarefa. O escopo da variável deve ser suficiente para que a variável fique visível às demais tarefas ou componentes que requerem a leitura ou a definição de seu valor.  
  
 Você pode alterar o escopo clicando na variável e, em seguida, clicando em **Mover Variável** na janela **Variáveis** .  
  
 **Tipo de Dados**  
 Exiba o tipo de dados da variável. Você pode selecionar um tipo de dados na lista para as variáveis definidas pelo usuário.  
  
> [!NOTE]  
>  Se você atribuir uma expressão à variável, não poderá alterar o tipo de dados.  
  
 **Value**  
 Exiba o valor da variável. Você pode atualizar o valor da variável para as variáveis definidas pelo usuário. Este valor pode ser literal ou uma expressão e pode ser uma cadeia de caracteres com várias linhas. Para atribuir uma expressão à variável, clique no botão de reticências ao lado da coluna **Expressão** na janela **Variáveis** .  
  
 **Namespace**  
 Exiba o nome do namespace. As variáveis definidas pelo usuário são criadas inicialmente no namespace **User** , mas você pode alterar o nome do namespace no campo **Namespace** . Para exibir esta coluna, clique em **Opções de Grade**.  
  
 **Elevar Evento de Alteração**  
 Indique se precisa gerar um evento **OnVariableValueChanged** quando o valor é alterado. Você pode atualizar o valor para as variáveis do sistema e as definidas pelo usuário. Por padrão, a janela **Variáveis** não lista esta coluna. Para exibir esta coluna, clique em **Opções de Grade**.  
  
 **Description**  
 Exiba a descrição da variável. Você pode alterar a descrição para as variáveis definidas pelo usuário. Por padrão, a janela **Variáveis** não lista esta coluna. Para exibir esta coluna, clique em **Opções de Grade**.  
  
 **Expressão**  
 Exiba a expressão atribuída à variável. Para atribuir uma expressão, clique botão de reticências.  
  
 Se você atribui uma expressão a uma variável, um marcador de ícone especial é exibido ao lado da variável. Esse marcador de ícone especial também é exibido ao lado de gerenciadores de conexões e tarefas que têm expressões definidas neles.  

## <a name="variable-grid-options-dialog-box"></a>Caixa de diálogo Opções de grade variável
 Use a caixa de diálogo **Opções de Grade Variáveis** para selecionar as colunas para serem exibidas na janela **Variáveis** e para selecionar os filtros para serem aplicados na lista de variáveis. Para obter mais informações sobre as propriedades de variáveis correspondentes, consulte [Variáveis do SSIS &#40;Integration Services&#41;](../integration-services/integration-services-ssis-variables.md).  
  
### <a name="options-for-filter"></a>Opções para filtrar  
 **Mostrar variáveis de sistema**  
 Selecione para listar variáveis de sistema na janela **Variáveis** . As variáveis de sistema são pré-definidas. Você não pode adicionar ou excluir as variáveis de sistema. É possível modificar as configurações da propriedade **RaiseChangedEvent** .  
  
 Essa lista é codificada por cor. As variáveis do sistema são cinza e as variáveis definidas pelo usuário são pretas.  
  
 **Mostrar variáveis de todos os escopos**  
 Selecione para mostrar variáveis dentro do escopo do pacote, e dentro do escopo de contêineres, tarefas ou manipuladores de eventos no pacote. Marque essa opção para mostrar somente variáveis dentro do escopo do pacote e dentro do escopo de um contêiner, tarefa ou manipulador de eventos selecionado.  
  
 Para obter mais informações sobre escopo variável, consulte [Variáveis do SSIS &#40;Integration Services&#41;](../integration-services/integration-services-ssis-variables.md).  
  
### <a name="options-for-columns"></a>Opções para colunas  
 Selecione as colunas que você quer que sejam exibidas na janela **Variáveis** .  
  
-   **Escopo**  
  
-   **Data type**  
  
-   **Value**  
  
-   **Namespace**  
  
-   **Levantar evento quando o valor da variável for alterado**  
  
-   **Description**  
  
-   **Expressão**  
  
## <a name="see-also"></a>Consulte também  
 [Variáveis do SSIS &#40;Integration Services&#41;](../integration-services/integration-services-ssis-variables.md)   
 [Usar variáveis em pacotes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)   
 [Integration Services &#40; SSIS &#41; Expressões](../integration-services/expressions/integration-services-ssis-expressions.md)   
 [Gerar arquivos de despejo para execução de pacote](../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  

