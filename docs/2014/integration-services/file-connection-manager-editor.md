---
title: Editor do Gerenciador de Conexão de arquivo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.fileconnectionmanager.f1
helpviewer_keywords:
- File Connection Manager Editor
ms.assetid: 051c48e5-3d86-49af-b554-ff62e3de3622
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 95a37202bece446dce6b8a3173415e9d0861ec60
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130805"
---
# <a name="file-connection-manager-editor"></a>Editor do Gerenciador de Conexões de Arquivos
  Use a caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos** para especificar as propriedades usadas para conectar a um arquivo ou pasta.  
  
> [!NOTE]  
>  Você pode definir a propriedade ConnectionString para o gerenciador de conexões de arquivos especificando uma expressão na janela Propriedades do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. No entanto, para evitar um erro de validação ao usar uma expressão para especificar o arquivo ou a pasta, no **Editor do Gerenciador de Conexões de Arquivos**, para **Arquivo/Pasta**, adicione um caminho de arquivo ou de pasta.  
  
 Para obter mais informações sobre o gerenciador de conexões de Arquivos, consulte [File Connection Manager](connection-manager/file-connection-manager.md).  
  
## <a name="options"></a>Opções  
 **Tipo de Uso**  
 Especifique se o **Gerenciador de Conexões de Arquivos** conecta a um arquivo ou pasta existente ou crie um novo arquivo ou pasta.  
  
|Valor|Description|  
|-----------|-----------------|  
|Criar arquivo|Crie um novo arquivo em tempo de execução.|  
|Arquivo existente|Use um arquivo existente.|  
|Criar pasta|Crie uma nova pasta em tempo de execução.|  
|Pasta existente|Use uma pasta existente.|  
  
 **Arquivo / Pasta**  
 Se **Arquivo**, especifique o arquivo a usar.  
  
 Se **Pasta**, especifique a pasta a usar.  
  
 **Procurar**  
 Selecione o arquivo ou pasta usando a caixa de diálogo **Selecionar Arquivo** ou **Procurar Pasta** .  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  