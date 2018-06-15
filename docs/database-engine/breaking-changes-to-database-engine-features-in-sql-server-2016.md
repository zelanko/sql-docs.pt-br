---
title: Alterações interruptivas em recursos do Mecanismo de Banco de Dados no SQL Server 2016 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: sql
ms.prod_service: high-availability
ms.component: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], what's new
- breaking changes [SQL Server]
ms.assetid: 47edefbd-a09b-4087-937a-453cd5c6e061
caps.latest.revision: 144
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 191155643b072cc2963d3de5e4b1651e219e35f0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32863231"
---
# <a name="breaking-changes-to-database-engine-features-in-sql-server-2016"></a>Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve as últimas alterações no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] e versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Essas alterações podem danificar aplicativos, scripts ou funcionalidades baseados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Talvez você tenha esses problemas ao atualizar.  
  
##  <a name="SQL15"></a> Últimas alterações do [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]  
  
-   A coluna sample_ms de sys.dm_io_virtual_file_stats foi expandida de um tipo de dados **int** para um **bigint** .  
  
-   A coluna TimeStamp de sys.fn_virtualfilestats foi expandida de um tipo de dados **int** para um **bigint** .  

-   O uso dos algoritmos de hash de MD2, MD4, MD5, SHA ou SHA1 (não recomendados) requer a definição do nível de compatibilidade do banco de dados para anterior a 130.  

-   No nível de compatibilidade 130 do banco de dados, as conversões implícitas de tipos de dados **datetime** para **datetime2** demonstram precisão aprimorada ao considerar os milissegundos fracionários, resultando em diferentes valores convertidos. Use conversão explícita para o tipo de dados datetime2 sempre que existir um cenário misto de comparação entre os tipos de dados datetime e datetime2. Para obter mais informações, consulte este [Artigo do Suporte da Microsoft](http://support.microsoft.com/help/4010261).
  
## <a name="previous-versions"></a>Versões anteriores  
  
-   [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2014](https://msdn.microsoft.com/library/ms143179\(v=sql.120\))  
  
-   [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2012](https://msdn.microsoft.com/library/ms143179\(v=sql.110\))  
  
-   [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2008](https://msdn.microsoft.com/library/ms143179\(v=sql.100\))  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do Mecanismo de Banco de Dados preteridos no SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Funcionalidade do Mecanismo de Banco de Dados descontinuada no SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Compatibilidade com versões anteriores do Mecanismo de Banco de Dados do SQL Server](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [Melhorias do SQL Server 2016 ou SQL Server 2017 no Windows referentes ao tratamento de alguns tipos de dados e operações incomuns](http://support.microsoft.com/help/4010261)
  
  
