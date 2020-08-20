---
description: Atualizar do banco de dados (MySQLToSQL)
title: Atualizar do banco de dados (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 59a6db8f-2db6-4071-9005-928a7231de92
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 027aa6557036c54c4b7e143cd94149fa5e8fe4f1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492355"
---
# <a name="refresh-from-database-mysqltosql"></a>Atualizar do banco de dados (MySQLToSQL)
A caixa **de diálogo atualizar do banco de dados** permite selecionar quais objetos atualizar do banco de dados MySQL. As linhas na caixa de diálogo são codificadas por cores com base no estado dos metadados:  
  
-   Se os metadados do objeto tiverem sido alterados localmente e no banco de dados MySQL, a linha ficará azul.  
  
-   Se os metadados do objeto tiverem sido alterados no banco de dados MySQL, mas não no SSMA, a linha será amarela.  
  
-   Se os metadados do objeto tiverem sido alterados localmente, mas não no banco de dados MySQL, a linha ficará verde.  
  
-   Se o objeto for novo no banco de dados MySQL, a linha será rosa.  
  
Você pode especificar as configurações de atualização de objeto padrão na caixa de diálogo **configurações do projeto** . Para obter mais informações, consulte [configurações do projeto &#40;sincronização&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
Para acessar a caixa **de diálogo atualizar do banco de dados** , clique com o botão direito do mouse em um objeto no Gerenciador de metadados MySQL e clique em **Atualizar do banco de dados**.  
  
## <a name="options"></a>Opções  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Recolher (-)**|Recolha todos os grupos de objetos para ocultar objetos individuais.|  
|**Expandir (+)**|Expanda todos os grupos de objetos para mostrar objetos individuais.|  
|**Ocultar/Mostrar objetos iguais**|Oculta os objetos da lista se os metadados do objeto forem os mesmos no banco de dados MySQL e no SSMA.|  
|**Atualizar do banco de dados (botão de seta)**|Use o botão de seta para especificar que os metadados dos objetos selecionados devem ser atualizados no SSMA.|  
|**Não atualizar do banco de dados (botão X)**|Use o botão X para especificar que os metadados dos objetos selecionados não devem ser atualizados no SSMA.|  
|**Legenda**|Exibe uma caixa de diálogo de **legenda** . A legenda contém o mapeamento entre as cores de linha e os Estados de metadados.<br /><br />Para manter a caixa de diálogo **legenda** na parte superior da caixa de diálogo **Atualizar do banco de dados** , marque a caixa de seleção **Mostrar na parte superior** .|  
  
