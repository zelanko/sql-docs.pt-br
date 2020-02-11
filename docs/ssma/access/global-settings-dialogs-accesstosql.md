---
title: Configurações globais (caixas de diálogo) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 6c2204f2-d49e-49ba-9c0f-f14cf07fa561
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5b8ef85b9d0d997ed8aae05fc53aa685a2dcacfa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67986410"
---
# <a name="global-settings-dialogs-accesstosql"></a>Configurações globais (caixas de diálogo) (AccessToSQL)
Use a página diálogos da caixa de diálogo **configurações globais** para especificar as configurações de ação e aviso do usuário padrão para o SSMA.  
  
Para acessar as configurações da caixa de diálogo no menu **ferramentas** , selecione **configurações globais**, clique em **GUI** na parte inferior do painel esquerdo e, em seguida, selecione **caixas de diálogo**.  
  
## <a name="options"></a>Opções  
**Mostrar assistente de migração na inicialização**  
No SSMA para Access, você tem a opção de habilitar ou desabilitar o **Assistente de migração** na inicialização do aplicativo SSMA. Por padrão, essa opção é **verdadeira**.  
  
-   Se a opção for definida como **true**, a caixa de diálogo Assistente de migração será mostrada inicialmente quando você abrir o aplicativo SSMA para Access.  
  
-   Se a opção for definida como **false**, o assistente de migração não será exibido e você terá que acessá-lo manualmente no menu **arquivo** , se necessário.  
  
**Avisar antes de substituir objetos**  
Quando o SSMA converte objetos em SQL Server, alguns objetos podem já existir nos metadados de SQL Server do projeto. Esses objetos podem já ter sido convertidos ou os objetos podem simplesmente ter o mesmo nome dentro do esquema de destino como objetos que você pretende converter.  
  
Use esta opção para especificar se o SSMA deve solicitar que você substitua definições de objetos duplicadas:  
  
-   Se você selecionar **verdadeiro**, o SSMA exibirá uma caixa de diálogo de aviso quando encontrar um objeto duplicado. Nesta caixa de diálogo, você pode especificar para substituir objetos individuais ou todos os objetos duplicados, ou para ignorar objetos individuais ou todos os objetos duplicados.  
  
-   Se você selecionar **falso**, a opção de **ação substituir objeto padrão** será exibida onde você especificar a ação padrão.  
  
**Ação padrão de substituição de objeto**  
Essa opção será exibida se você selecionar **falso** para a opção **avisar antes de substituir objetos** .  
  
Use esta opção para especificar o comportamento de substituição do objeto padrão:  
  
-   Se você selecionar **true**, o SSMA substituirá automaticamente os objetos no SQL Server metadados do projeto que têm o mesmo nome e estarão no mesmo esquema de destino que o objeto a ser convertido.  
  
-   Se você selecionar **falso**, o SSMA não substituirá os metadados do objeto durante a conversão.  
  
