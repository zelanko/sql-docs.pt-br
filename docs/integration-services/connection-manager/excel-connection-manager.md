---
title: "Gerenciador de conex&#245;es do Excel | Microsoft Docs"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "arquivos [Integration Services], conexões"
  - "conexões [Integration Services], Excel"
  - "Excel [Integration Services]"
  - "gerenciadores de conexões [Integration Services], Excel"
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 41
---
# Gerenciador de conex&#245;es do Excel
  Um gerenciador de conexão do Excel permite a conexão de um pacote a um arquivo de pasta de trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel existente. A fonte e o destino do Excel que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui usam o gerenciador de conexões do Excel.  
  
 Quando você adiciona um gerenciador de conexões do Excel a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que é resolvido como uma conexão do Excel em tempo de execução, define as propriedades do gerenciador de conexões e o adiciona à coleção **Coleções** no pacote.  
  
 A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **EXCEL**.  
  
## Configuração do gerenciador de conexões do Excel  
 Você pode configurar o gerenciador de conexões do Excel dos seguintes modos:  
  
-   Especificando o caminho do arquivo de pasta de trabalho Excel.  
  
    > [!NOTE]  
    >  Não é possível estabelecer conexão com um arquivo do Excel protegido por senha.  
  
-   Especificando a versão do Excel que foi usada para criar o arquivo.  
  
-   Indicando se a primeira linha de dados acessados nas planilhas ou intervalos selecionados contém nomes de coluna.  
  
 Se o gerenciador de conexões do Excel for usado por uma origem do Excel, os nomes das colunas serão incluídos junto com os dados extraídos. Se for usado por um destino do Excel, os nomes das colunas serão incluídos nos dados gravados.  
  
 Para obter mais informações sobre o comportamento de fontes e destinos do Excel, consulte [Origem do Excel](../../integration-services/data-flow/excel-source.md) e [Destino do Excel](../../integration-services/data-flow/excel-destination.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)], consulte [Editor do Gerenciador de Conexões do Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
 Para obter informações sobre loop através de um grupo de arquivos do Excel, consulte [Loop por meio de arquivos do Excel e tabelas usando um contêiner de Loop Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md).  
  
## Tarefas relacionadas  
  
-   [Loop através de arquivos e tabelas do Excel por meio de um contêiner Loop Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
-   [Conectar-se a uma pasta de trabalho do Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
  