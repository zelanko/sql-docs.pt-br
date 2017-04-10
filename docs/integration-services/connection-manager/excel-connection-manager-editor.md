---
title: "Editor de Gerenciador de Conex&#245;es Excel | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.excelconnection.f1"
helpviewer_keywords: 
  - "Editor de Gerenciador de Conexões Excel"
ms.assetid: 7ff097e4-cafb-4885-a898-05b2a46628c1
caps.latest.revision: 32
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# Editor de Gerenciador de Conex&#245;es Excel
  Use a caixa de diálogo **Editor de Gerenciador de Conexões Excel** para adicionar uma conexão a um arquivo da pasta de trabalho novo ou existente do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)].  
  
 Para saber mais sobre o Gerenciador de Conexões Excel, consulte [Gerenciador de conexões do Excel](../../integration-services/connection-manager/excel-connection-manager.md).  
  
## Opções  
 **Caminho de arquivo do Excel**  
 Digite o caminho e nome de arquivo de um arquivo de pasta de trabalho do Excel (.xls) novo ou existente.  
  
> [!NOTE]  
>  Não é possível estabelecer conexão com um arquivo do Excel protegido por senha.  
  
> [!WARNING]  
>  O **Editor de Destinos do Excel** cria o arquivo do Excel automaticamente quando você seleciona uma **Conexão do Excel** que aponta para um arquivo novo ou inexistente e, em seguida, clica em **Novo** para **Nome da Folha de Excel**.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para navegar até a pasta na qual o arquivo Excel existe ou onde você deseja criar o novo arquivo.  
  
 **Versão do Excel**  
 Especifique a versão do Microsoft Excel que foi usada para criar o arquivo.  
  
 **Primeira linha com nomes de coluna**  
 Especifique se a primeira linha de dados na planilha selecionada contém os nomes de coluna. O valor padrão desta opção é **Verdadeiro**.  
  
## Provedores e drivers para o arquivo do Microsoft Excel e Access  
 Você precisará baixar os provedores OLE DB e drivers para arquivos do Microsoft Office se eles ainda não estiverem instalados. Versões mais recentes do provedor podem abrir arquivos criados em versões anteriores do Excel.  
  
 Se o computador tiver uma versão de 32 bits do Office, você precisará instalar a versão de 32 bits dos drivers e precisará também certificar-se de executar o assistente ou o pacote do Integration Services que ele cria no modo de 32 bits.  
  
|Versão do Microsoft Office|Download|  
|------------------------------|--------------|  
|2007|[2007 Office System Driver: componentes de conectividade de dados](https://www.microsoft.com/download/details.aspx?id=23734)|  
|2010|[Tempo de execução do Microsoft Access 2010](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2013|[Tempo de execução do Microsoft Access 2013](http://www.microsoft.com/download/details.aspx?id=39358)|  
|2016|[Tempo de execução do Microsoft Access 2016](https://www.microsoft.com/download/details.aspx?id=50040)|
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Loop através de arquivos e tabelas do Excel por meio de um contêiner Loop Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  