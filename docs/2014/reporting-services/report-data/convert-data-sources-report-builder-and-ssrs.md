---
title: Converter uma fonte de dados inserida em compartilhada (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], embedded
- data sources [Reporting Services], shared
ms.assetid: 0e099c7e-8c03-43eb-9ea3-76e52d9ebbe3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 64879a7ab82f509f129cf43ab50c1cdbb3b7f913
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107407"
---
# <a name="convert-a-data-source-from-embedded-to-shared-report-builder-and-ssrs"></a>Converter uma fonte de dados inserida em compartilhada (Construtor de Relatórios e SSRS)
  Cada fonte de dados no painel de dados do relatório é inserida e específica do relatório ou é compartilhada. No Construtor de Relatórios, uma fonte de dados compartilhada aponta para uma fonte de dados compartilhada publicada em um servidor de relatório ou no site do SharePoint. No Designer de Relatórios, uma fonte de dados compartilhada aponta para uma fonte de dados compartilhada na pasta **Fontes de Dados Compartilhadas** do Gerenciador de Soluções.  
  
 Para obter mais informações sobre as diferenças entre fontes de dados inseridas e compartilhadas, consulte [Conexões de dados ou fontes de dados inseridas e compartilhadas &#40;Construtor de Relatórios e SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md).  
  
 Para obter mais informações sobre como criar uma fonte de dados compartilhada, consulte [Criar uma fonte de dados inserida ou compartilhada &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-designer"></a>Designer de Relatórios  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>Para converter uma fonte de dados inserida em compartilhada  
  
-   No painel Dados do Relatório, clique com o botão direito do mouse na fonte de dados e clique em **Converter em Fonte de Dados Compartilhada**.  
  
    > [!NOTE]  
    >  Se o painel Dados do Relatório não estiver visível, no menu **Exibir** , clique em **Dados do Relatório**. Se o painel for aberto como uma janela flutuante, você poderá encaixá-la. Para obter mais informações, consulte [Encaixar o painel de dados do relatório no Designer de Relatórios &#40;SSRS&#41;](../tools/dock-the-report-data-pane-in-report-designer-ssrs.md).  
  
     No painel de dados do relatório, o ícone da fonte de dados muda para o ícone de fonte de dados compartilhada. No Gerenciador de Soluções, uma fonte de dados compartilhada com o mesmo nome é exibida na pasta **Fonte de Dados Compartilhada** .  
  
### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>Para converter uma fonte de dados de compartilhada em inserida  
  
-   No painel Dados do Relatório, clique com o botão direito do mouse na fonte de dados, abra a caixa de diálogo **Propriedades da Fonte de Dados** e clique em **Conexão Inserida**. Digite as informações necessárias.  
  
     No painel de dados do relatório, o ícone da fonte de dados muda para o ícone de fonte de dados compartilhada.  
  
## <a name="report-builder"></a>Construtor de Relatórios  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>Para converter uma fonte de dados inserida em compartilhada  
  
-   No painel Dados do Relatório, clique com o botão direito do mouse na fonte de dados para abrir a caixa de diálogo **Propriedades da Fonte de Dados** e clique em **Conexão Inserida**. Digite as informações necessárias.  
  
     No painel de dados do relatório, o ícone da fonte de dados muda para o ícone de fonte de dados compartilhada.  
  
#### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>Para converter uma fonte de dados de compartilhada em inserida  
  
-   No painel Dados do Relatório, clique com o botão direito do mouse na fonte de dados, abra a caixa de diálogo **Propriedades da Fonte de Dados** e clique em **Conexão Inserida**. Digite as informações necessárias.  
  
     No painel de dados do relatório, o ícone da fonte de dados muda para o ícone de fonte de dados compartilhada.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar fontes de dados de relatório](manage-report-data-sources.md)   
 [Conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  
