---
title: Gerenciador de conexões do Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 08cc1263c5d16df9b078e583d1c1e311f3747703
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438483"
---
# <a name="excel-connection-manager"></a>Gerenciador de conexões do Excel
  Um gerenciador de conexão do Excel permite a conexão de um pacote a um arquivo de pasta de trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel existente. A origem do Excel e o destino do Excel que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluem usar o Gerenciador de conexões do Excel.  
  
 Quando você adiciona um gerenciador de conexões do Excel a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que é resolvido como uma conexão do Excel em tempo de execução, define as propriedades do gerenciador de conexões e o adiciona à coleção `Connections` no pacote.  
  
 A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `EXCEL`.  
  
> [!NOTE]  
>  Não é possível estabelecer conexão com um arquivo do Excel protegido por senha.  
  
## <a name="configuration-of-the-excel-connection-manager"></a>Configuração do gerenciador de conexões do Excel  
 Você pode configurar o gerenciador de conexões do Excel dos seguintes modos:  
  
-   Especificando o caminho do arquivo de pasta de trabalho Excel.  
  
-   Especificando a versão do Excel que foi usada para criar o arquivo.  
  
-   Indicando se a primeira linha de dados acessados nas planilhas ou intervalos selecionados contém nomes de coluna.  
  
 Se o gerenciador de conexões do Excel for usado por uma origem do Excel, os nomes das colunas serão incluídos junto com os dados extraídos. Se for usado por um destino do Excel, os nomes das colunas serão incluídos nos dados gravados.  
  
 O gerenciador de conexões do Excel usa o [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet 4.0 e o driver de método de acesso sequencial indexado (ISAM) do Excel para se conectar, ler e gravar dados nas fontes de dados do Excel. Para obter mais informações sobre o comportamento desse provedor e driver quando usado com fontes do Excel e destinos do Excel, consulte [origem do Excel](../data-flow/excel-source.md) e [destino do Excel](../data-flow/excel-destination.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor do Gerenciador de Conexões do Excel](../excel-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
 Para obter informações sobre loop através de um grupo de arquivos do Excel, consulte [Loop por meio de arquivos do Excel e tabelas usando um contêiner de Loop Foreach](../control-flow/foreach-loop-container.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Loop por meio de arquivos do Excel e tabelas usando um contêiner de Loop Foreach](../control-flow/foreach-loop-container.md)  
  
-   [Importar dados do Excel ou exportar dados para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md)
  
  
