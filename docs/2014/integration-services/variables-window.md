---
title: Janela Variáveis | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.variables.f1
helpviewer_keywords:
- Variables Window dialog box
ms.assetid: f405e5ce-ef69-4c58-8c7d-a3d44dfe9ab0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0b8541b0e590fe0fa6de9d577e69b7068fb2843d
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206195"
---
# <a name="variables-window"></a>Janela Variáveis
  Use a janela **Variáveis** para criar e modificar as variáveis definidas pelo usuário e para exibir as variáveis do sistema.  
  
 Por padrão, a janela **Variáveis** está localizada abaixo da área **Gerenciadores de Conexões** no Designer SSIS, no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Se não aparecer a janela **Variáveis**, clique em **Variáveis** no menu **SSIS** para exibir a janela.  
  
 Além disso, você pode exibir a janela **Variáveis** mapeando o comando View.Variables para uma combinação de teclas de sua escolha na página **Teclado** da caixa de diálogo **Opções** .  
  
> [!NOTE]
>  Os valores das propriedades `Name` e `Namespace` devem começar com uma letra de caractere alfabético, conforme definido pelo Unicode Standard 2.0 ou um sublinhado (_). Os caracteres subsequentes podem ser letras ou números conforme definido no padrão Unicode Standard 2.0 ou o sublinhado (\_).  
  
## <a name="options"></a>Opções  
 **Adicionar Variável**  
 Adicione uma variável definida pelo usuário.  
  
 **Mover variável**  
 Clique em uma variável na lista e, em seguida, clique **Mover Variável** para alterar o escopo da variável. Na caixa de diálogo **Selecionar Novo Escopo** , selecione o pacote ou um contêiner, tarefa ou manipulador de eventos no pacote, para alterar o escopo variável.  
  
 Para obter mais informações sobre escopo variável, consulte [Variáveis do SSIS &#40;Integration Services&#41;](integration-services-ssis-variables.md).  
  
 **Excluir Variável**  
 Selecione uma variável na lista e clique em **Excluir Variável**.  
  
 **Opções de grade**  
 Clique para abrir a caixa de diálogo **Opções de Grade Variáveis** em que é possível alterar a seleção de colunas e aplique filtros à janela **Variáveis** . Para obter mais informações, consulte [Opções de Grade Variáveis](../../2014/integration-services/variable-grid-options.md).  
  
 `Name`  
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
  
 `Namespace`  
 Exiba o nome do namespace. As variáveis definidas pelo usuário são inicialmente criadas na **usuário** namespace, mas você pode alterar o nome do namespace no `Namespace` campo. Para exibir esta coluna, clique em **Opções de Grade**.  
  
 **Elevar Evento de Alteração**  
 Indique se precisa gerar um evento `OnVariableValueChanged` quando o valor é alterado. Você pode atualizar o valor para as variáveis do sistema e as definidas pelo usuário. Por padrão, a janela **Variáveis** não lista esta coluna. Para exibir esta coluna, clique em **Opções de Grade**.  
  
 **Descrição**  
 Exiba a descrição da variável. Você pode alterar a descrição para as variáveis definidas pelo usuário. Por padrão, a janela **Variáveis** não lista esta coluna. Para exibir esta coluna, clique em **Opções de Grade**.  
  
 **Expression**  
 Exiba a expressão atribuída à variável. Para atribuir uma expressão, clique botão de reticências.  
  
 Se você atribui uma expressão a uma variável, um marcador de ícone especial é exibido ao lado da variável. Esse marcador de ícone especial também é exibido ao lado de gerenciadores de conexões e tarefas que têm expressões definidas neles.  
  
## <a name="see-also"></a>Consulte também  
 [Variáveis do SSIS &#40;Integration Services&#41;](integration-services-ssis-variables.md)   
 [Usar variáveis em pacotes](../../2014/integration-services/use-variables-in-packages.md)   
 [Expressões do Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md)   
 [Gerando arquivos de despejo para execução de pacote](troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
