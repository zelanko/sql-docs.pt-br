---
title: Vincular um relatório a um modelo como um relatório de Clickthrough | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- customizing clickthrough reports
- clickthrough reports, customizing
- clickthrough reports, templates
ms.assetid: 3af42de3-67ef-41c2-bc8a-7045baec6f63
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 90b21c6fa21322afe1d9351e73460fce1a4592f8
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59944152"
---
# <a name="link-a-report-to-a-model-as-a-clickthrough-report"></a>Vincular um relatório a um modelo como um relatório de clickthrough
  Em vez de usar os modelos de relatório de clickthrough padrão, você pode criar um relatório Construtor de Relatórios e vinculá-lo a uma entidade específica no modelo de relatório. Quando a pessoa que está exibindo o relatório clica nos dados interativos do relatório principal, esse relatório é exibido como relatório de clickthrough. Para vincular um relatório a uma entidade, use o Gerenciador de Relatórios [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  A entidade principal, ou básica, usada no relatório deve ser igual à entidade a qual o relatório está vinculado.  
  
### <a name="to-start-report-manager-from-a-browser"></a>Para iniciar o Gerenciador de Relatórios em um navegador  
  
1.  Abra o [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 6.0 ou posterior.  
  
2.  Na barra de endereço do navegador da Web, digite a URL do Gerenciador de Relatórios. Por padrão, a URL é http://\<*ComputerName*> / reports.  
  
### <a name="to-create-a-customized-clickthrough-report"></a>Para criar um relatório de clickthrough personalizado  
  
1.  Navegue até o modelo de relatório para o qual você quer adicionar o relatório de clickthrough personalizado.  
  
2.  Clique duas vezes no modelo de relatório.  
  
3.  Clique em **Clickthrough**.  
  
4.  Selecione a entidade para a qual você deseja anexar o relatório de clickthrough personalizado.  
  
    > [!NOTE]  
    >  Esta entidade deve ser igual à entidade básica do relatório de clickthrough personalizado.  
  
5.  Para exibir um relatório personalizado quando uma instância única da entidade selecionada é clicada, clique no botão **Procurar** do relatório de instância única.  
  
     -ou-  
  
     Para exibir um relatório personalizado quando uma instância múltipla da entidade selecionada é clicada, clique no botão **Procurar** do relatório de instância múltipla.  
  
6.  Selecione o relatório e clique em **OK**.  
  
7.  Clique em **Aplicar**.  
  
## <a name="see-also"></a>Consulte também  
 [Relatórios de Clickthrough &#40;SSRS&#41;](reports/clickthrough-reports-ssrs.md)  
  
  
