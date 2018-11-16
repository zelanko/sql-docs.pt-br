---
title: Requisitos do sistema para o endereço do aplicativo de livro | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: da385405-1c9a-478b-9bf6-fba70015324c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10a7097292562acd60e8b83af9a48bd61aeb8557
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558053"
---
# <a name="system-requirements-for-the-address-book-application"></a>Requisitos de sistema para o aplicativo de catálogo de endereços
Para configurar o aplicativo de exemplo do catálogo de endereços, você precisa cumprir os seguintes requisitos de software e banco de dados:  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="software-requirements"></a>Requisitos de software  
 Os requisitos de software de computador do servidor para executar este aplicativo Web incluem:  
  
-   Microsoft Windows NT® Server 4.0 com Service Pack 3 ou posterior, ou Microsoft Windows® 2000 Server.  
  
-   Microsoft Internet Information Services (IIS) versão 3.0 ou posterior, com Active Server Pages.  
  
 Os requisitos de software do computador cliente para executar este aplicativo Web incluem:  
  
-   Microsoft Internet Explorer 4.0 ou posterior.  
  
-   Estação de trabalho do Microsoft Windows NT 4.0 Server, Windows 2000 ou Microsoft Windows 98.  
  
## <a name="database-requirements"></a>Requisitos do banco de dados  
 Para usar este exemplo, você deve ter:  
  
-   Servidor um operacional Microsoft® SQL Server versão 6.5 ou posterior para banco de dados.  
  
-   Privilégios para criar o banco de dados e preenchê-lo com os dados de exemplo.  
  
-   Verificação dos dados preenchidos por meio do Enterprise Manager ou os utilitários ISQL (Analisador de consultas chamado no SQL Server 7.0).  
  
 Se você não tiver privilégios, o administrador de banco de dados talvez precise configurar o sistema e dê permissão de acesso para o banco de dados, ou configurar o banco de dados para você.  
  
## <a name="see-also"></a>Consulte também  
 [A execução do Script SQL do catálogo de endereço](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)   
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Executando o aplicativo de exemplo do catálogo de endereços](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


