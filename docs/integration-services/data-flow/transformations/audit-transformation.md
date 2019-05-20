---
title: Transformação Auditoria | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.audittrans.f1
- sql13.dts.designer.audittransformation.f1
helpviewer_keywords:
- environment data in packages [Integration Services]
- Audit transformation
ms.assetid: 8c143682-9c81-4150-83d6-1d9678151d37
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9161fe71f82d2ca0f2f31805dc07beba387bc28d
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726298"
---
# <a name="audit-transformation"></a>Transformação Auditoria

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A opção Auditar Transformação permite ao fluxo de dados de um pacote incluir dados sobre o ambiente em que o pacote é executado. Por exemplo, o nome do pacote, o computador e o operador podem ser adicionados ao fluxo de dados. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui variáveis do sistema que fornecem essas informações.  
  
## <a name="system-variables"></a>Variáveis do sistema  
 A tabela a seguir descreve as variáveis do sistema que podem ser usadas por Auditar Transformação.  
  
|Variável do sistema|Índice|Descrição|  
|---------------------|-----------|-----------------|  
|**ExecutionInstanceGUID**|0|O GUID que identifica a instância de execução do pacote.|  
|**PackageID**|1|O identificador exclusivo do pacote.|  
|**PackageName**|2|O nome do pacote.|  
|**VersionID**|3|A versão do pacote.|  
|**ExecutionStartTime**|4|A hora de início da execução do pacote.|  
|**MachineName**|5|O nome do computador.|  
|**UserName**|6|O nome de logon da pessoa que iniciou o pacote.|  
|**TaskName**|7|O nome da tarefa Fluxo de Dados à qual Auditar Transformação está associada.|  
|**TaskId**|8|O identificador exclusivo da tarefa Fluxo de Dados.|  
  
## <a name="configuration-of-the-audit-transformation"></a>Configuração da Transformação Auditoria  
 Para configurar a opção Auditar Transformação, forneça o nome de uma nova coluna de saída a ser adicionada à saída da transformação e, em seguida, mapeie a variável do sistema para a coluna de saída. Você pode mapear uma única variável do sistema para várias colunas.  
  
 Essa transformação tem uma entrada e uma saída. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="audit-transformation-editor"></a>Editor de Transformação Auditoria
  A opção Auditar Transformação permite ao fluxo de dados de um pacote incluir dados sobre o ambiente em que o pacote é executado. Por exemplo, o nome do pacote, o computador e o operador podem ser adicionados ao fluxo de dados. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui variáveis do sistema que fornecem essas informações.  
  
### <a name="options"></a>Opções  
 **Nome da coluna de saída**  
 Forneça um nome para a nova coluna de saída que conterá as informações de auditoria.  
  
 **Tipo de auditoria**  
 Selecione uma variável de sistema disponível para fornecer as informações de auditoria.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**GUID de instância de execução**|Insira o GUID que identifica com exclusividade a instância de execução do pacote.|  
|**ID do Pacote**|Insira o GUID que identifica com exclusividade o pacote.|  
|**Nome do pacote**|Insira o nome do pacote.|  
|**ID da Versão**|Insira o GUID que identifica com exclusividade a versão do pacote.|  
|**Hora de início de execução**|Insira a hora de início de execução do pacote.|  
|**Nome do computador**|Insira o nome do computador no qual o pacote foi inicializado.|  
|**User name**|Insira o nome de logon do usuário que inicializou o pacote.|  
|**Nome da tarefa**|Insira o nome da tarefa de Fluxo de Dados com a qual Auditar Transformação está associada.|  
|**ID da Tarefa**|Insira o GUID que identifica com exclusividade a tarefa de Fluxo de Dados com a qual Auditar Transformação está associada.|  
  
  
