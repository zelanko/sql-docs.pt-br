---
title: Caixa de diálogo Avisos de Validação (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65556
- vdt.dlgbox.validationwarnings
ms.assetid: fc76e234-ec9c-4a19-a65b-cb558ec8268e
author: stevestein
ms.author: sstein
ms.openlocfilehash: bea67df36c5c522484a166927378b7746d62561f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85040633"
---
# <a name="validation-warnings-dialog-box-visual-database-tools"></a>Caixa de diálogo Avisos de Validação (Visual Database Tools)
  Essa caixa de diálogo aparece se você tentar salvar modificações com efeitos colaterais potencialmente prejudiciais, ou se houver probabilidade da operação de confirmação de banco de dados falhar. Essa caixa de diálogo indica o que aqueles efeitos colaterais podem ser ou por que a operação de confirmação pode falhar. Isso lhe permite continuar com a modificação ou cancelar a operação.  
  
> [!NOTE]  
>  Essa caixa de diálogo aparece quando você tenta transmitir suas modificações ao banco de dados ou quando você salva um script de alteração.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Criar tabelas &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
