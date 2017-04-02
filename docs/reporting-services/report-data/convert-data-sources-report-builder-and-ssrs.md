---
title: "Converter fontes de dados (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "fontes de dados [Reporting Services], incorporadas"
  - "fontes de dados [Reporting Services], compartilhadas"
ms.assetid: 0e099c7e-8c03-43eb-9ea3-76e52d9ebbe3
caps.latest.revision: 16
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 16
---
# Converter fontes de dados (Construtor de Relat&#243;rios e SSRS)
  Cada fonte de dados no painel de dados do relatório é inserida e específica do relatório ou é compartilhada. No Construtor de Relatórios, uma fonte de dados compartilhada aponta para uma fonte de dados compartilhada publicada em um servidor de relatório ou no site do SharePoint. No Designer de Relatórios, uma fonte de dados compartilhada aponta para uma fonte de dados compartilhada na pasta **Fontes de Dados Compartilhadas** do Gerenciador de Soluções.  
  
 Para obter mais informações sobre as diferenças entre fontes de dados inseridas e compartilhadas, consulte [Conexões de dados ou fontes de dados inseridas e compartilhadas &#40;Construtor de Relatórios e SSRS&#41;](../Topic/Embedded%20and%20Shared%20Data%20Connections%20or%20Data%20Sources%20\(Report%20Builder%20and%20SSRS\).md).  
  
 Para obter mais informações sobre como criar uma fonte de dados compartilhada, consulte [Criar uma fonte de dados inserida ou compartilhada &#40;SSRS&#41;](../Topic/Create%20an%20Embedded%20or%20Shared%20Data%20Source%20\(SSRS\).md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Designer de Relatórios  
  
#### Para converter uma fonte de dados inserida em compartilhada  
  
-   No painel Dados do Relatório, clique com o botão direito do mouse na fonte de dados e clique em **Converter em Fonte de Dados Compartilhada**.  
  
    > [!NOTE]  
    >  Se o painel Dados do Relatório não estiver visível, no menu **Exibir**, clique em **Dados do Relatório**. Se o painel for aberto como uma janela flutuante, você poderá encaixá-la. Para obter mais informações, consulte [Encaixar o painel de dados do relatório no Designer de Relatórios &#40;SSRS&#41;](../../reporting-services/tools/dock-the-report-data-pane-in-report-designer-ssrs.md).  
  
     No painel de dados do relatório, o ícone da fonte de dados muda para o ícone de fonte de dados compartilhada. No Gerenciador de Soluções, uma fonte de dados compartilhada com o mesmo nome é exibida na pasta **Fonte de Dados Compartilhada**.  
  
### Para converter uma fonte de dados de compartilhada em inserida  
  
-   No painel Dados do Relatório, clique com o botão direito do mouse na fonte de dados, abra a caixa de diálogo **Propriedades da Fonte de Dados** e clique em **Conexão Inserida**. Digite as informações necessárias.  
  
     No painel de dados do relatório, o ícone da fonte de dados muda para o ícone de fonte de dados compartilhada.  
  
## Construtor de Relatórios  
  
#### Para converter uma fonte de dados inserida em compartilhada  
  
-   No painel Dados do Relatório, clique com o botão direito do mouse na fonte de dados para abrir a caixa de diálogo **Propriedades da Fonte de Dados** e clique em **Conexão Inserida**. Digite as informações necessárias.  
  
     No painel de dados do relatório, o ícone da fonte de dados muda para o ícone de fonte de dados compartilhada.  
  
#### Para converter uma fonte de dados de compartilhada em inserida  
  
-   No painel Dados do Relatório, clique com o botão direito do mouse na fonte de dados, abra a caixa de diálogo **Propriedades da Fonte de Dados** e clique em **Conexão Inserida**. Digite as informações necessárias.  
  
     No painel de dados do relatório, o ícone da fonte de dados muda para o ícone de fonte de dados compartilhada.  
  
## Consulte também  
 [Gerenciar fontes de dados de relatório](../../reporting-services/report-data/manage-report-data-sources.md)   
 [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  