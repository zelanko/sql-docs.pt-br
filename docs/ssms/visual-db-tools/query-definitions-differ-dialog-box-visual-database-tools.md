---
title: Caixa de diálogo Definições de Consulta Diferem (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:69639
- vdtsql.chm:69640
- vdt.dlgbox.querydefinitionsdiffer
ms.assetid: 90383473-2922-40e5-9682-3850849aa856
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4e065ac17e913d766813076df75a6a65ffe9472e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65098265"
---
# <a name="query-definitions-differ-dialog-box-visual-database-tools"></a>Caixa de diálogo Definições de Consulta Diferem (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
A caixa de diálogo notifica que a consulta não pode ser representada graficamente nos painéis de Diagrama e de Critério e que será possível editar a consulta apenas no painel SQL.  
  
A caixa de diálogo pode aparecer ao digitar ou editar uma instrução SQL no painel SQL; depois você irá para outro painel, verificará a consulta ou tentará executar a consulta, e uma das seguintes condições é aplicada:  
  
-   A instrução SQL está incompleta ou contém um ou mais erros de sintaxe.  
  
-   A instrução SQL é válida mas não tem suporte nos painéis gráficos (por exemplo, uma consulta de União).  
  
-   A instrução SQL é válida mas contém sintaxe específica para a conexão de dados que você está usando.  
  
> [!TIP]  
> É possível verificar se uma instrução é válida, usando o botão **Verificar Instrução SQL** na barra de ferramentas **Consulta** .  
  
A caixa de diálogo exibe uma mensagem com o motivo pelo qual a instrução SQL não pôde ser representada e, em seguida, pergunta como você deseja proceder.  
  
> [!NOTE]  
> A caixa de diálogo **Definições de Consulta Diferem** não aparecerá se os painéis de Diagrama e de Critérios estiverem ocultos.  
  
## <a name="options"></a>Opções  
**Botão Ignorar**  
Escolha esse botão para especificar se deseja aceitar a instrução SQL para editá-la ou executá-la mais tarde. Se você aceitar a instrução, os painéis de Diagrama e de Critério aparecerão para indicar que eles não representam a instrução no painel SQL.  
  
**Botão Desfazer**  
Escolha esse botão para descartar as alterações feitas para o painel SQL.  
  
> [!NOTE]  
> Se a instrução estiver correta mas não tiver suporte gráfico pelo Designer de Consulta e Exibição, será possível executá-la mesmo que não esteja representada nos painéis de Diagrama e de Critério. Por exemplo, se você inserir uma consulta de União, a instrução pode ser executada mas não representada nos outros painéis.  
  
## <a name="see-also"></a>Consulte Também  
[Ferramentas do Designer de Consulta e Exibição &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)  
  
