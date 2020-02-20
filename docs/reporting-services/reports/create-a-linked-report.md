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
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67492793"
---
# <a name="create-a-linked-report"></a>Criar um relatório vinculado
  Um relatório vinculado é um item de servidor de relatório que fornece um ponto de acesso a um relatório existente. Conceitualmente, é semelhante a um atalho de programa usado para executar um programa ou abrir um arquivo.  
  
 Um relatório vinculado é derivado de um relatório existente e retém a definição de relatório original. Um relatório vinculado sempre herda as propriedades da fonte de dados e layout de relatório do relatório original. Todas as outras propriedades e configurações podem ser diferentes daquelas do relatório original, incluindo segurança, parâmetros, localidade, assinaturas e agendas.  
  
 Você pode criar um relatório vinculado quando você quiser criar versões adicionais de um relatório existente. Por exemplo, você pode usar um único relatório de vendas regional para criar relatórios para regiões específicas para todos os seus territórios de vendas.  
  
 Embora os relatórios vinculados sejam normalmente baseados em relatórios com parâmetros, um relatório com parâmetros não é exigido. Você pode criar relatórios vinculados sempre que desejar implantar um relatório existente com configurações diferentes.  
  
## <a name="to-create-a-linked-report"></a>Para criar um relatório vinculado  
  
1. No portal da Web, navegue até o relatório desejado, clique com o botão direito do mouse nele e selecione **Gerenciar** no menu suspenso.

2. Na página **Gerenciar <reportname>** , selecione **Criar relatório vinculado**.  
  
3. Insira um nome para o novo relatório vinculado. Insira uma descrição opcionalmente.  
  
4. Para selecionar uma pasta diferente do relatório, selecione o botão de reticências (...) à direita de ***Localização***.  Navegue até a nova pasta do relatório e selecione **Selecionar**. Se você não selecionar uma pasta diferente, o relatório vinculado será criado na pasta atual.  
  
5. Selecione **Criar**. O relatório vinculado é criado.  

6. Em **Avançado**, selecione um valor **Tempo limite de relatório** diferente se desejado e selecione **Aplicar** para salvar as alterações.
  
     O ícone de um relatório vinculado difere de outros itens gerenciados por um servidor de relatório. O ícone a seguir indica um relatório vinculado:  
  
     ![Ícone do relatório vinculado](../../reporting-services/report-server/media/hlp-16linked.gif "Ícone do relatório vinculado")  
  
## <a name="see-also"></a>Confira também  

 [Conceitos do Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)  
 [O portal da Web de um servidor de relatório (modo nativo do SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)
  
