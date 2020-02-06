---
title: Referência de interface do usuário da caixa de diálogo Adicionar Gerenciador de Conexões de Arquivos | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.fileconnection.f1
helpviewer_keywords:
- Add File Connection Manager
ms.assetid: 9370bfb5-5993-4ad8-a9cd-2de53f320f34
author: chugugrace
ms.author: chugu
ms.openlocfilehash: dc0df82879f835428640b403a5d9b2befa66e34a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71294504"
---
# <a name="add-file-connection-manager-dialog-box-ui-reference"></a>Referência da interface do usuário da caixa de diálogo Adicionar Gerenciador de Conexões de Arquivos

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use a caixa de diálogo do **Adicionar Gerenciador de Conexões de Arquivos** para definir uma conexão com um grupo de arquivos ou pastas.  
  
 Para obter mais informações sobre o gerenciador de conexões de Vários Arquivos, consulte [Multiple Files Connection Manager](../../integration-services/connection-manager/multiple-files-connection-manager.md).  
  
> [!NOTE]  
>  As tarefas internas e os componentes de fluxo de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não usam o gerenciador de conexões de vários arquivos. No entanto você pode usar o gerenciador de conexões na tarefa Script ou no componente Script.  
  
## <a name="options"></a>Opções  
 **Tipo de uso**  
 Especifique os tipos de arquivos a serem usados para o gerenciador de conexões de vários arquivos.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Criar arquivos**|O gerenciador de conexões criará os arquivos.|  
|**Arquivos existentes**|O gerenciador de conexões utilizará arquivos existentes.|  
|**Criar pastas**|O gerenciador de conexões criará as pastas.|  
|**Pastas existentes**|O gerenciador de conexões utilizará pastas existentes.|  
  
 **Arquivos/Pastas**  
 Exiba os arquivos ou pastas que você adicionou usando os botões descritos abaixo.  
  
 **Adicionar**  
 Adicione um arquivo usando a caixa de diálogo **Selecionar Arquivos** ou adicione uma pasta usando a caixa de diálogo **Procurar pasta** .  
  
 **Editar**  
 Selecione um arquivo ou pasta e substitua-o por um arquivo ou pasta diferente usando a caixa de diálogo **Selecionar arquivos** ou **Procurar pasta** .  
  
 **Remover**  
 Selecione um arquivo ou pasta e remova-o da lista usando o botão **Remover** .  
  
 **Botões de seta**  
 Selecione um arquivo ou pasta e use os botões de seta para movê-los para cima ou para baixo para especificar a sequência de acesso.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
  
  
