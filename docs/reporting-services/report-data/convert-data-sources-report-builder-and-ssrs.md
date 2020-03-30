---
title: Converter fontes de dados (Construtor de Relatórios) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], embedded
- data sources [Reporting Services], shared
ms.assetid: 0e099c7e-8c03-43eb-9ea3-76e52d9ebbe3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 05aee467c3e69c115bedfa498a546a4e1664ba71
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081754"
---
# <a name="convert-data-sources-report-builder-and-ssrs"></a>Converter fontes de dados (Construtor de Relatórios e SSRS)
  Cada fonte de dados no painel de dados do relatório é inserida e específica do relatório ou é compartilhada. No Construtor de Relatórios, uma fonte de dados compartilhada aponta para uma fonte de dados compartilhada publicada em um servidor de relatório ou no site do SharePoint. No Designer de Relatórios, uma fonte de dados compartilhada aponta para uma fonte de dados compartilhada na pasta **Fontes de Dados Compartilhadas** do Gerenciador de Soluções.  
  
 Para obter mais informações sobre as diferenças entre fontes de dados inseridas e compartilhadas, consulte [Conexões de dados ou fontes de dados inseridas e compartilhadas &#40;Construtor de Relatórios e SSRS&#41;](https://msdn.microsoft.com/library/f417782c-b85a-4c4d-8a40-839176daba56).  
  
 Para obter mais informações sobre como criar uma fonte de dados compartilhada, consulte [Criar uma fonte de dados inserida ou compartilhada &#40;SSRS&#41;](https://msdn.microsoft.com/library/b111a8d0-a60d-4c8b-b00a-51644b19c34b).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-designer"></a>Designer de Relatórios  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>Para converter uma fonte de dados inserida em compartilhada  
  
-   No painel Dados do Relatório, clique com o botão direito do mouse na fonte de dados e clique em **Converter em Fonte de Dados Compartilhada**.  
  
    > [!NOTE]  
    >  Se o painel Dados do Relatório não estiver visível, no menu **Exibir** , clique em **Dados do Relatório**. Se o painel for aberto como uma janela flutuante, você poderá encaixá-la. Para obter mais informações, consulte [Encaixar o painel de dados do relatório no Designer de Relatórios &#40;SSRS&#41;](../../reporting-services/tools/dock-the-report-data-pane-in-report-designer-ssrs.md).  
  
     No painel de dados do relatório, o ícone da fonte de dados muda para o ícone de fonte de dados compartilhada. No Gerenciador de Soluções, uma fonte de dados compartilhada com o mesmo nome é exibida na pasta **Fonte de Dados Compartilhada** .  
  
### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>Para converter uma fonte de dados de compartilhada em inserida  
  
-   No painel Dados do Relatório, clique com o botão direito do mouse na fonte de dados, abra a caixa de diálogo **Propriedades da Fonte de Dados** e clique em **Conexão Inserida**. Insira as informações necessárias.  
  
     No painel de dados do relatório, o ícone da fonte de dados muda para o ícone de fonte de dados compartilhada.  
  
## <a name="report-builder"></a>Construtor de Relatórios  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>Para converter uma fonte de dados inserida em compartilhada  
  
-   No painel Dados do Relatório, clique com o botão direito do mouse na fonte de dados para abrir a caixa de diálogo **Propriedades da Fonte de Dados** e clique em **Conexão Inserida**. Insira as informações necessárias.  
  
     No painel de dados do relatório, o ícone da fonte de dados muda para o ícone de fonte de dados compartilhada.  
  
#### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>Para converter uma fonte de dados de compartilhada em inserida  
  
-   No painel Dados do Relatório, clique com o botão direito do mouse na fonte de dados, abra a caixa de diálogo **Propriedades da Fonte de Dados** e clique em **Conexão Inserida**. Insira as informações necessárias.  
  
     No painel de dados do relatório, o ícone da fonte de dados muda para o ícone de fonte de dados compartilhada.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar fontes de dados de relatório](../../reporting-services/report-data/manage-report-data-sources.md)   
 [Criar cadeias de conexão de dados – Construtor de Relatórios e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
