---
title: Parametrizar a caixa de diálogo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.parameter.f1
ms.assetid: fac02b6d-d247-447a-8940-e8700c7ac350
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7d60820ba7c384347aeeec80d8c41f934078eca8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66056868"
---
# <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
  A caixa de diálogo **Parametrizar** permite que você associe um novo parâmetro ou um existente à propriedade de uma tarefa. Você abre a caixa de diálogo clicando com o botão direito em uma tarefa ou na guia Fluxo de Controle no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] e, em seguida, clique em **Parametrizar**. A lista a seguir descreve os elementos da interface de usuário na caixa de diálogo. Para obter mais informações sobre parâmetros, consulte [Parâmetros do Integration Services &#40;SSIS&#41;](integration-services-ssis-package-and-project-parameters.md).  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Propriedade**  
 Selecione a propriedade da tarefa que você deseja associar a um parâmetro. Esta lista é preenchida com todas as propriedades que podem ser parametrizadas.  
  
 **Usar parâmetro existente**  
 Selecione esta opção para associar a propriedade da tarefa a um parâmetro existente e, em seguida, selecione o parâmetro na lista suspensa.  
  
 **Não usar parâmetros**  
 Selecione esta opção para remover uma referência a um parâmetro. O parâmetro não é excluído.  
  
 **Criar novo parâmetro**  
 Selecione esta opção para criar um novo parâmetro que você deseja associar à propriedade da tarefa.  
  
 **Nome**  
 Especifica o nome do parâmetro que você quer criar.  
  
 **Descrição**  
 Especifique a descrição para o parâmetro.  
  
 **Value**  
 Especifique o valor padrão para o parâmetro. Isto também é conhecido como o padrão de design que pode ser substituído posteriormente no momento da implantação.  
  
 **Escopo**  
 Especifique o escopo do parâmetro selecionando a opção **Projeto** ou **Pacote** . Os parâmetros do projeto são usados para fornecer uma entrada externa que o projeto recebe para um ou mais pacotes no projeto. Os parâmetros do pacote permitem modificar a execução do pacote sem a necessidade de editar e reimplantar o pacote.  
  
 **Confidencial**  
 Especifique se o parâmetro é confidencial marcando ou desmarcando a caixa de seleção. Valores de parâmetros confidenciais são criptografados no catálogo e aparecem como um valor NULL quando exibidos com o Transact-SQL ou o SQL Server Management Studio.  
  
 **Necessário**  
 Especifique se o parâmetro exige que um valor diferente do padrão de design seja especificado para que o pacote possa ser executado.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
  
