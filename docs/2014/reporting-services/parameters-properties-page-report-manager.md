---
title: Página de propriedades de parâmetros (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ebb53598-2378-46ae-8935-d5192f8ea49a
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 37b865f5f1e0ff029f030fcfab5bc1534fcb4a3c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153708"
---
# <a name="parameters-properties-page-report-manager"></a>Página Propriedades de Parâmetro (Gerenciador de Relatórios)
  Use página Propriedades de Parâmetro para exibir ou modificar configurações de parâmetro para um relatório com parâmetros.  
  
 Parâmetros são especificados na definição de relatório antes que o relatório seja publicado. Depois que o relatório é publicado, você pode modificar alguns valores de propriedade de parâmetro. Os valores que você pode modificar variam com base no modo como os parâmetros são definidos no relatório. Por exemplo, se uma lista de valores estáticos for definida para um parâmetro, você pode escolher um valor estático diferente para usar como padrão, mas não poderá adicionar ou remover valores da lista. Da mesma maneira, se o parâmetro for baseado em uma consulta, todos os aspectos dessa consulta (inclusive o conjunto de dados usado, quer sejam permitidos valores nulos ou em branco, quer seja fornecido um valor padrão) serão definidos no relatório antes da publicação.  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-parameters-properties-page"></a>Para abrir a página de propriedades de Parâmetros  
  
1.  Abra o Gerenciador de Relatórios e localize o relatório cujas configurações de parâmetro você deseja modificar.  
  
2.  Focalize o relatório e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Gerenciar**. Esse procedimento abre a página de propriedades Geral do relatório.  
  
4.  Selecione a guia **Parâmetros** . Se a guia **Parâmetros** não estiver visível, o relatório não contém parâmetros.  
  
## <a name="options"></a>Opções  
 **Nome do parâmetro**  
 Especifica o nome do parâmetro.  
  
 **Tipo de Dados**  
 Especifica o tipo de dados do parâmetro.  
  
 **Possui padrão**  
 Marque essa caixa de seleção para especificar se o parâmetro tem um valor padrão. Ao marcar essa caixa de seleção, **Valor Padrão**será habilitado. **Nulo** também será habilitado se o parâmetro de relatório aceitar valores nulos. Se **Possui Padrão** não for selecionado, será necessário ocultar o valor ou solicitar que o usuário forneça um valor quando o relatório for executado.  
  
 **Valor padrão**  
 Especifique um valor para o parâmetro. Para especificar um valor padrão, **Possui Padrão** deve ser selecionado e **Nulo** não deve ser selecionado. Um valor padrão pode ser fornecido pela definição de relatório. Se **Valor Padrão** for populado com um ou mais valores estáticos, esses valores se originarão com o relatório. Se **Valor padrão** for **Com Base em Consultas**, o valor do parâmetro será determinado por uma consulta definida no relatório.  
  
 Se **Valor Padrão** aceitar um valor, você pode digitar uma constante ou sintaxe que seja válida para a extensão de processamento de dados usada com o relatório. Por exemplo, se a linguagem da consulta da extensão de processamento de dados suportar curingas, você pode especificar um caractere curinga como valor padrão.  
  
 Se subsequentemente você especificar que um prompt seja exibido ao usuário, o valor padrão se tornará um valor inicial que os usuários podem usar ou modificar. Se você não solicitar um valor de parâmetro, esse valor será usado para todos os usuários que executarem o relatório.  
  
 **Nulo**  
 Marque essa caixa de seleção para especificar nulo como o valor padrão. Um valor nulo significa que o relatório será executado mesmo se o usuário não fornecer um valor de parâmetro. Se não houver nenhuma caixa de seleção nessa coluna, o parâmetro não aceitará valores nulos.  
  
 **Ocultar**  
 Marque essa caixa de seleção para ocultar o parâmetro na área de parâmetros que aparece no topo do relatório. O parâmetro ainda aparecerá em páginas de definição de assinatura e ainda pode ser especificado em uma URL de relatório. Ocultar o parâmetro é útil quando você quer executar sempre o relatório com um valor padrão especificado.  
  
 Desmarque esta caixa de seleção se você quiser o parâmetro seja visível no relatório.  
  
 **Avisar usuário**  
 Marque esta caixa de seleção para exibir uma caixa de texto que solicita aos usuários um valor de parâmetro.  
  
 Limpe essa caixa de seleção se você quiser executar o relatório no modo autônomo (por exemplo, para gerar o histórico do relatório ou instantâneos de execução de relatório), se quiser usar o mesmo valor de parâmetro para todos os usuários ou se não necessitar de entrada de usuário para o parâmetro.  
  
 **Texto de exibição**  
 Forneça uma cadeia de caracteres de texto que aparece próximo à caixa de texto de parâmetro. Essa cadeia de caracteres fornece um rótulo ou texto descritivo. Não há limite para o comprimento da cadeia de caracteres. Cadeias de caracteres de texto mais longo são encapsuladas no espaço fornecido.  
  
## <a name="see-also"></a>Consulte também  
 [Página Propriedades Gerais, Relatórios &#40;Gerenciador de Relatórios&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [Ajuda F1 do Gerenciador de Relatórios](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
