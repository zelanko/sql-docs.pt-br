---
title: 'Lição 2: Gerar Classes de esquema RDL usando a ferramenta xsd | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a81c87f1-7977-4b30-b6ac-b38b3e2b6398
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f5f74c6621d329885e9149fce9a37c7418d9c37b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025197"
---
# <a name="lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool"></a>Lição 2: Gerar Classes de esquema RDL usando a ferramenta xsd
  Depois que você criar seu projeto do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], a próxima etapa será recuperar uma cópia local do esquema de definição de relatório e executar a Ferramenta de Definição de Esquema XML (Xsd.exe).  
  
### <a name="to-generate-the-rdl-classes"></a>Para gerar as classes RDL  
  
1.  Abra uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] do Internet Explorer (ou navegador da Web equivalente) e navegue até a URL a seguir:  
  
    ```  
    https://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition/ReportDefinition.xsd  
    ```  
  
2.  Depois que o esquema RDL tiver sido aberto no navegador, navegue até a **arquivo** menu e selecione **Salvar como**.  
  
3.  Navegue até o local em que você criou o projeto do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e salve o esquema com o nome de arquivo ReportDefinition.xsd.  
  
4.  Depois que o arquivo foi salvo, abra uma instância da [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] prompt de comando. Para abrir uma instância do prompt de comando, clique no menu Iniciar, aponte para **todos os programas**, aponte para **Microsoft Visual Studio 2010**, aponte para **ferramentas do Visual Studio** e clique em **Prompt de comando do visual Studio (2010)**.  
  
5.  Altere o caminho atual para o local em que você salvou o arquivo ReportDefinition.xsd:  
  
     `CD\<ReportDefinition.xsd Path>`  
  
6.  Gere o arquivo ReportDefinition.cs que contém as classes para o esquema RDL com o seguinte comando:  
  
     `xsd /c /n:SampleRDLSchema ReportDefinition.xsd`  
  
     Para gerar um arquivo ReportDefinition.vb, use este comando:  
  
     `xsd /c /l:VB /n:SampleRDLSchema ReportDefinition.xsd`  
  
7.  Adicionar ReportDefinition.xsd a seu projeto. Dos **Project** menu, clique em **Add Existing Item**. Navegue até o local do arquivo Reportdefinition XSD, selecione Reportdefinition e clique em **adicionar**.  
  
    > [!NOTE]  
    >  Depois de adicionar o arquivo Reportdefinition XSD ao projeto, você observará na **Gerenciador de soluções** que o arquivo ReportDefinition.cs (. vb) não está lá. Para exibir o arquivo, clique no botão expandir/recolher ao lado do arquivo ReportDefinition.xsd.  
  
## <a name="next-lesson"></a>Próxima lição  
 Na próxima lição, você escreverá código para carregar uma definição de relatório de um servidor de relatório usando as classes geradas com base no esquema RDL. Consulte [lição 3: Carregar uma definição de relatório do servidor de relatório](../../2014/tutorials/lesson-3-load-a-report-definition-from-the-report-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [Atualizando relatórios por meio de Classes geradas a partir do esquema RDL &#40;Tutorial do SSRS&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [Linguagem RDL &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
