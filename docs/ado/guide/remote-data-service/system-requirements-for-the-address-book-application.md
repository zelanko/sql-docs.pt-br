---
title: Requisitos do sistema para o endereço do catálogo de aplicativo | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: da385405-1c9a-478b-9bf6-fba70015324c
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7fcb6383a8104834975d7e5988276b5004648367
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="system-requirements-for-the-address-book-application"></a>Requisitos de sistema para o aplicativo de catálogo de endereços
Para configurar o aplicativo de exemplo do catálogo de endereços, é necessário atender aos seguintes requisitos de software e o banco de dados:  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="software-requirements"></a>Requisitos de software  
 Os requisitos de software de computador do servidor para executar este aplicativo da Web incluem:  
  
-   Microsoft Windows NT® Server 4.0, com Service Pack 3 ou posterior, ou Microsoft Windows® 2000 Server.  
  
-   Microsoft Internet Information Services (IIS) versão 3.0 ou posterior, com o Active Server Pages.  
  
 Os requisitos de software do computador cliente para executar este aplicativo da Web incluem:  
  
-   Microsoft Internet Explorer 4.0 ou posterior.  
  
-   Estação de trabalho do Microsoft Windows NT 4.0 ou o servidor, o Windows 2000 ou o Microsoft Windows 98.  
  
## <a name="database-requirements"></a>Requisitos do banco de dados  
 Para usar este exemplo, você deve ter:  
  
-   Um operacionais Microsoft® SQL Server versão 6.5 ou posterior servidor de banco de dados.  
  
-   Privilégios para criar o banco de dados e preenchê-lo com os dados de exemplo.  
  
-   Verificação dos dados preenchidas por meio do Enterprise Manager ou os utilitários ISQL (chamado analisador de consultas no SQL Server 7.0).  
  
 Se você não tiver privilégios, o administrador de banco de dados precisará configurar o sistema e conceder permissão de acesso para o banco de dados, ou configurar o banco de dados para você.  
  
## <a name="see-also"></a>Consulte também  
 [A execução do Script SQL do catálogo de endereço](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)   
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Executando o aplicativo de exemplo do catálogo de endereços](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


