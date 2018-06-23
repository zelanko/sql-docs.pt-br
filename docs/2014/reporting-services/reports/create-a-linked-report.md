---
title: Criar um relatório vinculado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
caps.latest.revision: 43
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 87e95389a4571162e07efce30c4bcd933309bef7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012836"
---
# <a name="create-a-linked-report"></a>Criar um relatório vinculado
  Um relatório vinculado é um item de servidor de relatório que fornece um ponto de acesso a um relatório existente. Conceitualmente, é semelhante a um atalho de programa usado para executar um programa ou abrir um arquivo.  
  
 Um relatório vinculado é derivado de um relatório existente e retém a definição de relatório original. Um relatório vinculado sempre herda as propriedades da fonte de dados e layout de relatório do relatório original. Todas as outras propriedades e configurações podem ser diferentes daquelas do relatório original, incluindo segurança, parâmetros, localidade, assinaturas e agendas.  
  
 Você pode criar um relatório vinculado quando você quiser criar versões adicionais de um relatório existente. Por exemplo, você pode usar um único relatório de vendas regional para criar relatórios para regiões específicas para todos os seus territórios de vendas.  
  
 Embora os relatórios vinculados sejam normalmente baseados em relatórios com parâmetros, um relatório com parâmetros não é exigido. Você pode criar relatórios vinculados sempre que desejar implantar um relatório existente com configurações diferentes.  
  
### <a name="to-create-a-linked-report"></a>Para criar um relatório vinculado  
  
1.  No Gerenciador de Relatórios, navegue até a pasta que contém o relatório a ser vinculado, abra o menu de opções e clique em **Criar Relatório Vinculado**.  
  
2.  Digite um nome para o novo relatório vinculado. Como opção, digite uma descrição.  
  
3.  Para selecionar uma pasta diferente para o relatório, clique em **Alterar Local**. Clique na pasta que deseja usar ou digite o nome de pasta na caixa **Local** . [!INCLUDE[clickOK](../../../includes/clickok-md.md)] Se você não selecionar uma pasta diferente, o relatório vinculado é criado na pasta atual (em que o relatório se baseia está armazenado).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)] O relatório vinculado é aberto.  
  
     O ícone de um relatório vinculado difere de outros itens gerenciados por um servidor de relatório. O ícone a seguir indica um relatório vinculado:  
  
     ![Ícone Relatório vinculado](../media/hlp-16linked.gif "Ícone Relatório vinculado")  
  
## <a name="see-also"></a>Consulte também  
 [Abrir e fechar um relatório &#40;Gerenciador de relatórios&#41;](../reports/open-and-close-a-report-report-manager.md)   
 [Página Novo Relatório Vinculado &#40;Gerenciador de Relatórios&#41;](../new-linked-report-page-report-manager.md)   
 [Página Escolher Local do Item &#40;Gerenciador de Relatórios&#41;](../choose-item-location-page-report-manager.md)   
 [Página Propriedades Gerais, Relatórios &#40;Gerenciador de Relatórios&#41;](../general-properties-page-reports-report-manager.md)   
 [Conceitos do Reporting Services &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md)  
  
  