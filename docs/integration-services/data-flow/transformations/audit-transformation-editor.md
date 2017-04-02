---
title: "Editor de Transforma&#231;&#227;o Auditoria | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.audittransformation.f1"
helpviewer_keywords: 
  - "Editor de Transformação Auditoria"
ms.assetid: 32786a34-5870-4fde-83c7-ec74d62404b8
caps.latest.revision: 13
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 13
---
# Editor de Transforma&#231;&#227;o Auditoria
  A opção Auditar Transformação permite ao fluxo de dados de um pacote incluir dados sobre o ambiente em que o pacote é executado. Por exemplo, o nome do pacote, o computador e o operador podem ser adicionados ao fluxo de dados. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui variáveis do sistema que fornecem essas informações.  
  
 Para saber mais sobre Auditar Transformação, consulte [Audit Transformation](../../../integration-services/data-flow/transformations/audit-transformation.md).  
  
## Opções  
 **Nome da coluna de saída**  
 Forneça um nome para a nova coluna de saída que conterá as informações de auditoria.  
  
 **Tipo de auditoria**  
 Selecione uma variável de sistema disponível para fornecer as informações de auditoria.  
  
|Value|Description|  
|-----------|-----------------|  
|**GUID de instância de execução**|Insira o GUID que identifica com exclusividade a instância de execução do pacote.|  
|**ID do Pacote**|Insira o GUID que identifica com exclusividade o pacote.|  
|**Nome do pacote**|Insira o nome do pacote.|  
|**ID da Versão**|Insira o GUID que identifica com exclusividade a versão do pacote.|  
|**Hora de início de execução**|Insira a hora de início de execução do pacote.|  
|**Nome do computador**|Insira o nome do computador no qual o pacote foi inicializado.|  
|**Nome de usuário**|Insira o nome de logon do usuário que inicializou o pacote.|  
|**Nome da tarefa**|Insira o nome da tarefa de Fluxo de Dados com a qual Auditar Transformação está associada.|  
|**ID da Tarefa**|Insira o GUID que identifica com exclusividade a tarefa de Fluxo de Dados com a qual Auditar Transformação está associada.|  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)  
  
  