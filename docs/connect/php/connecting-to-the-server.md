---
title: Conexão ao Servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c251a239-e0bd-4f45-9207-b76651072dd0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 789fec0bd9299f4d436c664306d380bb9a7da153
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015139"
---
# <a name="connecting-to-the-server"></a>Conectando-se ao servidor
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Os tópicos nesta seção descrevem as opções e os procedimentos para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

Os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] podem se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a Autenticação do Windows ou do SQL Server. Por padrão, os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] tentam se conectar ao servidor usando a Autenticação do Windows.  

## <a name="in-this-section"></a>Nesta seção  

|Tópico|Descrição|  
|---------|---------------|  
|[Como: Conectar usando a Autenticação do Windows](../../connect/php/how-to-connect-using-windows-authentication.md)|Descreve como estabelecer uma conexão usando a Autenticação do Windows.|  
|[Como: Conectar usando a Autenticação do SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md)|Descreve como estabelecer uma conexão usando a Autenticação do SQL Server.|  
|[Como: Conectar usando a Autenticação do Azure Active Directory](../../connect/php/azure-active-directory.md)|Descreve como definir um modo de autenticação e conectar-se usando as identidades do Azure Active Directory.|  
|[Como: Conectar em uma porta especificada](../../connect/php/how-to-connect-on-a-specified-port.md)|Descreve como se conectar ao servidor usando uma porta específica.|  
|[Pool de conexão](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)|Fornece informações sobre o pool de conexões no driver.|  
|[Como: Desabilitar MARS (conjuntos de resultados ativos múltiplos)](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)|Descreve como desabilitar o recurso MARS ao fazer uma conexão.|  
|[Opções de conexão](../../connect/php/connection-options.md)|Lista as opções permitidas na matriz associativa que contém atributos de conexão.|  
|[Suporte ao LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)|Descreve o suporte dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] para o recurso LocalDB, adicionado no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].|  
|[Suporte a alta disponibilidade e recuperação de desastres](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)|Aborda como seu aplicativo pode ser configurado para aproveitar os recursos de alta disponibilidade e de recuperação de desastre adicionados no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].|  
|[Conectando-se ao Banco de Dados SQL do Microsoft Azure](../../connect/php/connecting-to-microsoft-azure-sql-database.md)|Discute como se conectar a um Banco de Dados SQL do Azure.|  
|[Resiliência de conexão](../../connect/php/connection-resiliency.md)|Discute o recurso de resiliência de conexão que restabelece conexões desfeitas.|  

## <a name="see-also"></a>Consulte Também  
[Guia de programação do Microsoft Drivers para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Aplicativo de exemplo &#40;driver SQLSRV&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
