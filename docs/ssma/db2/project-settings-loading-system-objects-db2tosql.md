---
title: Configurações (Carregando objetos de sistema) do projeto (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9a545233-1b0a-488a-a1ec-c33aa608dcc1
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3b2398732bc920b926a3db3352eacca6e39f7399
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "40395811"
---
# <a name="project-settingsloading-system-objects-db2tosql"></a>Configurações (Carregando objetos de sistema) do projeto (DB2ToSQL)
A página de carregamento de objetos do sistema do **configurações do projeto** caixa de diálogo permite que você especifique quais objetos de sistema do DB2 SSMA converte e carrega em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
O painel de carregamento de objetos do sistema está disponível na **configurações do projeto** e **configurações do projeto padrão** caixas de diálogo:  
  
-   Para especificar configurações para todos os projetos do SSMA, na **ferramentas** menu, selecione **configurações do projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibida ou alterada de **Versão de destino de migração** suspensa clique **gerais** na parte inferior do painel esquerdo e, em seguida, clique **Carregando objetos do sistema**.  
  
-   Para especificar configurações para o projeto atual, nos **ferramentas** menu, selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique em **Ao carregar objetos do sistema**.  
  
## <a name="default-settings"></a>Configurações padrão  
Converter objetos de sistema consome recursos do sistema e leva tempo. Para melhorar o desempenho, o SSMA seleciona somente os objetos do sistema usados com mais frequência, como mostrado na lista a seguir:  
  
-   SYS.DBMS_OUTPUT  
  
-   SYS.DBMS_PIPE  
  
-   SYS.DBMS_UTILITY  
  
-   SYS. STANDARD  
  
-   SYS. UTL_FILE  
  
-   SYS.DBMS_LOB  
  
-   SYS.DBMS_SQL  
  
-   SYS.DBMS_SESSION  
  
Se seus objetos de DB2 se referirem a objetos de sistema adicionais, você deve selecionar esses objetos. Se você não selecionar os objetos do sistema que são referenciados por seus objetos de banco de dados do DB2, o SSMA relatará erros de conversão. Se você receber erros de conversão causados por falta de objetos do sistema, selecione os objetos ausentes nessa caixa de diálogo. Em seguida, você pode repetir a conversão, conforme necessário.  
  
