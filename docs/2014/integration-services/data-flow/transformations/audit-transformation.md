---
title: Transformação Auditoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.audittrans.f1
helpviewer_keywords:
- environment data in packages [Integration Services]
- Audit transformation
ms.assetid: 8c143682-9c81-4150-83d6-1d9678151d37
author: janinezhang
ms.author: janinez
ms.openlocfilehash: daca48b79b4bb0dd4655bb306c881c199ecfb0a7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84913836"
---
# <a name="audit-transformation"></a>Transformação Auditoria
  A opção Auditar Transformação permite ao fluxo de dados de um pacote incluir dados sobre o ambiente em que o pacote é executado. Por exemplo, o nome do pacote, o computador e o operador podem ser adicionados ao fluxo de dados. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui variáveis do sistema que fornecem essas informações.  
  
## <a name="system-variables"></a>Variáveis do sistema  
 A tabela a seguir descreve as variáveis do sistema que podem ser usadas por Auditar Transformação.  
  
|Variável do sistema|Índice|DESCRIÇÃO|  
|---------------------|-----------|-----------------|  
|`ExecutionInstanceGUID`|0|O GUID que identifica a instância de execução do pacote.|  
|`PackageID`|1|O identificador exclusivo do pacote.|  
|`PackageName`|2|O nome do pacote.|  
|`VersionID`|3|A versão do pacote.|  
|`ExecutionStartTime`|4|A hora de início da execução do pacote.|  
|`MachineName`|5|O nome do computador.|  
|`UserName`|6|O nome de logon da pessoa que iniciou o pacote.|  
|`TaskName`|7|O nome da tarefa Fluxo de Dados à qual Auditar Transformação está associada.|  
|**TaskId**|8|O identificador exclusivo da tarefa Fluxo de Dados.|  
  
## <a name="configuration-of-the-audit-transformation"></a>Configuração da Transformação Auditoria  
 Para configurar a opção Auditar Transformação, forneça o nome de uma nova coluna de saída a ser adicionada à saída da transformação e, em seguida, mapeie a variável do sistema para a coluna de saída. Você pode mapear uma única variável do sistema para várias colunas.  
  
 Essa transformação tem uma entrada e uma saída. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Auditar Editor de Transformação** , consulte [Audit Transformation Editor](../../audit-transformation-editor.md).  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../../common-properties.md)  
  
-   [Propriedades personalizadas da transformação](transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md).  
  
  
