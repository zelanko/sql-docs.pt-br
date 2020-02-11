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
ms.openlocfilehash: 8fc15968501fed6b94a7ccddb984cbdf76bcbcb0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915800"
---
# <a name="odbc-driver-for-oracle"></a>Driver ODBC para Oracle
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O Microsoft® ODBC driver for Oracle permite que você conecte seu aplicativo em conformidade com ODBC a um banco de dados Oracle. O ODBC driver for Oracle está em conformidade com a especificação ODBC (Open Database Connectivity) descrita na *referência do programador de ODBC*. Ele permite o acesso a pacotes PL/SQL, integração XA/DTC e acesso Oracle de dentro do Serviços de Informações da Internet (IIS).  
  
 O Oracle RDBMS é um sistema de gerenciamento de banco de dados relacional multiusuário que é executado com vários sistemas operacionais de estação de trabalho e Minicomputer. Os computadores compatíveis com IBM que executam o Microsoft Windows podem se comunicar com servidores de banco de dados Oracle por meio de uma rede. As redes com suporte incluem o Microsoft LAN Manager, o NetWare, VINEs, o DECnet e qualquer rede que ofereça suporte a TCP/IP.  
  
 O ODBC driver for Oracle permite que um aplicativo acesse dados em um Oracle Database por meio da interface ODBC. O driver pode acessar bancos de dados do Oracle locais ou ele pode se comunicar com a rede por meio do SQL * net. O diagrama a seguir fornece detalhes sobre essa arquitetura de aplicativo e driver.  
  
 ![ODBC driver for Oracle app&#47;driver Architecture](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 O ODBC driver for Oracle está em conformidade com o nível de conformidade de API 1 e o núcleo de nível de conformidade do SQL. Ele também dá suporte a algumas funções no nível de conformidade da API 2 e na maior parte da gramática nos níveis central e de conformidade do SQL estendido. O driver é compatível com ODBC 2,5 e dá suporte a sistemas de 32 bits. O Oracle 7.3 x tem suporte total; Oracle8 tem suporte limitado. O ODBC driver for Oracle não oferece suporte a nenhum dos novos tipos de dados Oracle8-tipos de dados Unicode, BLOBs, CLOBs e assim por diante, nem dá suporte ao novo modelo de objeto relacional da Oracle. Para obter mais informações sobre os tipos de dados com suporte, consulte [tipos de dados com suporte](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) neste guia.  
  
 Para acessar os dados do Oracle, são necessários os seguintes componentes:  
  
-   O ODBC driver for Oracle  
  
-   Um banco de dados do Oracle RDBMS  
  
-   Software cliente Oracle  
  
 Além disso, para conexões remotas:  
  
-   Uma rede que conecta os computadores que executam o driver e o banco de dados. A rede deve dar suporte a conexões SQL * net.  
  
## <a name="component-documentation"></a>Documentação do componente  
 Este guia contém informações detalhadas sobre como configurar e configurar o Microsoft ODBC driver for Oracle e adicionar a funcionalidade programática. Ele também contém material de referência técnica.  
  
 Para obter informações sobre o comportamento específico do produto Oracle, consulte a documentação que acompanha o produto Oracle.  
  
 Para obter informações sobre como configurar ou configurar o Microsoft ODBC driver for Oracle usando o administrador de fonte de dados ODBC, consulte a documentação do [administrador de fonte de dados ODBC](../../odbc/admin/odbc-data-source-administrator.md) .  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Guia do usuário do Driver ODBC para Oracle](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [Referência do programador do driver ODBC para Oracle](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
