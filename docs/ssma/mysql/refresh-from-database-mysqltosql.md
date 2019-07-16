---
title: Atualização do banco de dados (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 59a6db8f-2db6-4071-9005-928a7231de92
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5acc3153d7305f404c5fc6a0478b83cc0c98bad6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066700"
---
# <a name="refresh-from-database-mysqltosql"></a>Atualizar do banco de dados (MySQLToSQL)
O **Refresh do banco de dados** caixa de diálogo permite que você selecione quais objetos de atualização do banco de dados MySQL. Linhas na caixa de diálogo são codificadas por cores com base no estado de metadados:  
  
-   Se os metadados do objeto foi alterado localmente e no banco de dados MySQL, a linha é azul.  
  
-   Se os metadados do objeto foi alterado no banco de dados MySQL, mas não no SSMA, a linha será amarela.  
  
-   Se os metadados do objeto foi alterado localmente, mas não no banco de dados MySQL, a linha está verde.  
  
-   Se o objeto é novo no banco de dados MySQL, a linha é rosa.  
  
Você pode especificar configurações de atualização do objeto padrão no **configurações do projeto** caixa de diálogo. Para obter mais informações, consulte [configurações do projeto &#40;sincronização&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
Para acessar o **atualização do banco de dados** caixa de diálogo, clique com botão direito um objeto no Gerenciador de metadados do MySQL e clique em **atualização do banco de dados**.  
  
## <a name="options"></a>Opções  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Recolher (-)**|Recolha todos os grupos de objeto para ocultar objetos individuais.|  
|**Expandir (+)**|Expanda todos os grupos de objeto para mostrar objetos individuais.|  
|**Ocultar/Mostrar objetos iguais**|Oculta os objetos da lista se os metadados do objeto são o mesmo no banco de dados MySQL e no SSMA.|  
|**Atualização do banco de dados (botão de seta)**|Use o botão de seta para especificar que os metadados para os objetos selecionados devem ser atualizados no SSMA.|  
|**Fazer a atualização não do banco de dados (botão X)**|Use o botão X para especificar os metadados para os objetos selecionados não devem ser atualizados no SSMA.|  
|**Legenda**|Exibe uma **legenda** caixa de diálogo. A legenda contém o mapeamento entre os estados de metadados e as cores de linha.<br /><br />Para manter o **legenda** caixa de diálogo, na parte superior das **atualização do banco de dados** caixa de diálogo, selecione o **Mostrar na parte superior** caixa de seleção.|  
  
