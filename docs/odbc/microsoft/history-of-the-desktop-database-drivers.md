---
title: Histórico dos Drivers de banco de dados da área de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], history
- ODBC desktop database drivers [ODBC], history
- desktop database drivers [ODBC], history
ms.assetid: b4a2aff8-bde7-4bd5-8580-bc50f27311c8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a77aeafff6b27b2de0b947700cef1c7251cd7548
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127262"
---
# <a name="history-of-the-desktop-database-drivers"></a>Histórico de drivers de banco de dados de área de trabalho
A tabela a seguir mostra o histórico de versões de Drivers de banco de dados de área de trabalho.  
  
|Versão|Data de lançamento|Descrição|  
|-------------|------------------|-----------------|  
|1.0|Agosto de 1993|Usaram o processador de consulta do SIMBA produzido pela PageAhead Software. Com a SIMBA recebeu chamadas ODBC e instruções SQL, processada-los em chamadas ISAM instaláveis do Microsoft Jet e, em seguida, a chamada de camada de expedição de ISAM do Microsoft Jet para carregar e chamar o driver ISAM instalável apropriado.|  
|2.0|Dezembro de 1994|Usada com ODBC 2.0, que significativamente expandido de funcionalidade do ODBC. A principal alteração na versão 2.0 foi que o mecanismo de banco de dados Microsoft Jet substituído o processador de consultas com a SIMBA. Com o mecanismo de banco de dados Microsoft Jet, os Drivers de banco de dados de área de trabalho muito mais estreitamente integrado com os drivers ISAM instaláveis do Microsoft Jet e a tecnologia do Microsoft Access. Foram feitas melhorias significativas:<br /><br /> -Suporte nativo para cursores roláveis.<br />-Suporte nativo de junções externas, junções atualizáveis e heterogêneas e transações.<br />-as versões de 32 bits dos drivers para o Microsoft Windows NT.|  
|3.0|Outubro de 1995|É fornecido suporte para o Windows 95 e estação de trabalho do Windows NT ou NT 3.51 do servidor. Somente drivers de 32 bits foram incluídos nesta versão; os drivers de 16 bits para Windows versão 3.1 foram removidos.|  
|3.5|Outubro de 1996|Esses drivers foram o conjunto de caracteres de byte duplo (DBCS)-habilitado, foram mais adequados para uso com aplicativos da Internet que as versões anteriores e acomodada o uso de nomes de fonte de dados de arquivo (DSNs). O driver do Microsoft Access foi lançado em uma versão RISC para uso em plataformas de alfa para o Windows 95/98 e Windows NT 3.51 e sistemas operacionais posteriores.|  
|4.0|1998 tardia|Fornece suporte para o formato Unicode de mecanismo Jet Microsoft juntamente com a compatibilidade para o formato ANSI de versões anteriores.|  
  
> [!NOTE]  
>  Os drivers version3.5 foram projetados para trabalhar com ODBC2. *x*. Embora também funcionam com o ODBC 3.0, eles não têm suporte a todos os recursos de ODBC 3.0. Para obter mais informações sobre como esses drivers funcionam com o ODBC 3.0, consulte [compatibilidade com versões anteriores e em conformidade com padrões](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).
