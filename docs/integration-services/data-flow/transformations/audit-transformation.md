---
title: "Transforma&#231;&#227;o Auditoria | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.audittrans.f1"
helpviewer_keywords: 
  - "dados de ambiente em pacotes [Integration Services]"
  - "Transformação Auditoria"
ms.assetid: 8c143682-9c81-4150-83d6-1d9678151d37
caps.latest.revision: 46
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 46
---
# Transforma&#231;&#227;o Auditoria
  A opção Auditar Transformação permite ao fluxo de dados de um pacote incluir dados sobre o ambiente em que o pacote é executado. Por exemplo, o nome do pacote, o computador e o operador podem ser adicionados ao fluxo de dados. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui variáveis do sistema que fornecem essas informações.  
  
## Variáveis do sistema  
 A tabela a seguir descreve as variáveis do sistema que podem ser usadas por Auditar Transformação.  
  
|Variável do sistema|Índice|Description|  
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
  
## Configuração da Transformação Auditoria  
 Para configurar a opção Auditar Transformação, forneça o nome de uma nova coluna de saída a ser adicionada à saída da transformação e, em seguida, mapeie a variável do sistema para a coluna de saída. Você pode mapear uma única variável do sistema para várias colunas.  
  
 Essa transformação tem uma entrada e uma saída. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Auditar Editor de Transformação** , consulte [Audit Transformation Editor](../../../integration-services/data-flow/transformations/audit-transformation-editor.md).  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../Topic/Common%20Properties.md)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  