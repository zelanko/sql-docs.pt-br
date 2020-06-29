---
title: Caixa de diálogo Parametrizar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.parameter.f1
ms.assetid: fac02b6d-d247-447a-8940-e8700c7ac350
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 50bd1674dcc31240864f87a6e0d13c2599996e0b
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423523"
---
# <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
  A caixa de diálogo **Parametrizar** permite que você associe um novo parâmetro ou um existente à propriedade de uma tarefa. Você abre a caixa de diálogo clicando com o botão direito em uma tarefa ou na guia Fluxo de Controle no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] e, em seguida, clique em **Parametrizar**. A lista a seguir descreve os elementos da interface de usuário na caixa de diálogo. Para obter mais informações sobre parâmetros, consulte [Parâmetros do Integration Services &#40;SSIS&#41;](integration-services-ssis-package-and-project-parameters.md).  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
 **Propriedade**  
 Selecione a propriedade da tarefa que você deseja associar a um parâmetro. Esta lista é preenchida com todas as propriedades que podem ser parametrizadas.  
  
 **Usar parâmetros existentes**  
 Selecione esta opção para associar a propriedade da tarefa a um parâmetro existente e, em seguida, selecione o parâmetro na lista suspensa.  
  
 **Não usar parâmetro**  
 Selecione esta opção para remover uma referência a um parâmetro. O parâmetro não é excluído.  
  
 **Criar novo parâmetro**  
 Selecione esta opção para criar um novo parâmetro que você deseja associar à propriedade da tarefa.  
  
 **Nome**  
 Especifica o nome do parâmetro que você quer criar.  
  
 **Descrição**  
 Especifique a descrição para o parâmetro.  
  
 **Valor**  
 Especifique o valor padrão para o parâmetro. Isto também é conhecido como o padrão de design que pode ser substituído posteriormente no momento da implantação.  
  
 **Escopo**  
 Especifique o escopo do parâmetro selecionando a opção **Projeto** ou **Pacote** . Os parâmetros do projeto são usados para fornecer uma entrada externa que o projeto recebe para um ou mais pacotes no projeto. Os parâmetros do pacote permitem modificar a execução do pacote sem a necessidade de editar e reimplantar o pacote.  
  
 **Diferencia**  
 Especifique se o parâmetro é confidencial marcando ou desmarcando a caixa de seleção. Valores de parâmetros confidenciais são criptografados no catálogo e aparecem como um valor NULL quando exibidos com o Transact-SQL ou o SQL Server Management Studio.  
  
 **Necessário**  
 Especifique se o parâmetro exige que um valor diferente do padrão de design seja especificado para que o pacote possa ser executado.  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
  
