---
title: Histórico dos drivers de banco de dados de desktop | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304977"
---
# <a name="history-of-the-desktop-database-drivers"></a>Histórico de drivers de banco de dados de área de trabalho
A tabela a seguir mostra o histórico da versão do Desktop Database Drivers.  
  
|Versão|Data de lançamento|Descrição|  
|-------------|------------------|-----------------|  
|1.0|agosto de 1993|Usei o processador de consulta SIMBA produzido pelo PageAhead Software. O SIMBA recebeu chamadas oDBC e instruções SQL, processou-as em chamadas ISAM instaláveis do Microsoft Jet e, em seguida, chamou a camada de despacho ISAM do Microsoft Jet para carregar e chamar o driver ISAM instalável apropriado.|  
|2,0|dezembro de 1994|Usado com ODBC 2.0, que expandiu significativamente a funcionalidade do ODBC. A principal mudança na versão 2.0 foi que o mecanismo de banco de dados Microsoft Jet substituiu o processador de consulta SIMBA. Com o mecanismo de banco de dados Microsoft Jet, os Drivers de banco de dados de desktop integraram-se muito mais fortemente com os drivers ISAM instalados pelo Microsoft Jet e a tecnologia Microsoft Access. Melhorias significativas foram:<br /><br /> - Suporte nativo para cursores roláveis.<br />- Suporte nativo para adesões externas, adesões updatable e heterogêneas, e transações.<br />- Versões de 32 bits dos drivers para Microsoft Windows NT.|  
|3.0|outubro de 1995|Forneceu suporte para Windows 95 e Windows NT Workstation ou NT Server 3.51. Apenas drivers de 32 bits foram incluídos nesta versão; os drivers de 16 bits para windows versão 3.1 foram removidos.|  
|3,5|outubro de 1996|Esses drivers eram habilitados para dbcs (double-bytes), eram mais adequados para uso com aplicativos de Internet do que as versões anteriores e acomodavam o uso de dSNs (File data source name). O driver Microsoft Access foi lançado em uma versão RISC para uso nas plataformas Alpha para Windows 95/98 e Windows NT 3.51 e posteriormente sistemas operacionais.|  
|4,0|Final de 1998|Fornece suporte para o formato Microsoft Jet Engine Unicode, juntamente com a compatibilidade para o formato ANSI de versões anteriores.|  
  
> [!NOTE]  
>  Os drivers version3.5 foram projetados para funcionar com ODBC2. *x*. Embora também trabalhem com o ODBC 3.0, eles não suportam todos os recursos do ODBC 3.0. Para obter mais informações sobre como esses drivers trabalham com o ODBC 3.0, consulte [Retrocompatibilidade e Conformidade de Padrões](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).
