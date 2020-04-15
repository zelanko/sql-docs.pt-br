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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 093cb7352a7f509b0afcc061e2691311bb183169
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298126"
---
# <a name="odbc-driver-for-oracle"></a>Driver ODBC para Oracle
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O Driver ODBC ® Microsoft para Oracle permite conectar seu aplicativo compatível com ODBC a um banco de dados Oracle. O Driver ODBC for Oracle está em conformidade com a especificação De conectividade de banco de dados aberto (ODBC) descrita na *referência do programador ODBC*. Ele permite acesso a pacotes PL/SQL, integração XA/DTC e acesso Oracle a partir de Serviços de Informação da Internet (IIS).  
  
 Oracle RDBMS é um sistema de gerenciamento de banco de dados relacional multiusuário que funciona com vários sistemas operacionais de estação de trabalho e minicomputadores. Computadores compatíveis com a IBM que executam o Microsoft Windows podem se comunicar com servidores de banco de dados Oracle através de uma rede. As redes suportadas incluem o Microsoft LAN Manager, NetWare, VINES, DECnet e qualquer rede que suporte TCP/IP.  
  
 O Driver ODBC para Oracle permite que um aplicativo acesse dados em um banco de dados Oracle através da interface ODBC. O driver pode acessar bancos de dados Oracle locais ou pode se comunicar com a rede através do SQL*Net. O diagrama a seguir detalha esta arquitetura de aplicativo e driver.  
  
 ![ODBC Driver for Oracle app&#47;arquitetura de driver](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 O Driver ODBC para Oracle está em conformidade com o API Conformance Level 1 e o SQL Conformance Level Core. Ele também suporta algumas funções no API Conformância Nível 2 e a maior parte da gramática nos níveis de conformidade SQL núcleo e estendido. O driver é compatível com ODBC 2.5 e suporta sistemas de 32 bits. O Oracle 7.3x é suportado totalmente; A Oracle8 tem suporte limitado. O Driver ODBC para Oracle não suporta nenhum dos novos tipos de dados Oracle8 - tipos de dados Unicode, BLOBs, CLOBs e assim por diante - nem suporta o novo Modelo de Objeto Relacional da Oracle. Para obter mais informações sobre os tipos de dados suportados, consulte [Tipos de dados suportados](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) neste guia.  
  
 Para acessar os dados oracle, são necessários os seguintes componentes:  
  
-   O Driver ODBC para Oracle  
  
-   Um banco de dados Oracle RDBMS  
  
-   Oracle Client Software  
  
 Além disso, para conexões remotas:  
  
-   Uma rede que conecta os computadores que executam o driver e o banco de dados. A rede deve suportar conexões SQL*Net.  
  
## <a name="component-documentation"></a>Documentação de componentes  
 Este guia contém informações detalhadas sobre como configurar e configurar o Driver ODBC do Microsoft para Oracle e adicionar funcionalidade programática. Também contém material de referência técnica.  
  
 Para obter informações sobre o comportamento específico do produto Oracle, consulte a documentação que acompanha o produto Oracle.  
  
 Para obter informações sobre como configurar ou configurar o Microsoft ODBC Driver for Oracle usando o Administrador de Origem de Dados do ODBC, consulte a documentação do Administrador de Origem de Dados do [ODBC.](../../odbc/admin/odbc-data-source-administrator.md)  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Guia do usuário do Driver ODBC para Oracle](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [Referência do programador do driver ODBC para Oracle](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
