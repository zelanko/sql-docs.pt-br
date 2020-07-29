---
title: Arquivos que gerenciam soluções e projetos
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], files
- .ssmssln files
- .ssmsmobileproj files
- .ssmsasproj files
- .ssmssqlproj files
- .sqlsuo files
- files [SQL Server Management Studio], projects
ms.assetid: e19d2859-0b97-4727-ac27-c4c226d86b2f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bec1f5859162d2438d2db137ef0637fc4900b32b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000839"
---
# <a name="files-that-manage-solutions-and-projects"></a>Arquivos que gerenciam soluções e projetos
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
 Este tópico descreve os tipos de arquivos específicos para o [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Por padrão, todas as soluções e seus projetos são criados em \Meus Documentos\SQL Server Management Studio Projects.  


## <a name="management-studio-solution-files"></a>Arquivos de solução do Management Studio  
O [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa tipos de arquivo diferentes em comparação com o [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] ou o [!INCLUDE[msCoName](../../includes/msconame_md.md)] Visual Studio. Isso significa que você não pode abrir uma solução [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] ou não Visual Studio. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Os arquivos da solução permitem que o Gerenciador de Soluções exiba uma interface gráfica para gerenciar seus arquivos.  
   
|Extensão|Tipo de arquivo|DESCRIÇÃO|Criado por|  
|-------------|-------------|---------------|--------------|  
|.ssmssln|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Objeto de solução|Fornece o ambiente com referências ao local em disco de projetos, itens de projeto e soluções do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
  
## <a name="management-studio-project-files"></a>Arquivos de projeto do Management Studio  
Da mesma forma que as soluções contêm arquivos que gerenciam os objetos da solução, os projetos contêm arquivos de projeto. O tipo de arquivo de projeto que o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] cria para um projeto depende do modelo usado para criar o projeto. A tabela a seguir descreve o tipo de arquivo criado para cada projeto.  
   
|Extensão|Modelo do projeto|  
|-------------|--------------------|  
|.ssmssqlproj|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Projeto de scripts|  
|.ssmsasproj|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] Projeto de scripts|  
   
## <a name="location-of-solution-level-files"></a>Local dos arquivos do nível da solução  
Por padrão, arquivos do nível da solução são criados no diretório físico do primeiro projeto criado com a solução. Você pode especificar um diretório para a solução criando uma solução, ou especificar o diretório ao criar um projeto novo.  
 
Se você tiver uma estrutura de diretórios semelhante à estrutura lógica mostrada no Gerenciador de Soluções, os arquivos de projeto e solução serão mais fáceis de localizar e compartilhar com outros desenvolvedores em uma equipe.  
   
## <a name="see-also"></a>Consulte Também  
[Gerenciar arquivos com codificação](../../ssms/solution/manage-files-with-encoding.md)  
[Arquivos diversos](../../ssms/solution/miscellaneous-files.md)  
[Gerenciador de Soluções](../../ssms/solution/solution-explorer.md)  
[Soluções &#40;SQL Server Management Studio&#41;](../../ssms/solution/solutions-sql-server-management-studio.md)  
[Projetos &#40;SQL Server Management Studio&#41;](../../ssms/solution/projects-sql-server-management-studio.md)  
[Controle do código-fonte do Gerenciador de Soluções](https://msdn.microsoft.com/library/ms173879.aspx)  
  
