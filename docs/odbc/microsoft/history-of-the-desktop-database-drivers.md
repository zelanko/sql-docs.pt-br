---
title: Histórico dos drivers do banco de dados de desktop | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89434b397c07fdee751ca4272b65ac2eada94cf3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304977"
---
# <a name="history-of-the-desktop-database-drivers"></a>Histórico de drivers de banco de dados de área de trabalho
A tabela a seguir mostra o histórico de versão dos drivers do banco de dados de desktop.  
  
|Versão|Data de lançamento|Descrição|  
|-------------|------------------|-----------------|  
|1.0|Agosto de 1993|Usou o processador de consulta SIMBA produzido pelo software PageAhead. SIMBA recebeu chamadas de ODBC e instruções SQL, as processou em chamadas ISAM instaláveis do Microsoft Jet e, em seguida, chamou a camada de expedição ISAM do Microsoft Jet para carregar e chamar o driver ISAM instalável apropriado.|  
|2,0|Dezembro de 1994|Usado com o ODBC 2,0, que expandiu significativamente a funcionalidade do ODBC. A principal alteração na versão 2,0 era que o mecanismo de banco de dados do Microsoft Jet substituiu o processador de consultas SIMBA. Com o mecanismo de banco de dados do Microsoft Jet, os drivers de banco de dados de desktop integrados de forma muito mais rígida com os drivers ISAM instaláveis do Microsoft Jet e a tecnologia Microsoft Access. Melhorias significativas foram:<br /><br /> -Suporte nativo para cursores roláveis.<br />-Suporte nativo para junções externas, junções atualizáveis e heterogêneas e transações.<br />-versões de 32 bits dos drivers para o Microsoft Windows NT.|  
|3.0|Outubro de 1995|Fornecido suporte para Windows 95 e Windows NT Workstation ou NT Server 3,51. Somente drivers de 32 bits foram incluídos nesta versão; os drivers de 16 bits para o Windows versão 3,1 foram removidos.|  
|3,5|Outubro de 1996|Esses drivers eram habilitados para DBCS (conjunto de caracteres de dois bytes), foram mais adequados para uso com aplicativos de Internet do que para versões anteriores e acomodavam o uso de DSNs (nomes de fontes de dados de arquivo). O driver do Microsoft Access foi lançado em uma versão de RISC para uso em plataformas alfa para Windows 95/98 e Windows NT 3,51 e sistemas operacionais posteriores.|  
|4,0|Atrasado em 1998|Fornece suporte para o formato Unicode do mecanismo do Microsoft Jet juntamente com a compatibilidade para o formato ANSI de versões anteriores.|  
  
> [!NOTE]  
>  Os drivers da versão 3.5 foram projetados para funcionar com o ODBC2. *x*. Embora eles também funcionem com o ODBC 3,0, eles não oferecem suporte a todos os recursos ODBC 3,0. Para obter mais informações sobre como esses drivers funcionam com o ODBC 3,0, consulte [compatibilidade com versões anteriores e conformidade com padrões](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).
