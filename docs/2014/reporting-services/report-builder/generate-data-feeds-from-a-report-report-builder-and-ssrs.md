---
title: Gerar feeds de dados com base em um relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e68baae2-9f2a-4f13-9179-9ac7f29111c5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ceca9ef914afeab3420bbd35c46c582c112644dc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107845"
---
# <a name="generate-data-feeds-from-a-report-report-builder-and-ssrs"></a>Gerar feeds de dados de um relatório (Construtor de Relatórios e SSRS)
  Você pode gerar feeds de dados em conformidade com Atom a partir de relatórios e, em seguida, usar os feeds de dados em aplicativos, como o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cliente, que pode consumir feeds de dados.  
  
 A extensão de renderização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Atom gera um documento de serviço Atom que lista os feeds de dados disponíveis a partir de um relatório. O documento lista pelo menos um feed de dados para cada região no relatório. Dependendo do tipo de região de dados e dos dados que a região de dados exibe, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pode gerar vários feeds de dados de uma região de dados.  
  
 O documento de serviço Atom contém um identificador exclusivo para cada feed de dados e você usa o identificador em uma URL para exibir o conteúdo do feed de dados.  
  
 Para obter mais informações, consulte [Gerando feeds de dados de relatórios &#40;Construtor de Relatórios e SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-generate-an-atom-service-document"></a>Para gerar um documento de serviço Atom  
  
1.  Na página **inicial** do Gerenciador de Relatórios, navegue até o relatório do qual você deseja gerar feeds de dados.  
  
2.  Clique no relatório.  
  
     O relatório é executado.  
  
3.  Na barra de ferramentas, clique no ícone Exportar para Feed de Dados.  
  
     Uma mensagem é exibida perguntando se você deseja salvar ou abrir o documento Atom que contém o feed de dados.  
  
4.  Clique em **Salvar** para salvar o documento no sistema de arquivos, ou clique em **Abrir** para exibir o conteúdo do documento antes de salvá-lo. **Por padrão, o documento é aberto em um navegador.**  
  
5.  Navegue até o local onde o documento será salvo.  
  
6.  Outra opção é alterar o nome do documento.  
  
    > [!NOTE]  
    >  Por padrão, o nome do documento é o nome do relatório.  
  
7.  Verifique se o tipo do documento é **Arquivo ATOMSVC**e clique em **Salvar**.  
  
8.  Opcionalmente, abra o arquivo .atomsvc em um navegador, editor de texto ou editor de XML.  
  
### <a name="to-view-an-atom-compliant-data-feed"></a>Para exibir um feed de dados compatível com Atom  
  
1.  Se o documento de serviço Atom ainda não estiver aberto, localize-o e abra-o em um navegador como o Internet Explorer.  
  
2.  Copie no navegador a URL do feed de dados a ser exibida a partir do documento de serviço Atom.  
  
     Este é o formato da URL:  
  
 `http://<server name>/ReportServer?%2f<ReportName>rs%3aCommand=Render&rs%3aFormat=ATOM&rc%3aDataFeed=<Identifier>`  
  
1.  Pressione ENTER.  
  
     Uma mensagem é exibida perguntando se você deseja salvar ou abrir o documento Atom que contém o feed de dados.  
  
2.  Clique em **Salvar** para salvar o documento no sistema de arquivos, ou clique em **Abrir** para exibir o feed de dados antes de salvar o documento.  
  
3.  Navegue até o local onde o documento será salvo.  
  
4.  Outra opção é alterar o nome do documento.  
  
    > [!NOTE]  
    >  Por padrão, o nome do documento é o nome do relatório. Se o documento de serviço Atom tiver vários feeds, por padrão todos usarão o mesmo nome, o nome do relatório. Para diferenciá-los, renomeie-os para usar nomes significativos.  
  
5.  Verifique se o tipo do documento é **Arquivo ATOM**e clique em **Salvar**.  
  
6.  Opcionalmente, abra o arquivo .atom em um navegador, editor de texto ou editor de XML.  
  
## <a name="see-also"></a>Consulte Também  
 [Exportando relatórios &#40;Construtor de Relatórios e SSRS&#41;](export-reports-report-builder-and-ssrs.md)  
  
  
