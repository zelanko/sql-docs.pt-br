---
title: Conectando-se ao servidor
description: Saiba mais sobre os diferentes métodos para se conectar ao banco de dados usando Drivers da Microsoft para PHP para SQL Server.
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c251a239-e0bd-4f45-9207-b76651072dd0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5a2ec027a72bd96b567b08639568b6ead8e5dc64
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87410972"
---
# <a name="connecting-to-the-server"></a>Conectando-se ao servidor
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Os tópicos nesta seção descrevem as opções e os procedimentos para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

Os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] podem se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a Autenticação do Windows ou do SQL Server. Por padrão, os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] tentam se conectar ao servidor usando a Autenticação do Windows.  

## <a name="in-this-section"></a>Nesta seção  

|Tópico|Descrição|  
|---------|---------------|  
|[Como fazer: Conectar usando a Autenticação do Windows](../../connect/php/how-to-connect-using-windows-authentication.md)|Descreve como estabelecer uma conexão usando a Autenticação do Windows.|  
|[Como: conectar usando a Autenticação do SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md)|Descreve como estabelecer uma conexão usando a Autenticação do SQL Server.|  
|[Como conectar-se usando a Autenticação do Azure Active Directory](../../connect/php/azure-active-directory.md)|Descreve como definir um modo de autenticação e conectar-se usando as identidades do Azure Active Directory.|  
|[Como se conectar a uma porta especificada](../../connect/php/how-to-connect-on-a-specified-port.md)|Descreve como se conectar ao servidor usando uma porta específica.|  
|[Pool de conexões](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)|Fornece informações sobre o pool de conexões no driver.|  
|[Como desabilitar vários conjuntos de resultados ativos (MARS)](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)|Descreve como desabilitar o recurso MARS ao fazer uma conexão.|  
|[Opções de conexão](../../connect/php/connection-options.md)|Lista as opções permitidas na matriz associativa que contém atributos de conexão.|  
|[Suporte ao LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)|Descreve o suporte dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] para o recurso LocalDB, adicionado no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].|  
|[Suporte a alta disponibilidade e recuperação de desastres](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)|Aborda como seu aplicativo pode ser configurado para aproveitar os recursos de alta disponibilidade e de recuperação de desastre adicionados no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].|  
|[Conectar-se ao Banco de Dados SQL do Microsoft Azure](../../connect/php/connecting-to-microsoft-azure-sql-database.md)|Discute como se conectar a um Banco de Dados SQL do Azure.|  
|[Resiliência de conexão](../../connect/php/connection-resiliency.md)|Discute o recurso de resiliência de conexão que restabelece conexões desfeitas.|  

## <a name="see-also"></a>Consulte Também  
[Guia de programação do Microsoft Drivers para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Aplicativo de exemplo &#40;driver SQLSRV&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
