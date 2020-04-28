---
title: Atualizar do banco de dados (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 613a8368-b372-443f-8252-fb6dc31a003d
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: a53c3005aca2e599d8ceb0b973a58bcf2ca5e14c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68060135"
---
# <a name="refresh-from-database-db2tosql"></a>Atualizar do banco de dados (DB2ToSQL)
A caixa de diálogo **Atualizar do banco de dados** permite que você Selecione quais objetos atualizar do banco de dados DB2. As linhas na caixa de diálogo são codificadas por cores com base no estado dos metadados:  
  
-   Se os metadados do objeto tiverem sido alterados localmente e no banco de dados DB2, a linha ficará azul.  
  
-   Se os metadados do objeto forem alterados no banco de dados DB2, mas não no SSMA, a linha será amarela.  
  
-   Se os metadados do objeto tiverem sido alterados localmente, mas não no banco de dados DB2, a linha ficará verde.  
  
-   Se o objeto for novo no banco de dados DB2, a linha será rosa.  
  
Você pode especificar as configurações de atualização de objeto padrão na caixa de diálogo **configurações do projeto** . Para obter mais informações, consulte [configurações do projeto&#40;sincronização&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md).  
  
Para acessar a caixa **de diálogo atualizar do banco de dados** , clique com o botão direito do mouse em um objeto no Gerenciador de metadados DB2 e clique em **Atualizar do banco de dados**.  
  
## <a name="options"></a>Opções  
**Recolher (-)**  
Recolha todos os grupos de objetos para ocultar objetos individuais.  
  
**Expandir (+)**  
Expanda todos os grupos de objetos para mostrar objetos individuais.  
  
**Ocultar/Mostrar objetos iguais**  
Oculta os objetos da lista se os metadados do objeto forem os mesmos no banco de dados DB2 e no SSMA.  
  
**Atualizar do banco de dados (botão de seta)**  
Use o botão de seta para especificar que os metadados dos objetos selecionados devem ser atualizados no SSMA.  
  
**Não atualizar do banco de dados (botão X)**  
Use o botão X para especificar que os metadados dos objetos selecionados não devem ser atualizados no SSMA.  
  
**Legenda**  
Exibe uma caixa de diálogo de **legenda** . A legenda contém o mapeamento entre as cores de linha e os Estados de metadados.  
  
Para manter a caixa de diálogo **legenda** na parte superior da caixa de diálogo **Atualizar do banco de dados** , marque a caixa de seleção **Mostrar na parte superior** .  
  
