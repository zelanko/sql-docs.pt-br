---
description: Configurações globais (caixas de diálogo) (MySQLToSQL)
title: Configurações globais (caixas de diálogo) (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 6df20fbb-e92d-475f-a94d-aaf70b06eb9b
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: e902927b90ff868e8766b3eb1fe9839938dd8ece
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463411"
---
# <a name="global-settings-dialogs-mysqltosql"></a>Configurações globais (caixas de diálogo) (MySQLToSQL)
Use a página diálogos da caixa de diálogo **configurações globais** para especificar as configurações de ação e aviso do usuário padrão para o SSMA.  
  
Para acessar as configurações da caixa de diálogo no menu **ferramentas** , selecione **configurações globais**, clique em **GUI** na parte inferior do painel esquerdo e, em seguida, selecione **caixas de diálogo**.  
  
## <a name="options"></a>Opções  
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
  
