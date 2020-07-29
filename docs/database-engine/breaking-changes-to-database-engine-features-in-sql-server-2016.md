---
title: 'Mecanismo de Banco de Dados: Alterações mais recentes | Microsoft Docs'
titleSuffix: SQL Server 2016
description: Saiba mais sobre as alterações do Mecanismo de Banco de Dados no SQL Server 2016 (13.x) e anteriores que podem interromper a funcionalidade da versão anterior ao atualizar.
ms.custom: seo-lt-2019
ms.date: 07/22/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], what's new
- breaking changes [SQL Server]
ms.assetid: 47edefbd-a09b-4087-937a-453cd5c6e061
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bddfd0b06bfc64d68534548cfb90ea09ed2d4076
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87235965"
---
# <a name="breaking-changes-to-database-engine-features-in-sql-server-2016"></a>Alterações mais recentes a recursos do Mecanismo de Banco de Dados no SQL Server 2016

[!INCLUDE [SQL Server 2016](../includes/applies-to-version/sqlserver2016.md)]  

  Este tópico descreve as últimas alterações no [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] e versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Essas alterações podem danificar aplicativos, scripts ou funcionalidades baseados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Talvez você tenha esses problemas ao atualizar.  
  
##  <a name="breaking-changes-in-sssql15"></a><a name="SQL15"></a> Últimas alterações do [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]  
  
-   A coluna *sample_ms* de `sys.dm_io_virtual_file_stats` foi expandida de um tipo de dados **int** para um **bigint**.  
  
-   A coluna *TimeStamp* de `sys.fn_virtualfilestats` foi expandida de um tipo de dados **int** para um **bigint**.  

-   No nível de compatibilidade 130 do banco de dados, as conversões implícitas de tipos de dados **datetime** para **datetime2** demonstram precisão aprimorada ao considerar os milissegundos fracionários, resultando em diferentes valores convertidos. Use conversão explícita para o tipo de dados datetime2 sempre que existir um cenário misto de comparação entre os tipos de dados datetime e datetime2. Para obter mais informações, veja este [Artigo de Suporte da Microsoft](https://support.microsoft.com/help/4010261).

-   No nível de compatibilidade 130 do banco de dados, as operações que realizam conversões implícitas entre determinados tipos de dados numéricos e datetime mostram uma precisão aprimorada e podem resultar em diferentes valores convertidos. Isso inclui o uso de funções que exigem cálculos como, por exemplo, `DATEDIFF` e `ROUND`. Para obter mais informações, veja este [Artigo de Suporte da Microsoft](https://support.microsoft.com/help/4010261).

## <a name="previous-versions"></a><a name="previous-versions"></a> Versões anteriores  

Para obter informações sobre alterações da falha no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] e em algumas versões anteriores, confira [Alterações da falha em recursos do mecanismo de banco de dados no SQL Server 2014](/previous-versions/sql/2014/database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016).

#### <a name="archived-documentation-for-very-old-versions-of-sql-server"></a>Documentação arquivada de versões muito antigas do SQL Server

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>Consulte Também  
 [Recursos do Mecanismo de Banco de Dados preteridos no SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Funcionalidade do Mecanismo de Banco de Dados descontinuada no SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Compatibilidade com versões anteriores do Mecanismo de Banco de Dados do SQL Server](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [Melhorias do SQL Server 2016 ou SQL Server 2017 no Windows referentes ao tratamento de alguns tipos de dados e operações incomuns](https://support.microsoft.com/help/4010261)   
