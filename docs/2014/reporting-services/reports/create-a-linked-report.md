---
title: Criar um relatório vinculado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 27667eececc3905b927b7e888e692a8261d14d30
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177054"
---
# <a name="create-a-linked-report"></a>Criar um relatório vinculado
  Um relatório vinculado é um item de servidor de relatório que fornece um ponto de acesso a um relatório existente. Conceitualmente, é semelhante a um atalho de programa usado para executar um programa ou abrir um arquivo.

 Um relatório vinculado é derivado de um relatório existente e retém a definição de relatório original. Um relatório vinculado sempre herda as propriedades da fonte de dados e layout de relatório do relatório original. Todas as outras propriedades e configurações podem ser diferentes daquelas do relatório original, incluindo segurança, parâmetros, localidade, assinaturas e agendas.

 Você pode criar um relatório vinculado quando você quiser criar versões adicionais de um relatório existente. Por exemplo, você pode usar um único relatório de vendas regional para criar relatórios para regiões específicas para todos os seus territórios de vendas.

 Embora os relatórios vinculados sejam normalmente baseados em relatórios com parâmetros, um relatório com parâmetros não é exigido. Você pode criar relatórios vinculados sempre que desejar implantar um relatório existente com configurações diferentes.

### <a name="to-create-a-linked-report"></a>Para criar um relatório vinculado

1.  No Gerenciador de Relatórios, navegue até a pasta que contém o relatório a ser vinculado, abra o menu de opções e clique em **Criar Relatório Vinculado**.

2.  Digite um nome para o novo relatório vinculado. Como opção, digite uma descrição.

3.  Para selecionar uma pasta diferente para o relatório, clique em **Alterar Local**. Clique na pasta que deseja usar ou digite o nome de pasta na caixa **Local** . 
  [!INCLUDE[clickOK](../../../includes/clickok-md.md)] Se você não selecionar uma pasta diferente, o relatório vinculado será criado na pasta atual (em que o relatório no qual ele se baseia está armazenado).

4.  
  [!INCLUDE[clickOK](../../../includes/clickok-md.md)] O relatório vinculado é aberto.

     O ícone de um relatório vinculado difere de outros itens gerenciados por um servidor de relatório. O ícone a seguir indica um relatório vinculado:

     ![Ícone de relatório vinculado](../media/hlp-16linked.gif "Ícone de relatório vinculado")

## <a name="see-also"></a>Consulte Também
 [Abra e feche um relatório &#40;Report Manager&#41;](../reports/open-and-close-a-report-report-manager.md) [nova página de relatório vinculada &#40;Report Manager](../new-linked-report-page-report-manager.md)&#41;[escolha a página local &#40;](../choose-item-location-page-report-manager.md) Report Manager o SSRS [&#41;&#40;](../report-manager-ssrs-native-mode.md) [de propriedades gerais, relatórios Report Manager&#41;](../general-properties-page-reports-report-manager.md) Reporting Services [conceitos](../reporting-services-concepts-ssrs.md) &#40;


