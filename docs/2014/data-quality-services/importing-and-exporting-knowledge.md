---
title: Importando e exportando conhecimento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 12537c9d-31e4-40b0-a411-cb343abbe96a
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2cc9c9576a6ae2f70f2d54d48471339ec07d0e61
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480530"
---
# <a name="importing-and-exporting-knowledge"></a>Importando e exportando conhecimento
  Você pode criar bases de dados de conhecimento e domínios diretamente no aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] ou exportar/importar o conhecimento da/para a base de dados de conhecimento. No aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , você pode usar um arquivo de dados nas operações de importação e exportação ou um arquivo do Excel nas operações de importação. O arquivo de dados usado é um arquivo criptografado criado através do [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) com uma extensão .dqs. Os arquivos criados pelo Microsoft Excel podem ter a extensão .xlsx, .xls ou .csv. Essas operações lhe dão mais flexibilidade na compilação e no compartilhamento do conhecimento usado para executar a limpeza e a correspondência de dados.  
  
> [!IMPORTANT]  
>  Você pode exportar *todas* as bases de dados de conhecimento do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] para um arquivo de backup do DQS (.dqsb) simultaneamente, executando o arquivo DQSInstaller.exe no prompt de comando. Da mesma forma, você pode importar *todas* as bases de dados de conhecimento de um arquivo de backup do DQS (.dqsb) para o [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] simultaneamente, executando o arquivo DQSInstaller.exe no prompt de comando. Para obter mais informações sobre como fazer isso, consulte [Exportar e importar bases de dados de conhecimento DQS usando o DQSInstaller.exe](install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md) no guia de instalação do DQS.  
  
## <a name="in-this-section"></a>Nesta seção  
 Você pode executar as seguintes operações de importação e exportação:  
  
|||  
|-|-|  
|Exportar um domínio de uma base de dados de conhecimento para um arquivo de dados .dqs|[Exportar um domínio para um arquivo .dqs](../../2014/data-quality-services/export-a-domain-to-a-dqs-file.md)|  
|Importar um domínio de um arquivo de dados .dqs para uma base de dados de conhecimento existente|[Importar um domínio de um arquivo .dqs](../../2014/data-quality-services/import-a-domain-from-a-dqs-file.md)|  
|Exportar uma base de dados de conhecimento inteira para um arquivo de dados .dqs.|[Exportar uma base de dados de conhecimento para um arquivo .dqs](../../2014/data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)|  
|Importar uma base de dados de conhecimento inteira para um arquivo de dados .dqs.|[Importar uma base de dados de conhecimento de um arquivo .dqs](../../2014/data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)|  
|Importar valores de um arquivo do Excel para um domínio.|[Importar valores de um arquivo do Excel para um domínio](../../2014/data-quality-services/import-values-from-an-excel-file-into-a-domain.md)|  
|Importar domínios de um arquivo do Excel para uma base de dados de conhecimento|[Importar domínios de um arquivo do Excel na descoberta da base de dados de conhecimento](../../2014/data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md)|  
|Importar o conhecimento coletado durante a limpeza para uma base de dados de conhecimento|[Importar valores de projeto de limpeza para um domínio](../../2014/data-quality-services/import-cleansing-project-values-into-a-domain.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar uma base de dados de conhecimento executando a descoberta da base de dados de conhecimento e gerenciando o conhecimento de modo interativo|[Criar uma base de dados de conhecimento](../../2014/data-quality-services/building-a-knowledge-base.md)|  
|Criar um domínio único e adicionar conhecimento ao domínio.|[Gerenciar um domínio](../../2014/data-quality-services/managing-a-domain.md)|  
|Criar um domínio composto e adicionar conhecimento ao domínio.|[Gerenciar um domínio de composição](../../2014/data-quality-services/managing-a-composite-domain.md)|  
  
  
