---
title: Validando dados (Suplemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 71eda98f-01a4-4fff-8246-be3133782523
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 02a788c5675a763d7285c9986eef94f3621e6a9f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65478816"
---
# <a name="validating-data-mds-add-in-for-excel"></a>Validando dados (Suplemento do MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], quando você publica dados, ocorrem dois tipos de validação:  
  
-   Qualquer regra de negócio definida é aplicada aos dados.  
  
-   Os dados são verificados quanto a valores de atributo permitidos (por exemplo, número de caracteres ou tipo de dados).  
  
 Em cada caso, os dados válidos são publicados no repositório do MDS. Os dados que não são válidos são realçados e detalhes do erro podem ser mostrados em colunas de status.  
  
## <a name="when-validation-occurs"></a>Quando ocorre a validação  
 No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], a validação ocorre quando você publica novos dados ou altera os existentes ou quando aplica regras de negócio manualmente.  
  
 Quando as regras de negócio falham, os dados ainda são publicados no repositório do MDS. Quando a validação de entrada falha, os dados não são publicados no repositório.  
  
## <a name="validation-statuses"></a>Status da validação  
 No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], os status de validação a seguir são possíveis.  
  
|Status|Descrição|  
|------------|-----------------|  
|Erro|Um ou mais valores na linha validação falharam na validação em relação a regras de negócio definidas por um administrador do MDS.|  
|Não Validado|Os valores na linha ainda não foram validados em relação a regras de negócio.|  
|Êxito|Todos os valores na linha passaram na validação quanto a regras de negócio.|  
  
## <a name="input-statuses"></a>Status de Entrada  
 No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], os status de entrada a seguir são possíveis  
  
|Status|Descrição|  
|------------|-----------------|  
|Erro|Um ou mais valores na linha não atendem aos requisitos de sistema, como comprimento ou tipo de dados. O valor não é atualizado no repositório do MDS.|  
|Nova Linha|Os valores na linha ainda não foram publicados no repositório do MDS.|  
|Somente leitura|O usuário registrado em log tem permissões Somente leitura para um ou mais valores na linha e os valores não podem ser atualizados.|  
|Inalterado|Nenhum valor na linha foi alterado na planilha. Isso não significa que os valores no repositório não foram alterados; para obter os dados mais recentes na planilha, no grupo **Conectar e Carregar** , clique em **Carregar ou Atualizar**.<br /><br /> Essa é a configuração padrão para cada linha.|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Determine quais valores não transmitem as regras de negócio definidas.|[Aplicar regras de negócio &#40;Suplemento MDS para Excel&#41;](apply-business-rules-mds-add-in-for-excel.md)|  
|Para ajudar a corrigir erros de validação, exiba todas as transações que ocorreram para um membro.|[Exibir todas as anotações ou transações de um membro &#40;Suplemento MDS para Excel&#41;](view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Publicando dados &#40;Suplemento MDS para Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
