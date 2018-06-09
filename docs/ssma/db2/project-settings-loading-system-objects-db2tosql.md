---
title: Configurações (objetos de sistema de carregamento) do projeto (DB2ToSQL) | Microsoft Docs
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
ms.openlocfilehash: a36764c5799b78c1de460e5c462d6c28c3d84806
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34775492"
---
# <a name="project-settingsloading-system-objects-db2tosql"></a>Configurações (objetos de sistema de carregamento) do projeto (DB2ToSQL)
A página carregar objetos do sistema do **configurações de projeto** caixa de diálogo permite que você especifique quais objetos de sistema DB2 SSMA converte e carrega em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
O painel ao carregar objetos do sistema está disponível na **configurações de projeto** e **configurações de projeto padrão** caixas de diálogo:  
  
-   Para especificar configurações para todos os projetos do SSMA, no **ferramentas** menu, selecione **configurações de projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibido ou alterado de **versão de destino de migração** suspensa clique **geral** na parte inferior do painel esquerdo e, em seguida, clique **carregar objetos do sistema**.  
  
-   Para especificar as configurações para o projeto atual, no **ferramentas** menu, selecione **configurações de projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique **carregar objetos do sistema**.  
  
## <a name="default-settings"></a>Configurações padrão  
Converter objetos de sistema consome recursos do sistema e leva tempo. Para melhorar o desempenho, o SSMA seleciona somente os objetos de sistema usados com mais frequência, conforme mostrado na lista a seguir:  
  
-   SYS.DBMS_OUTPUT  
  
-   SYS.DBMS_PIPE  
  
-   SYS.DBMS_UTILITY  
  
-   SYS. PADRÃO  
  
-   SYS. UTL_FILE  
  
-   SYS.DBMS_LOB  
  
-   SYS.DBMS_SQL  
  
-   SYS.DBMS_SESSION  
  
Se os objetos do DB2 se referem a objetos de sistema adicionais, você deve selecionar os objetos. Se você não selecionar os objetos do sistema que são referenciados por seus objetos de banco de dados do DB2, o SSMA relatará erros de conversão. Se você receber erros de conversão causados pela falta de objetos do sistema, selecione os objetos ausentes na caixa de diálogo. Você pode repetir a conversão conforme necessário.  
  
