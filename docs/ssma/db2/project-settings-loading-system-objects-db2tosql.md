---
description: Configurações do projeto (carregando objetos do sistema) (DB2ToSQL)
title: Configurações do projeto (carregando objetos do sistema) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9a545233-1b0a-488a-a1ec-c33aa608dcc1
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: cb0f25ce5063a22fb89d0afa8619b90d34a96f16
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426958"
---
# <a name="project-settingsloading-system-objects-db2tosql"></a>Configurações do projeto (carregando objetos do sistema) (DB2ToSQL)
A página carregando objetos do sistema da caixa de diálogo **configurações do projeto** permite especificar quais objetos do sistema DB2 o SSMA converte e carrega [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
O painel carregando objetos do sistema está disponível nas caixas de diálogo **configurações do projeto** e **configurações padrão do projeto** :  
  
-   Para especificar as configurações para todos os projetos do SSMA, no menu **ferramentas** , selecione **configurações de projeto padrão**, selecione tipo de projeto de migração para o qual as configurações devem ser exibidas ou alteradas na lista suspensa **versão de destino de migração** clique em **geral** na parte inferior do painel esquerdo e clique em **carregar objetos do sistema**.  
  
-   Para especificar as configurações do projeto atual, no menu **ferramentas** , selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique em **carregar objetos do sistema**.  
  
## <a name="default-settings"></a>Configurações padrão  
A conversão de objetos do sistema consome recursos do sistema e leva tempo. Para melhorar o desempenho, o SSMA seleciona apenas os objetos do sistema usados com mais frequência, conforme mostrado na lista a seguir:  
  
-   Sistema. DBMS_OUTPUT  
  
-   Sistema. DBMS_PIPE  
  
-   Sistema. DBMS_UTILITY  
  
-   Sistema. STANDARDIZATION  
  
-   Sistema. UTL_FILE  
  
-   Sistema. DBMS_LOB  
  
-   Sistema. DBMS_SQL  
  
-   Sistema. DBMS_SESSION  
  
Se os objetos do DB2 se referirem a objetos do sistema adicionais, você deverá selecionar esses objetos. Se você não selecionar os objetos do sistema que são referenciados por seus objetos de banco de dados DB2, o SSMA relatará erros de conversão. Se você receber erros de conversão causados por objetos do sistema ausentes, selecione os objetos ausentes nessa caixa de diálogo. Em seguida, você pode repetir a conversão conforme necessário.  
  
