---
description: Requisitos de sistema para o aplicativo de catálogo de endereços
title: Requisitos do sistema para o aplicativo de catálogo de endereços | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: da385405-1c9a-478b-9bf6-fba70015324c
author: rothja
ms.author: jroth
ms.openlocfilehash: 2e8555a61639ed7019c9972debe916f9f1a64934
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977457"
---
# <a name="system-requirements-for-the-address-book-application"></a>Requisitos de sistema para o aplicativo de catálogo de endereços
Para configurar o aplicativo de exemplo do catálogo de endereços, você precisa atender aos seguintes requisitos de software e banco de dados:  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="software-requirements"></a>Requisitos de software  
 Os requisitos de software do computador servidor para executar esse aplicativo Web incluem:  
  
-   Microsoft Windows NT® Server 4,0, com Service Pack 3 ou posterior, ou Microsoft Windows® 2000 Server.  
  
-   Microsoft Serviços de Informações da Internet (IIS) versão 3,0 ou posterior, com Active Server páginas.  
  
 Os requisitos de software do computador cliente para executar esse aplicativo Web incluem:  
  
-   Microsoft Internet Explorer 4,0 ou posterior.  
  
-   Microsoft Windows NT 4,0 Workstation ou Server, Windows 2000 ou Microsoft Windows 98.  
  
## <a name="database-requirements"></a>Requisitos do banco de dados  
 Para usar este exemplo, você deve ter:  
  
-   Um servidor de banco de dados do Microsoft® operacional SQL Server versão 6,5 ou posterior.  
  
-   Privilégios para criar o banco de dados e preenchê-lo com os exemplos de dado.  
  
-   Verificação dos dados populados por meio do Enterprise Manager ou dos utilitários ISQL (chamado de analisador de consultas no SQL Server 7,0).  
  
 Se você não tiver privilégios, o administrador do banco de dados poderá precisar configurar o sistema e conceder a você permissão de acesso ao banco de dados ou configurar o banco de dados para você.  
  
## <a name="see-also"></a>Consulte Também  
 [Executando o script SQL do catálogo de endereços](./running-the-address-book-sql-script.md)   
 [Objeto DataControl (RDS)](../../reference/rds-api/datacontrol-object-rds.md)   
 [Executar o aplicativo de exemplo do catálogo de endereços](./running-the-address-book-sample-application.md)