---
title: "Caixa de diálogo Avisos de Validação (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:65556
- vdt.dlgbox.validationwarnings
ms.assetid: fc76e234-ec9c-4a19-a65b-cb558ec8268e
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed5e7c20f59ffd598cd6de1aa8431e1498e62b1e
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="validation-warnings-dialog-box-visual-database-tools"></a>Caixa de diálogo Avisos de Validação (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Essa caixa de diálogo aparece se você tenta salvar modificações com efeitos colaterais potencialmente prejudiciais ou se há probabilidade de a operação de confirmação de banco de dados falhar. Essa caixa de diálogo indica o que aqueles efeitos colaterais podem ser ou por que a operação de confirmação pode falhar. Isso lhe permite continuar com a modificação ou cancelar a operação.  
  
> [!NOTE]  
> Essa caixa de diálogo aparece quando você tenta transmitir suas modificações ao banco de dados ou quando você salva um script de alteração.  
  
A caixa de diálogo pode aparecer por qualquer uma das seguintes razões:  
  
-   Talvez você não tenha permissões para confirmar todas as modificações.  
  
-   Suas modificações resultariam em colunas derivadas, restrições padrão, ou restrições de verificação incorretas.  
  
-   Uma modificação para o tipo de dados de uma coluna poderia causar perda de dados.  
  
-   Uma modificação resultaria em um índice maior que 900 bytes.  
  
-   Uma modificação alteraria uma tabela ou coluna contribuindo para uma exibição associada a esquema ou função definida pelo usuário.  
  
-   Uma modificação resultaria na recriação de uma tabela com um ou mais gatilhos criptografados; os gatilhos serão descartados.  
  
-   Suas modificações geram configurações notáveis de ANSI_NULLS ou ANSI_PADDING ou ambos para as colunas dentro de uma tabela.  
  
## <a name="options"></a>Opções  
**Sim**  
Continue com a operação e gere o script de alteração ou transmita as modificações ao banco de dados. A operação de confirmação ainda pode falhar se você não tiver privilégios para alterar o banco de dados, se suas modificações resultarem em um índice maior que 900 bytes, ou se suas modificações resultarem em uma coluna computada, restrição padrão, ou restrição de verificação incorreta.  
  
**Não**  
Cancela a ação de salvar.  
  
**Salvar Arquivo de Texto**  
Exibe a caixa de diálogo **Salvar como** , permitindo especificar um local para um arquivo de texto contendo a lista de avisos.  
  
## <a name="see-also"></a>Consulte também  
[Criar tabelas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
