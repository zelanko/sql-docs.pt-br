---
title: Driver ODBC para Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], about ODBC driver for Oracle
- Oracle data access [ODBC]
ms.assetid: 937e0662-8b1d-44f7-b077-4015c6605b2c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4685d209d768bd3ff41c1c7367ef6cb6dcd45bcf
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52515098"
---
# <a name="odbc-driver-for-oracle"></a>Driver ODBC para Oracle
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O Microsoft® ODBC Driver for Oracle permite que você conecte seu aplicativo compatível com ODBC para um banco de dados Oracle. O Driver ODBC para Oracle está de acordo com a especificação de conectividade de banco de dados aberto (ODBC) descrita o *referência do programador de ODBC*. Ele permite o acesso a pacotes de PL/SQL, integração de XA/DTC e acesso do Oracle de dentro do Internet Information Services (IIS).  
  
 Oracle RDBMS é um sistema de gerenciamento de vários usuários de banco de dados relacional que é executado com vários sistemas operacionais da estação de trabalho e minicomputador. Computadores compatíveis com o IBM executando o Microsoft Windows podem se comunicar com servidores de banco de dados Oracle em uma rede. Redes com suporte incluem Microsoft LAN Manager, NetWare, VINES, DECnet e qualquer rede que dá suporte a TCP/IP.  
  
 O Driver ODBC para Oracle permite que um aplicativo acessar dados em um banco de dados Oracle por meio da interface do ODBC. O driver pode acessar bancos de dados Oracle locais, ou ele pode se comunicar com a rede por meio do SQL * Net. O diagrama a seguir fornece detalhes sobre essa arquitetura de aplicativo e o driver.  
  
 ![O Driver ODBC para Oracle aplicativo&#47;arquitetura do driver](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 O Driver ODBC para Oracle é compatível com a API de conformidade de nível 1 e núcleo de nível de conformidade do SQL. Ele também dá suporte a algumas funções em nível de conformidade com a API 2 e a maioria da gramática nos níveis de conformidade Core e SQL estendida. O driver é compatível com o ODBC 2.5 e dá suporte a sistemas de 32 bits. Oracle 7.3 x tem suporte totalmente; Oracle8 tem suporte limitado. O Driver ODBC para Oracle não oferece suporte a qualquer um dos novos tipos de dados Oracle8 - tipos de dados Unicode, BLOBs, CLOBs e assim por diante – nem oferece suporte a novo modelo de objeto relacional da Oracle. Para obter mais informações sobre os tipos de dados com suporte, consulte [suporte para tipos de dados](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) neste guia.  
  
 Para acessar dados da Oracle, são necessários os seguintes componentes:  
  
-   O Driver ODBC para Oracle  
  
-   Um banco de dados Oracle RDBMS  
  
-   Software cliente Oracle  
  
 Além disso, para conexões remotas:  
  
-   Uma rede que conecta os computadores que executam o driver e o banco de dados. A rede deve oferecer suporte a SQL * Net conexões.  
  
## <a name="component-documentation"></a>Documentação do componente  
 Este guia contém informações detalhadas sobre como configurar e configurar o Microsoft ODBC Driver para Oracle e adicionando a funcionalidade de programação. Ele também contém o material de referência.  
  
 Para obter informações sobre o comportamento de produto específico do Oracle, consulte a documentação que acompanha o produto Oracle.  
  
 Para obter informações sobre como definir ou configurar o Microsoft ODBC Driver for Oracle usando o administrador de fonte de dados ODBC, consulte a [administrador de fonte de dados ODBC](../../odbc/admin/odbc-data-source-administrator.md) documentação.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Guia do usuário do Driver ODBC para Oracle](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [Referência do programador do driver ODBC para Oracle](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
