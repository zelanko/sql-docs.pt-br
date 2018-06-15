---
title: Caixa de diálogo Importar Políticas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.importpolicy.f1
ms.assetid: 78ab5f6e-2f13-4788-937e-8892ef4e2345
caps.latest.revision: 22
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0e672c7cfb95870236e6e6ed4601790fda6d0a87
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32955351"
---
# <a name="import-policies-dialog-box"></a>Caixa de diálogo Importar Políticas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use esta caixa de diálogo para importar uma ou mais políticas (e suas condições referenciadas) salvas como arquivo XML na instância atual do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] .  
  
## <a name="options"></a>Opções  
 **Arquivos a importar**  
 Para importar uma política de um arquivo XML, digite o caminho e o nome do arquivo ou use o botão Procurar (**...**).  
  
 **Substituir duplicatas por itens importados**  
 Selecione para substituir as políticas ou condições existentes com o mesmo nome, caso elas já existam nessa instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Uma condição com uma política dependente não pode ser substituída, a menos que a política dependente também esteja sendo substituída. Se esta opção não estiver selecionada uma condição existente que esteja usando a mesma expressão de condição não causará um erro.  
  
 **Estado da política**  
 Selecione o estado que você deseja para a política importada:  
  
-   **Preservar estado de política na importação**  
  
-   **Habilitar todas as políticas na importação**  
  
-   **Desabilitar todas as políticas na importação**  
  
## <a name="see-also"></a>Consulte Também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Importar política de Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/import-a-policy-based-management-policy.md)   
 [Exportar uma política do Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/export-a-policy-based-management-policy.md)  
  
  
