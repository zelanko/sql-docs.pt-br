---
title: Criar um relatório vinculado | Microsoft Docs
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6dad85f35be1d7fb26f4c9eef6241e01baadb692
ms.sourcegitcommit: c0e48b643385ce19c65ca6e348ce83b2d22b6514
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492793"
---
# <a name="create-a-linked-report"></a>Criar um relatório vinculado
  Um relatório vinculado é um item de servidor de relatório que fornece um ponto de acesso a um relatório existente. Conceitualmente, é semelhante a um atalho de programa usado para executar um programa ou abrir um arquivo.  
  
 Um relatório vinculado é derivado de um relatório existente e retém a definição de relatório original. Um relatório vinculado sempre herda as propriedades da fonte de dados e layout de relatório do relatório original. Todas as outras propriedades e configurações podem ser diferentes daquelas do relatório original, incluindo segurança, parâmetros, localidade, assinaturas e agendas.  
  
 Você pode criar um relatório vinculado quando você quiser criar versões adicionais de um relatório existente. Por exemplo, você pode usar um único relatório de vendas regional para criar relatórios para regiões específicas para todos os seus territórios de vendas.  
  
 Embora os relatórios vinculados sejam normalmente baseados em relatórios com parâmetros, um relatório com parâmetros não é exigido. Você pode criar relatórios vinculados sempre que desejar implantar um relatório existente com configurações diferentes.  
  
## <a name="to-create-a-linked-report"></a>Para criar um relatório vinculado  
  
1. No portal da web, navegue até o relatório desejado, clique com botão direito nele e selecione **gerenciar** no menu suspenso.

2. Sobre o **Manage <reportname>**  página, selecione **criar relatório vinculado**.  
  
3. Insira um nome para o novo relatório vinculado. Opcionalmente, insira uma descrição.  
  
4. Para selecionar uma pasta diferente para o relatório, selecione o botão de reticências (...) à direita da vírgula ***local***.  Navegue até a nova pasta para o relatório e selecione **selecionar**. Se você não selecionar uma pasta diferente, o relatório vinculado é criado na pasta atual.  
  
5. Selecione **Criar**. O relatório vinculado é criado.  

6. Sob **Advanced**, selecione uma opção diferente **tempo limite do relatório** valor se desejado e, em seguida, selecione **aplicar** para salvar as alterações.
  
     O ícone de um relatório vinculado difere de outros itens gerenciados por um servidor de relatório. O ícone a seguir indica um relatório vinculado:  
  
     ![Ícone Relatório vinculado](../../reporting-services/report-server/media/hlp-16linked.gif "Ícone Relatório vinculado")  
  
## <a name="see-also"></a>Confira também  

 [Conceitos do Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)  
 [O portal da Web de um servidor de relatório (modo nativo do SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)
  
