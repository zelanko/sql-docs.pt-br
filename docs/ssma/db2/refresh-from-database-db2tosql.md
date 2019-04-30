---
title: Atualização do banco de dados (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 613a8368-b372-443f-8252-fb6dc31a003d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ef7778854248f194c01254b9cd6f833f67e9cefc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63269995"
---
# <a name="refresh-from-database-db2tosql"></a>Atualização do banco de dados (DB2ToSQL)
O **Refresh do banco de dados** caixa de diálogo permite que você selecione quais objetos de atualização do banco de dados DB2. Linhas na caixa de diálogo são codificadas por cores com base no estado de metadados:  
  
-   Se os metadados do objeto foi alterado localmente e no banco de dados DB2, a linha é azul.  
  
-   Se os metadados do objeto foi alterado no banco de dados DB2, mas não no SSMA, a linha será amarela.  
  
-   Se os metadados do objeto foi alterado localmente, mas não no banco de dados DB2, a linha está verde.  
  
-   Se o objeto é novo no banco de dados DB2, a linha é rosa.  
  
Você pode especificar configurações de atualização do objeto padrão no **configurações do projeto** caixa de diálogo. Para obter mais informações, consulte [configurações do projeto&#40;sincronização&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md).  
  
Para acessar o **atualização do banco de dados** caixa de diálogo, clique com botão direito um objeto no Gerenciador de metadados do DB2 e clique em **atualização do banco de dados**.  
  
## <a name="options"></a>Opções  
**Recolher (-)**  
Recolha todos os grupos de objeto para ocultar objetos individuais.  
  
**Expandir (+)**  
Expanda todos os grupos de objeto para mostrar objetos individuais.  
  
**Ocultar/Mostrar objetos iguais**  
Oculta os objetos da lista se os metadados do objeto são o mesmo do banco de dados do DB2 e do SSMA.  
  
**Atualização do banco de dados (botão de seta)**  
Use o botão de seta para especificar que os metadados para os objetos selecionados devem ser atualizados no SSMA.  
  
**Fazer a atualização não do banco de dados (botão X)**  
Use o botão X para especificar os metadados para os objetos selecionados não devem ser atualizados no SSMA.  
  
**Legenda**  
Exibe uma **legenda** caixa de diálogo. A legenda contém o mapeamento entre os estados de metadados e as cores de linha.  
  
Para manter o **legenda** caixa de diálogo, na parte superior das **atualização do banco de dados** caixa de diálogo, selecione o **Mostrar na parte superior** caixa de seleção.  
  
