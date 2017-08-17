---
title: "Alterações interruptivas em recursos do Mecanismo de Banco de Dados no SQL Server 2017 | Microsoft Docs"
description: "Alterações interruptivas em recursos do Mecanismo de Banco de Dados no SQL Server 2017"
ms.date: 04/19/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- breaking changes 2017 [SQL Server]
ms.assetid: 
caps.latest.revision: 1
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b1599f34a61548b87f06b4b92c7a9307620cf89e
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="breaking-changes-to-database-engine-features-in-includesssqlv14-mdincludessssqlv14-mdmd"></a>Alterações interruptivas em recursos do Mecanismo de Banco de Dados no [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]   


  Este tópico descreve as alterações interruptivas no [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)]. Essas alterações podem danificar aplicativos, scripts ou funcionalidades baseados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Talvez você tenha esses problemas ao atualizar.  
  
## <a name="breaking-changes-in-includesssqlv14-mdincludessssqlv14-mdmdincludessdeincludesssde-mdmd"></a>Alterações interruptivas do [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)]  
  
-  O CLR usa o CAS (Segurança de Acesso do Código) no .NET Framework, para o qual não há mais suporte como um limite de segurança. A partir do [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)], uma opção `sp_configure` chamada `clr strict security` é introduzida, a fim de aumentar a segurança de assemblies CLR. A opção clr strict security está habilitada por padrão e trata assemblies CLR `SAFE` e `EXTERNAL_ACCESS` como se eles fossem marcados como `UNSAFE`. A opção `clr strict security` pode ser desabilitada para compatibilidade com versões anteriores, mas isso não é recomendado. Quando a opção `clr strict security` estiver desabilitada, um assembly CLR criado com o `PERMISSION_SET = SAFE` pode conseguir acessar recursos externos do sistema, chamar um código não gerenciado e adquirir privilégios **sysadmin**. Depois de habilitar segurança estrita, os assemblies que não estão assinados não serão carregados. Além disso, se um banco de dados tiver assemblies `SAFE` ou `EXTERNAL_ACCESS`, as instruções `RESTORE` ou `ATTACH DATABASE` poderão ser concluídas, mas os assemblies poderão falhar ao serem carregados.   
  Para carregar os assemblies, você deve alterar ou remover e recriar cada assembly, de modo que ele seja assinado com um certificado ou uma chave assimétrica que tem um logon correspondente à permissão `UNSAFE ASSEMBLY` no servidor. Para obter mais informações, consulte [Segurança estrita do CLR](../database-engine/configure-windows/clr-strict-security.md). 


  
## <a name="previous-versions"></a>Versões anteriores  

-   [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)  
  
-   [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2014](https://msdn.microsoft.com/library/ms143179\(v=sql.120\))  
  
-   [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2012](https://msdn.microsoft.com/library/ms143179\(v=sql.110\))  
  
-   [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2008](https://msdn.microsoft.com/library/ms143179\(v=sql.100\))  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do Mecanismo de Banco de Dados preteridos no SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Funcionalidade do Mecanismo de Banco de Dados descontinuada no SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Compatibilidade com versões anteriores do Mecanismo de Banco de Dados do SQL Server](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  

