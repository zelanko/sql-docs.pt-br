---
title: "Configurações (objetos de sistema de carregamento) do projeto (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9418cb34-d869-4d24-95b3-6cb9db949bb0
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5cb5bdd526addeb11acf0553bbf022ff75415e70
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="project-settingsloading-system-objects-oracletosql"></a>Configurações (objetos de sistema de carregamento) do projeto (OracleToSQL)
A página carregar objetos do sistema do **configurações de projeto** caixa de diálogo permite que você especifique quais objetos de sistema Oracle SSMA converte e carrega em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
O painel ao carregar objetos do sistema está disponível na **configurações de projeto** e **configurações de projeto padrão** caixas de diálogo:  
  
-   Para especificar configurações para todos os projetos do SSMA, no **ferramentas** menu, selecione **configurações de projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibido ou alterado de **versão de destino de migração** suspensa clique **geral** na parte inferior do painel esquerdo e, em seguida, clique **carregar objetos do sistema**.  
  
-   Para especificar as configurações para o projeto atual, no **ferramentas** menu, selecione **configurações de projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique **carregar objetos do sistema**.  
  
## <a name="default-settings"></a>Configurações padrão  
Converter objetos de sistema consome recursos do sistema e leva tempo. Para melhorar o desempenho, o SSMA seleciona somente os objetos de sistema usados com mais frequência, conforme mostrado na lista a seguir:  
  
-   SYS. DBMS_OUTPUT  
  
-   SYS. DBMS_PIPE  
  
-   SYS. DBMS_UTILITY  
  
-   SYS. PADRÃO  
  
-   SYS. UTL_FILE  
  
-   SYS. DBMS_LOB  
  
-   SYS. DBMS_SQL  
  
-   SYS. DBMS_SESSION  
  
Se os objetos Oracle se referem a objetos de sistema adicionais, você deve selecionar os objetos. Se você não selecionar os objetos do sistema que são referenciados por seus objetos de banco de dados Oracle, o SSMA relatará erros de conversão. Se você receber erros de conversão causados pela falta de objetos do sistema, selecione os objetos ausentes na caixa de diálogo. Você pode repetir a conversão conforme necessário.  
  

