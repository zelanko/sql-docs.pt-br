---
title: Configurações globais (caixas de diálogo) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: e11452b7-ba94-4367-a745-5ccf1764acec
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c9688410b2b5768bcc5cb323d986d949f8a16f67
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="global-settings-dialogs--sybasetosql"></a>Configurações globais (caixas de diálogo) (SybaseToSQL)
Use a página de caixas de diálogo do **configurações globais** caixa de diálogo para especificar as configurações de aviso para o SSMA e uma ação do usuário padrão.  
  
Para acessar as caixa de diálogo configurações no **ferramentas** menu, selecione **configurações globais**, clique em **GUI** na parte inferior do painel esquerdo e, em seguida, selecione **caixas de diálogo**.  
  
## <a name="options"></a>Opções  
**Avisar antes de substituir objetos**  
Quando o SSMA converte objetos para o SQL Server, alguns objetos talvez já exista nos metadados do SQL Server do projeto. Esses objetos podem já foram convertidos, ou os objetos simplesmente podem ter o mesmo nome dentro do esquema de destino que objetos que serão convertidas.  
  
Use esta opção para especificar se o SSMA deve pedir para substituir as definições de objeto duplicado:  
  
-   Se você selecionar **True**, SSMA exibirá uma caixa de diálogo de aviso quando encontra um objeto duplicado. Nesta caixa de diálogo, você pode especificar para substituir os objetos individuais ou todos os objetos duplicados, ou para ignorar objetos individuais ou todos os objetos duplicados.  
  
-   Se você selecionar **False**, o **ação padrão de substituição de objeto** opção é exibida, onde você pode especificar a ação padrão.  
  
**Ação de padrão de substituição de objeto**  
Essa opção será exibida se você selecionar **False** para o **Avisar antes de substituir objetos** opção.  
  
Use esta opção para especificar o comportamento de substituição de objeto padrão:  
  
-   Se você selecionar **True**, SSMA substituirá automaticamente objetos nos metadados do projeto do SQL Server que têm o mesmo nome e estão no mesmo esquema de destino como o objeto a ser convertido.  
  
-   Se você selecionar **False**, SSMA não substitui os metadados do objeto durante a conversão.  
  
