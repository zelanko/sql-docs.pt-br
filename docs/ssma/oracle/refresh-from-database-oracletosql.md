---
title: Atualizar do banco de dados (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 84492f44-c368-4c75-954d-7307a2d2bbc0
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: ba9a56c5fb47be4db081aebb3753db2c3e9ed6ad
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266541"
---
# <a name="refresh-from-database-oracletosql"></a>Atualização do banco de dados (OracleToSQL)
A caixa de diálogo **Atualizar do banco de dados** permite selecionar quais objetos atualizar do banco de dados Oracle. As linhas na caixa de diálogo são codificadas por cores com base no estado dos metadados:  
  
-   Se os metadados do objeto tiverem sido alterados localmente e no banco de dados Oracle, a linha ficará azul.  
  
-   Se os metadados do objeto tiverem sido alterados no banco de dados Oracle, mas não no SSMA, a linha será amarela.  
  
-   Se os metadados do objeto tiverem sido alterados localmente, mas não no banco de dados Oracle, a linha ficará verde.  
  
-   Se o objeto for novo no banco de dados Oracle, a linha será rosa.  
  
Você pode especificar as configurações de atualização de objeto padrão na caixa de diálogo **configurações do projeto** . Para obter mais informações, consulte [configurações do projeto&#40;sincronização&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md).  
  
Para acessar a caixa **de diálogo atualizar do banco de dados** , clique com o botão direito do mouse em um objeto no Gerenciador de metadados Oracle e clique em **Atualizar do banco de dados**.  
  
## <a name="options"></a>Opções  
**Recolher (-)**  
Recolha todos os grupos de objetos para ocultar objetos individuais.  
  
**Expandir (+)**  
Expanda todos os grupos de objetos para mostrar objetos individuais.  
  
**Ocultar/Mostrar objetos iguais**  
Oculta os objetos da lista se os metadados do objeto forem os mesmos no banco de dados Oracle e no SSMA.  
  
**Atualizar do banco de dados (botão de seta)**  
Use o botão de seta para especificar que os metadados dos objetos selecionados devem ser atualizados no SSMA.  
  
**Não atualizar do banco de dados (botão X)**  
Use o botão X para especificar que os metadados dos objetos selecionados não devem ser atualizados no SSMA.  
  
**Legenda**  
Exibe uma caixa de diálogo de **legenda** . A legenda contém o mapeamento entre as cores de linha e os Estados de metadados.  
  
Para manter a caixa de diálogo **legenda** na parte superior da caixa de diálogo **Atualizar do banco de dados** , marque a caixa de seleção **Mostrar na parte superior** .  
  
