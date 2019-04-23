---
title: Nova página de modelo (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 27d5bf66-b0e7-489e-a830-ffe2ec8e5350
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b0d571210c44026fc34ab43cb07e18bbd8526ed5
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59948572"
---
# <a name="new-model-page-report-manager"></a>Página Novo Modelo (Gerenciador de Relatórios)
  Use essa página para gerar um modelo de relatório padrão de uma fonte de dados compartilhada. Você só pode gerar modelos de relatório de fontes de dados multidimensionais do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , Oracle e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Modelos gerados no Gerenciador de Relatórios têm base no esquema de fonte de dados compartilhada. Entidades, pastas e campos são criados para todas as tabelas e colunas na fonte de dados. Você não pode excluir itens nem definir opções que determinam como o modelo é gerado. Para personalizar ou refinar um modelo, você deve usar o Designer de Modelo.  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-new-model-page"></a>Para abrir a página Novo Modelo  
  
1.  Abra o Gerenciador de Relatórios e localize a fonte de dados compartilhada a partir da qual você deseja gerar um modelo.  
  
2.  Focalize a fonte de dados e clique na seta para baixo.  
  
3.  No menu suspenso, execute uma destas etapas:  
  
    -   Clique em **Gerar Modelo de Relatório** para abrir a página Novo Modelo.  
  
    -   Clique em **Gerenciar** para abrir a página Propriedades gerais do relatório. Em seguida, clique em **Gerar Modelo** para abrir a página Novo Modelo.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Especifica o nome do modelo. Um nome deve conter pelo menos um caractere alfanumérico. Também pode conter espaços e alguns símbolos. Não use os seguintes caracteres ao especificar um nome:  
  
 ; ? : \@ & = + , $ / * \< > | " /  
  
 **Descrição**  
 Mostra uma descrição do modelo. Os usuários que exibirem esse item no Gerenciador de Relatórios poderão ver esta descrição ao navegar na hierarquia das pastas.  
  
 **Alterar local**  
 Mostra o local da pasta para o novo modelo. Clique no botão **Alterar Local** para selecionar outro local.  
  
  
