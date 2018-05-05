---
title: O histórico dos Drivers de banco de dados de área de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], history
- ODBC desktop database drivers [ODBC], history
- desktop database drivers [ODBC], history
ms.assetid: b4a2aff8-bde7-4bd5-8580-bc50f27311c8
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 703a7470372d9e823ae9c76e0425eb3e859fbfe6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="history-of-the-desktop-database-drivers"></a>Histórico dos Drivers de banco de dados de área de trabalho
A tabela a seguir mostra o histórico de versões de Drivers de banco de dados de área de trabalho.  
  
|Versão|Data de lançamento|Description|  
|-------------|------------------|-----------------|  
|1.0|Agosto de 1993|Usaram o processador de consulta SIMBA produzido pela PageAhead Software. SIMBA recebeu chamadas ODBC e instruções SQL, processados-los em chamadas ISAM instaláveis do Microsoft Jet e, em seguida, a chamada de camada de expedição de ISAM do Microsoft Jet para carregar e chamar o driver ISAM instalável apropriado.|  
|2.0|Dezembro de 1994|Usada com ODBC 2.0, que expandido significativamente a funcionalidade do ODBC. A principal alteração na versão 2.0 foi que o mecanismo de banco de dados Microsoft Jet substituído o processador de consultas SIMBA. Com o mecanismo de banco de dados Microsoft Jet, os Drivers de banco de dados de área de trabalho muito mais estreitamente integrados com os drivers ISAM instaláveis do Microsoft Jet e a tecnologia do Microsoft Access. Aprimoramentos significativos foram:<br /><br /> -Suporte nativo para cursores roláveis.<br />-Suporte nativo de junções externas, junções heterogêneas e atualizáveis e transações.<br />-as versões de 32 bits dos drivers para o Microsoft Windows NT.|  
|3.0|Outubro de 1995|É fornecido suporte para o Windows 95 e Windows NT Workstation ou Server do NT 3.51. Somente drivers de 32 bits foram incluídos nesta versão; os drivers de 16 bits para o Windows versão 3.1 foram removidos.|  
|3.5|Outubro de 1996|Esses drivers foram conjunto de caracteres de dois bytes (DBCS)-habilitado, foram mais adequados para uso com aplicativos da Internet que as versões anteriores e acomodada o uso de nomes de fonte de dados (DSNs) de arquivo. O driver do Microsoft Access foi lançado em uma versão RISC para uso em plataformas de alfa para o Windows 95/98 e Windows NT 3.51 e sistemas operacionais posteriores.|  
|4.0|1998 tardia|Fornece suporte para o formato Unicode de mecanismo Jet Microsoft juntamente com a compatibilidade para o formato ANSI de versões anteriores.|  
  
> [!NOTE]  
>  Os drivers version3.5 foram projetados para trabalhar com ODBC2. *x*. Embora elas também funcionam com ODBC 3.0, eles não dão suporte a todos os recursos de ODBC 3.0. Para obter mais informações sobre como esses drivers funcionam com ODBC 3.0, consulte [compatibilidade com versões anteriores e a conformidade com padrões](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).
