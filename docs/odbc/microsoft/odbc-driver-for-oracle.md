---
title: O Driver ODBC para Oracle | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], about ODBC driver for Oracle
- Oracle data access [ODBC]
ms.assetid: 937e0662-8b1d-44f7-b077-4015c6605b2c
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 70ae9b447f0f3bcc6e70060b2f46f994ef3ea773
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="odbc-driver-for-oracle"></a>Driver ODBC para Oracle
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O Microsoft® ODBC Driver for Oracle permite conectar seu aplicativo compatível com ODBC para um banco de dados Oracle. O Driver ODBC do Oracle está de acordo com a especificação de conectividade de banco de dados aberto (ODBC) descrita o *referência do programador de ODBC*. Ele permite acesso aos pacotes de PL/SQL, integração XA/DTC e Oracle acesso dentro dos serviços de informações da Internet (IIS).  
  
 Oracle RDBMS é um sistema de gerenciamento de vários usuários de banco de dados relacional que é executado com vários sistemas operacionais de estação de trabalho e minicomputador. IBM compatível com computadores que executam o Microsoft Windows podem se comunicar com servidores de banco de dados Oracle em uma rede. Redes com suporte incluem Microsoft LAN Manager, NetWare, VINES, DECnet e qualquer rede que oferece suporte a TCP/IP.  
  
 O Driver ODBC do Oracle permite que um aplicativo acessar dados em um banco de dados Oracle por meio da interface do ODBC. O driver pode acessar bancos de dados Oracle locais ou pode se comunicar com a rede por meio do SQL * Net. O diagrama a seguir fornece detalhes sobre essa arquitetura de aplicativo e o driver.  
  
 ![O Driver ODBC para Oracle aplicativo &#47; a arquitetura do driver](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 O Driver ODBC do Oracle é compatível com a API conformidade nível 1 e o núcleo de nível de conformidade do SQL. Também oferece suporte a algumas funções na API de conformidade de nível 2 e a maioria da gramática nos níveis de conformidade de núcleo e estendida do SQL. O driver é compatível com o ODBC 2.5 e dá suporte a sistemas de 32 bits. Oracle 7.3 x pode ser totalmente; Oracle8 tem suporte limitado. O Driver ODBC do Oracle não dá suporte a qualquer um dos novos tipos de dados do Oracle8 — tipos de dados Unicode, BLOBs, CLOBs, e assim por diante, nem ela dá suporte ao novo modelo de objeto relacional da Oracle. Para obter mais informações sobre tipos de dados com suporte, consulte [suporte para tipos de dados](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) neste guia.  
  
 Para acessar dados do Oracle, são necessários os seguintes componentes:  
  
-   O Driver ODBC do Oracle  
  
-   Um banco de dados Oracle RDBMS  
  
-   Software cliente Oracle  
  
 Além disso, para conexões remotas:  
  
-   Uma rede que conecta os computadores que executam o driver e o banco de dados. A rede deve oferecer suporte ao SQL * Net conexões.  
  
## <a name="component-documentation"></a>Documentação do componente  
 Este guia contém informações detalhadas sobre como definir e configurar o Microsoft ODBC Driver for Oracle e adicionando a funcionalidade de programação. Ele também contém o material de referência técnica.  
  
 Para obter informações sobre o comportamento de produto específico do Oracle, consulte a documentação que acompanha o produto Oracle.  
  
 Para obter informações sobre como definir ou configurar o Microsoft ODBC Driver for Oracle usando o administrador de fonte de dados ODBC, consulte o [administrador de fonte de dados ODBC](../../odbc/admin/odbc-data-source-administrator.md) documentação.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Guia do usuário do Driver ODBC para Oracle](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [Referência do programador do driver ODBC para Oracle](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
