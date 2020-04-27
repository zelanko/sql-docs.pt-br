---
title: Parâmetros de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine analysis [Upgrade Advisor]
- SQL Server Upgrade Advisor, Database Engine
- Upgrade Advisor [SQL Server], Database Engine
- analyzing system [Upgrade Advisor], Database Engine
ms.assetid: 44a18bfe-e593-47a5-995f-382c01d3f618
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e528b94e51238a06a9776e58693c3093f4bfb831
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091874"
---
# <a name="sql-server-parameters"></a>Parâmetros do SQL Server
  Nesta página, é possível definir os parâmetros que o analisador usará para análise do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. É possível analisar um, vários ou todos os bancos de dados, analisar arquivos de rastreamento criados usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e analisar arquivos em lote do SQL.  
  
> [!NOTE]  
>  Alguns problemas de atualização poderão ser detectados somente se você submeter arquivos de rastreamento ou arquivos em lote do SQL à análise.  
  
## <a name="options"></a>Opções  
 **Banco(s) de dados a serem analisados**  
 Para analisar todos os bancos de dados, marque a caixa de seleção **todos os bancos de dados** . Para analisar uma seleção de bancos de dados, marque a caixa de seleção próxima a cada banco de dados para incluir na verificação.  
  
 **Analisar arquivo(s) de rastreamento**  
 Marque esta caixa de seleção para analisar arquivos de rastreamento no sistema de arquivos.  
  
 **Caminho do(s) arquivo(s) de rastreamento**  
 Você pode analisar um ou mais arquivos. É possível navegar até um local e selecionar vários arquivos ou fornecer vários nomes de arquivos. Use o nome do caminho completo para cada arquivo, incluindo o nome do arquivo, e separe as entrada usando o caractere barra vertical (|).  
  
 Se você habilitar **analisar arquivo (s) de rastreamento**, **Avançar** será desabilitado até que você insira um nome de caminho e um nome de arquivo.  
  
 **Analisar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] arquivo (s) em lotes**  
 Marque essa caixa de seleção para analisar arquivos em lote do [!INCLUDE[tsql](../../includes/tsql-md.md)] no sistema de arquivos.  
  
 **Caminho para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] arquivo (s) em lotes**  
 Você pode analisar um ou mais lotes de arquivos. Você pode navegar até um local e selecionar vários arquivos ou pode digitar vários nomes de arquivos. Use o nome do caminho completo para cada arquivo, incluindo o nome do arquivo, e separe as entrada usando o caractere barra vertical (|).  
  
 Se você habilitar **analisar arquivo (s) do lote SQL**, o botão **Avançar** será desabilitado até que você insira um nome de caminho e um nome de arquivo.  
  
 **Separador de Lotes do SQL**  
 O texto que é usado para separar lotes de instruções do [!INCLUDE[tsql](../../includes/tsql-md.md)]. O valor padrão é **go**.  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhando com o supervisor de atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Referência da interface de usuário do Supervisor de Atualização](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
