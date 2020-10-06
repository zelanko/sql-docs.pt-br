---
title: 'Mecanismo de Banco de Dados: Alterações mais recentes | Microsoft Docs'
titleSuffix: SQL Server 2017
description: Saiba mais sobre as alterações que podem interromper aplicativos, scripts ou recursos baseados em versões anteriores do SQL Server.
ms.custom: seo-lt-2019
ms.date: 07/22/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- breaking changes 2017 [SQL Server]
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 18a129e630028d0384f10a373a2302ff57bd78cb
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670153"
---
# <a name="breaking-changes-to-database-engine-features-in-sssqlv14-md"></a>Alterações interruptivas em recursos do Mecanismo de Banco de Dados no [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]
[!INCLUDE[SQL Server 2017](../includes/applies-to-version/sqlserver2017.md)]


  Este tópico descreve as alterações interruptivas no [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]. Essas alterações podem danificar aplicativos, scripts ou funcionalidades baseados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Talvez você tenha esses problemas ao atualizar.  
  
## <a name="breaking-changes-in-sssqlv14-md-ssde"></a>Últimas alterações do [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]  
  
-  O CLR usa o CAS (Segurança de Acesso do Código) no .NET Framework, para o qual não há mais suporte como um limite de segurança. A partir do [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)], uma opção `sp_configure` chamada `clr strict security` é introduzida, a fim de aumentar a segurança de assemblies CLR. A opção clr strict security está habilitada por padrão e trata assemblies CLR `SAFE` e `EXTERNAL_ACCESS` como se eles fossem marcados como `UNSAFE`. A opção `clr strict security` pode ser desabilitada para compatibilidade com versões anteriores, mas isso não é recomendado. Quando a opção `clr strict security` estiver desabilitada, um assembly CLR criado com o `PERMISSION_SET = SAFE` pode conseguir acessar recursos externos do sistema, chamar um código não gerenciado e adquirir privilégios **sysadmin**. Depois de habilitar segurança estrita, os assemblies que não estão assinados não serão carregados. Além disso, se um banco de dados tiver assemblies `SAFE` ou `EXTERNAL_ACCESS`, as instruções `RESTORE` ou `ATTACH DATABASE` poderão ser concluídas, mas os assemblies poderão falhar ao serem carregados.   
  Para carregar os assemblies, você deve alterar ou remover e recriar cada assembly, de modo que ele seja assinado com um certificado ou uma chave assimétrica que tem um logon correspondente à permissão `UNSAFE ASSEMBLY` no servidor. Para obter mais informações, consulte [Segurança estrita do CLR](../database-engine/configure-windows/clr-strict-security.md). 
  
-  Os algoritmos MD2, MD4, MD5, SHA e SHA1 foram preteridos no [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]. Até o [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], um certificado autoassinado é criado usando SHA1. Do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] em diante, um certificado autoassinado é criado usando SHA2_256.

## <a name="previous-versions"></a><a name="previous-versions"></a> Versões anteriores  

- [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)

- [Alterações recentes em recursos do Mecanismo de Banco de Dados no SQL Server 2014](/previous-versions/sql/2014/database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016?view=sql-server-2014#SQL14)

#### <a name="archived-documentation-for-very-old-versions-of-sql-server"></a>Documentação arquivada de versões muito antigas do SQL Server

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>Consulte Também  
 [Recursos do Mecanismo de Banco de Dados preteridos no SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Funcionalidade do Mecanismo de Banco de Dados descontinuada no SQL Server 2016](./discontinued-database-engine-functionality-in-sql-server.md)   
 [Compatibilidade com versões anteriores do Mecanismo de Banco de Dados do SQL Server](./discontinued-database-engine-functionality-in-sql-server.md)   
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
