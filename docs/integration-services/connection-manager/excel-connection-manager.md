---
title: Gerenciador de conexões do Excel | Microsoft Docs
ms.date: 04/02/2018
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c36d49debc132b6e67b2bcbd2a37df75007419ff
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2018
---
# <a name="excel-connection-manager"></a>Gerenciador de conexões do Excel
  Um gerenciador de conexões do Excel permite a conexão de um pacote a um arquivo de pasta de trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel. A fonte e o destino do Excel que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui usam o gerenciador de conexões do Excel.  
 
> [!IMPORTANT]
> Para obter informações detalhadas sobre como se conectar a arquivos do Excel, e sobre limitações e problemas conhecidos para carregar dados de ou para arquivos do Excel, consulte [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md).

 Quando você adiciona um gerenciador de conexões do Excel a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que é resolvido como uma conexão do Excel em tempo de execução, define as propriedades do gerenciador de conexões e o adiciona à coleção **Coleções** no pacote.  
  
 A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **EXCEL**.  
  
## <a name="configure-the-excel-connection-manager"></a>Configurar o Gerenciador de conexões do Excel  
 Você pode configurar o gerenciador de conexões do Excel dos seguintes modos:  
  
-   Especificando o caminho do arquivo de pasta de trabalho Excel.  
  
-   Especificando a versão do Excel que foi usada para criar o arquivo.  
  
-   Indique se a primeira linha nas planilhas ou intervalos selecionados contém nomes de coluna.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor do Gerenciador de Conexões do Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="excel-connection-manager-editor"></a>Editor de Gerenciador de Conexões Excel
  Use a caixa de diálogo **Editor de Gerenciador de Conexões Excel** para adicionar uma conexão a um arquivo da pasta de trabalho novo ou existente do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] .  
  
### <a name="options"></a>Opções  
 **Caminho de arquivo do Excel**  
 Digite o caminho e o nome do arquivo de um arquivo de pasta de trabalho novo ou existente do Excel.  
   
 **Procurar**  
 Use a caixa de diálogo **Abrir** para navegar até a pasta na qual o arquivo Excel existe ou na qual você deseja criar o novo arquivo.  
  
 **Versão do Excel**  
 Especifique a versão do Microsoft Excel que foi usada para criar o arquivo.  
  
 **Primeira linha com nomes de coluna**  
 Especifique se a primeira linha de dados na planilha selecionada contém os nomes de coluna. O valor padrão desta opção é **Verdadeiro**.  
  
## <a name="related-tasks"></a>Related Tasks  
[Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md)  
[Origem do Excel](../data-flow/excel-source.md)  
[Destino do Excel](../data-flow/excel-destination.md)
