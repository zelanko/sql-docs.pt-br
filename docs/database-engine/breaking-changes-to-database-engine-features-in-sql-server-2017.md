---
title: Alterações interruptivas em recursos do Mecanismo de Banco de Dados no SQL Server 2017 | Microsoft Docs
description: Alterações interruptivas em recursos do Mecanismo de Banco de Dados no SQL Server 2017
ms.date: 04/19/2017
ms.prod: sql
ms.prod_service: high-availability
ms.component: database-engine
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- breaking changes 2017 [SQL Server]
ms.assetid: ''
caps.latest.revision: 1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: d0477ddabf1a2691ef444e99dc7ca662a05abb1b
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40406132"
---
# <a name="breaking-changes-to-database-engine-features-in-includesssqlv14-mdincludessssqlv14-mdmd"></a>Alterações interruptivas em recursos do Mecanismo de Banco de Dados no [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


  Este tópico descreve as alterações interruptivas no [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)]. Essas alterações podem danificar aplicativos, scripts ou funcionalidades baseados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Talvez você tenha esses problemas ao atualizar.  
  
## <a name="breaking-changes-in-includesssqlv14-mdincludessssqlv14-mdmdincludessdeincludesssde-mdmd"></a>Alterações interruptivas do [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)]  
  
-  O CLR usa o CAS (Segurança de Acesso do Código) no .NET Framework, para o qual não há mais suporte como um limite de segurança. A partir do [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)], uma opção `sp_configure` chamada `clr strict security` é introduzida, a fim de aumentar a segurança de assemblies CLR. A opção clr strict security está habilitada por padrão e trata assemblies CLR `SAFE` e `EXTERNAL_ACCESS` como se eles fossem marcados como `UNSAFE`. A opção `clr strict security` pode ser desabilitada para compatibilidade com versões anteriores, mas isso não é recomendado. Quando a opção `clr strict security` estiver desabilitada, um assembly CLR criado com o `PERMISSION_SET = SAFE` pode conseguir acessar recursos externos do sistema, chamar um código não gerenciado e adquirir privilégios **sysadmin**. Depois de habilitar segurança estrita, os assemblies que não estão assinados não serão carregados. Além disso, se um banco de dados tiver assemblies `SAFE` ou `EXTERNAL_ACCESS`, as instruções `RESTORE` ou `ATTACH DATABASE` poderão ser concluídas, mas os assemblies poderão falhar ao serem carregados.   
  Para carregar os assemblies, você deve alterar ou remover e recriar cada assembly, de modo que ele seja assinado com um certificado ou uma chave assimétrica que tem um logon correspondente à permissão `UNSAFE ASSEMBLY` no servidor. Para obter mais informações, consulte [Segurança estrita do CLR](../database-engine/configure-windows/clr-strict-security.md). 


  
## <a name="previous-versions"></a>Versões anteriores  

-   [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)  
  
-   [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2014](breaking-changes-to-database-engine-features-in-sql-server-2016.md))  
  
-   [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2012](breaking-changes-to-database-engine-features-in-sql-server-2016.md))  
  
-   [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2008](breaking-changes-to-database-engine-features-in-sql-server-2016.md))  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do Mecanismo de Banco de Dados preteridos no SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Funcionalidade do Mecanismo de Banco de Dados descontinuada no SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Compatibilidade com versões anteriores do Mecanismo de Banco de Dados do SQL Server](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  
