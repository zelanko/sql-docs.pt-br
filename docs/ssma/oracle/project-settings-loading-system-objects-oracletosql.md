---
title: Configurações (Carregando objetos de sistema) do projeto (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9418cb34-d869-4d24-95b3-6cb9db949bb0
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: a5e8feb6c083c787d877cbc5491c533b8a35d740
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266607"
---
# <a name="project-settingsloading-system-objects-oracletosql"></a>Configurações do projeto (carregar objetos de sistema) (OracleToSQL)
A página de carregamento de objetos do sistema do **configurações do projeto** caixa de diálogo permite que você especifique quais objetos de sistema Oracle SSMA converte e carrega em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
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
  
Se seus objetos Oracle se referirem a objetos de sistema adicionais, você deve selecionar esses objetos. Se você não selecionar os objetos do sistema que são referenciados por seus objetos de banco de dados Oracle, o SSMA relatará erros de conversão. Se você receber erros de conversão causados por falta de objetos do sistema, selecione os objetos ausentes nessa caixa de diálogo. Em seguida, você pode repetir a conversão, conforme necessário.  
  
