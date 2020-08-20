---
description: Atualizar do banco de dados (AccessToSQL)
title: Atualizar do banco de dados (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3b671f49-c4cc-44fd-801e-e738a8c79415
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 471b1b3891d017858c0f0d035f8207bc8a1d2539
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497771"
---
# <a name="refresh-from-database-accesstosql"></a>Atualizar do banco de dados (AccessToSQL)
A caixa **de diálogo atualizar do banco de dados** permite que você Selecione quais objetos atualizar do banco de dados do Access. As linhas na caixa de diálogo são codificadas por cores com base no estado dos metadados:  
  
-   Se os metadados do objeto tiverem sido alterados localmente e no banco de dados do Access, a linha ficará azul.  
  
-   Se os metadados do objeto forem alterados no banco de dados do Access, mas não no SSMA, a linha será amarela.  
  
-   Se os metadados do objeto tiverem sido alterados localmente, mas não no banco de dados do Access, a linha ficará verde.  
  
-   Se o objeto for novo no banco de dados do Access, a linha será rosa.  
  
Você pode especificar as configurações de atualização de objeto padrão na caixa de diálogo **configurações do projeto** . Para obter mais informações, consulte [configurações do projeto &#40;carregando objetos&#41; &#40;AccessToSQL&#41;](../../ssma/access/project-settings-loading-objects-accesstosql.md)  
  
Para acessar a caixa **de diálogo atualizar do banco de dados** , clique com o botão direito em qualquer nó de **banco de dados** no Gerenciador de metadados do Access e clique em **Atualizar do banco**  
  
