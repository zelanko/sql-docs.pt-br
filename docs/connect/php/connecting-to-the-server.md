---
title: Conectando ao servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c251a239-e0bd-4f45-9207-b76651072dd0
caps.latest.revision: 44
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03f3e44683ab329e67360be3992fb942c3799165
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35307805"
---
# <a name="connecting-to-the-server"></a>Conectando-se ao servidor
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Os tópicos nesta seção descrevem as opções e os procedimentos para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usando os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

Os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] podem se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usando a Autenticação do Windows ou do SQL Server. Por padrão, os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] tentam se conectar ao servidor usando a Autenticação do Windows.  

## <a name="in-this-section"></a>Nesta seção  

|Tópico|Description|  
|---------|---------------|  
|[Como se conectar usando a Autenticação do Windows](../../connect/php/how-to-connect-using-windows-authentication.md)|Descreve como estabelecer uma conexão usando a Autenticação do Windows.|  
|[Como se conectar usando a Autenticação do SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md)|Descreve como estabelecer uma conexão usando a Autenticação do SQL Server.|  
|[Como se conectar usando a Autenticação do Azure Active Directory](../../connect/php/azure-active-directory.md)|Descreve como definir o modo de autenticação e conecte-se usando identidades do Active Directory do Azure.|  
|[Como se conectar a uma porta especificada](../../connect/php/how-to-connect-on-a-specified-port.md)|Descreve como se conectar ao servidor usando uma porta específica.|  
|[Pool de conexões](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)|Fornece informações sobre o pool de conexões no driver.|  
|[Como desabilitar vários conjuntos de resultados ativos (MARS)](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)|Descreve como desabilitar o recurso MARS ao fazer uma conexão.|  
|[Opções de conexão](../../connect/php/connection-options.md)|Lista as opções permitidas na matriz associativa que contém atributos de conexão.|  
|[Suporte ao LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)|Descreve o suporte dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] para o recurso LocalDB, adicionado no [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)].|  
|[Suporte a alta disponibilidade e recuperação de desastres](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)|Discute como seu aplicativo pode ser configurado para aproveitar a recuperação de desastres de alta disponibilidade, recursos adicionados [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)].|  
|[Conectando-se ao Banco de Dados SQL do Microsoft Azure](../../connect/php/connecting-to-microsoft-azure-sql-database.md)|Descreve como se conectar a um banco de dados do SQL Azure.|  
|[Resiliência da conexão](../../connect/php/connection-resiliency.md)|Discute o recurso de resiliência de conexão que restabelece as conexões interrompidas.|  

## <a name="see-also"></a>Consulte também  
[Programação de guia para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Aplicativo de exemplo &#40;driver SQLSRV&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
