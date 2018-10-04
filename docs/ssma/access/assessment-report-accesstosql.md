---
title: Relatório de avaliação (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Assessment Report dialog box
- Conversion Report dialog box
ms.assetid: ba6f53aa-0049-4c49-8bb8-607a8bfaa737
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d6a73f88a0c1bc0ab2235241f7801c8fbc0f8328
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47660334"
---
# <a name="assessment-report-accesstosql"></a>Relatório de avaliação (AccessToSQL)
A janela relatório de avaliação mostra os resultados da conversão de objetos de banco de dados para [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, e também pode ajudar a estimar a complexidade e custo de seus projetos de migração.  
  
Para criar um relatório de avaliação, selecionar objetos a ser convertido no Gerenciador de metadados de origem, clique com botão direito **bancos de dados**e, em seguida, selecione **criar relatório**. Também é possível exibir este relatório automaticamente após a conversão de esquemas. No entanto, o nome do relatório será o relatório de conversão. Para obter mais informações, consulte [projeto configurações (GUI) (SSMA comuns)](http://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
## <a name="options"></a>Opções  
**Painel do Explorer**  
Contém uma hierarquia de objetos no relatório de avaliação. Expanda pastas para exibir os subcomponentes e objetos individuais. Quando você clica em uma categoria ou um objeto, as estatísticas de conversão para essa categoria ou um objeto são exibidos no painel de detalhes.  
  
**Painel de detalhes**  
Mostra a conversão de mensagens de estatísticas ou erro e aviso para o objeto selecionado. Por exemplo, se a pasta de tabelas é selecionada, o painel de detalhes mostrará os números de chaves estrangeiras, índices, chaves primárias e tabelas que foram convertidas.  
  
**Painel mensagens**  
Mostra os erros, avisos e mensagens de informações que foram geradas quando o relatório de avaliação foi criado. As mensagens são agrupadas por número.  
  
Para exibir detalhes da mensagem, clique **erros**, **avisos**, ou **mensagens**e, em seguida, expanda uma mensagem. O SSMA exibirá a lista de objetos que têm esse erro. Clique em um objeto para exibir todos os detalhes de conversão para o objeto.  
  
## <a name="see-also"></a>Consulte também  
[Reference(Access) de Interface do usuário](http://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
