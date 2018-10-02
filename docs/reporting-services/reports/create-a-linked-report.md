---
title: Criar um relatório vinculado | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a757dd4dac0e788c33e1189171c58987a7bc4fa2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47663614"
---
# <a name="create-a-linked-report"></a>Criar um relatório vinculado
  Um relatório vinculado é um item de servidor de relatório que fornece um ponto de acesso a um relatório existente. Conceitualmente, é semelhante a um atalho de programa usado para executar um programa ou abrir um arquivo.  
  
 Um relatório vinculado é derivado de um relatório existente e retém a definição de relatório original. Um relatório vinculado sempre herda as propriedades da fonte de dados e layout de relatório do relatório original. Todas as outras propriedades e configurações podem ser diferentes daquelas do relatório original, incluindo segurança, parâmetros, localidade, assinaturas e agendas.  
  
 Você pode criar um relatório vinculado quando você quiser criar versões adicionais de um relatório existente. Por exemplo, você pode usar um único relatório de vendas regional para criar relatórios para regiões específicas para todos os seus territórios de vendas.  
  
 Embora os relatórios vinculados sejam normalmente baseados em relatórios com parâmetros, um relatório com parâmetros não é exigido. Você pode criar relatórios vinculados sempre que desejar implantar um relatório existente com configurações diferentes.  
  
### <a name="to-create-a-linked-report"></a>Para criar um relatório vinculado  
  
1.  No Gerenciador de Relatórios, navegue até a pasta que contém o relatório a ser vinculado, abra o menu de opções e clique em **Criar Relatório Vinculado**.  
  
2.  Digite um nome para o novo relatório vinculado. Como opção, digite uma descrição.  
  
3.  Para selecionar uma pasta diferente para o relatório, clique em **Alterar Local**. Clique na pasta que deseja usar ou digite o nome de pasta na caixa **Local** . [!INCLUDE[clickOK](../../includes/clickok-md.md)] Se você não selecionar uma pasta diferente, o relatório vinculado será criado na pasta atual (em que o relatório no qual ele se baseia está armazenado).  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] O relatório vinculado é aberto.  
  
     O ícone de um relatório vinculado difere de outros itens gerenciados por um servidor de relatório. O ícone a seguir indica um relatório vinculado:  
  
     ![Ícone Relatório vinculado](../../reporting-services/report-server/media/hlp-16linked.gif "Ícone Relatório vinculado")  
  
## <a name="see-also"></a>Consulte Também  
 [Abrir e fechar um relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/reports/open-and-close-a-report-report-manager.md)   
 [Página Novo Relatório Vinculado &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/fefb46e8-6901-4d50-a3f8-7c49ad72e7b1)   
 [Página Escolher Local do Item &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/4a53a1a8-d1e1-47ef-b1fc-63352ece7d3c)   
 [Página Propriedades Gerais, Relatórios &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/66c99d28-ab41-45f0-bf02-ed560293595d)   
 [Conceitos do Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  
