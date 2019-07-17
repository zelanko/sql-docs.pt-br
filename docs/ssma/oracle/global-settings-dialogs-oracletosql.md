---
title: Configurações globais (caixas de diálogo) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 43989355-cebf-4d8b-ba3d-fa8546e70230
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 4fc68e8b8d3fc009b766f0fb0be97f1124797764
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68259657"
---
# <a name="global-settings-dialogs--oracletosql"></a>Configurações globais (caixas de diálogo) (OracleToSQL)
Use a página de caixas de diálogo do **configurações globais** caixa de diálogo para especificar as configurações de aviso para o SSMA e uma ação do usuário padrão.  
  
Para acessar as configurações de caixa de diálogo sobre o **ferramentas** menu, selecione **configurações globais**, clique em **GUI** na parte inferior do painel esquerdo e, em seguida, selecione **caixas de diálogo**.  
  
## <a name="options"></a>Opções  
**Avisar antes de substituir os objetos**  
Quando o SSMA converte objetos para o SQL Server, alguns objetos talvez já exista nos metadados do SQL Server do projeto. Esses objetos podem já foram convertidos ou os objetos simplesmente podem ter o mesmo nome dentro do esquema de destino que objetos que serão convertidas.  
  
Use esta opção para especificar se o SSMA solicitará que você para substituir as definições de objeto duplicados:  
  
-   Se você selecionar **verdadeira**, SSMA exibirá uma caixa de diálogo de aviso quando ele encontra um objeto duplicado. Nesta caixa de diálogo, você pode especificar para substituir os objetos individuais ou todos os objetos duplicados ou para ignorar objetos individuais ou para todos os objetos duplicados.  
  
-   Se você selecionar **falsos**, o **ação padrão de substituição de objeto** opção é exibida em que você especifica a ação padrão.  
  
**Ação de padrão de substituição de objeto**  
Essa opção aparecerá se você selecionar **falsos** para o **Avisar antes de substituir objetos** opção.  
  
Use esta opção para especificar o comportamento de substituição de objeto padrão:  
  
-   Se você selecionar **verdadeira**, SSMA substituirá automaticamente os objetos nos metadados do projeto do SQL Server que têm o mesmo nome e estão no mesmo esquema de destino como o objeto a ser convertido.  
  
-   Se você selecionar **falsos**, SSMA não substitui os metadados de objeto durante a conversão.  
  
