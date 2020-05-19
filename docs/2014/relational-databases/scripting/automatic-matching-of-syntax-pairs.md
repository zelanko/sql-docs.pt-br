---
title: Correspondência automática de pares de sintaxe
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [SQL Server], delimiter highlighting
- IntelliSense [SQL Server], syntax pair matching
ms.assetid: bfc54cda-bfd6-4545-a5b9-f9db2ae13769
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e4359a546c350c666190331ab6a8484ca9a99a83
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704089"
---
# <a name="automatic-matching-of-syntax-pairs"></a>Correspondência automática de pares de sintaxe
  A correspondência automática de pares de sintaxe informa imediatamente se os elementos de sintaxe que devem ser codificados em pares estão formando pares corretos. Isso é conhecido como correspondência de delimitadores no Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , correspondência de colchetes no Editor de Consultas XMLA do Analysis Services e correspondência de parênteses nos editores MDX e DMX.  
  
## <a name="database-engine-query-editor-delimiter-matching"></a>Correspondência de delimitadores do Editor de Consultas do Mecanismo de Banco de Dados  
 O Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] faz a correspondência de delimitadores que identificam os limites dos blocos de código. A correspondência é feita de duas maneiras:  
  
-   O editor realça ambos delimitadores em um par quando você termina de digitar o segundo delimitador do par.  
  
-   Sempre que o cursor estiver em um dos delimitadores de um par, você poderá usar o atalho de teclado CTRL+] para saltar para o delimitador correspondente.  
  
### <a name="delimiter-pairs"></a>Pares de delimitadores  
 A correspondência automática de delimitadores reconhece os seguintes conjuntos de delimitadores:  
  
|Delimitador inicial|Delimitador de fechamento|  
|--------------------|-----------------------|  
|**(**|**)**|  
|**BEGIN**|**END**|  
|**BEGIN TRY**|**END TRY**|  
|**BEGIN CATCH**|**END CATCH**|  
  
 A correspondência automática de delimitadores não reconhece os delimitadores de identificadores entre colchetes ([ObjectName]) ou identificadores entre aspas ("ObjectName"). A correspondência de pares não faz a correspondência dos delimitadores aspas simples de literais de cadeia de caracteres ('cadeia de caracteres') porque a codificação por cores já indica visualmente se a cadeia de caracteres foi delimitada ou não.  
  
### <a name="delimiter-highlighting"></a>Realce de delimitadores  
 A correspondência realça os elementos inicial e de fechamento de um par de delimitadores. Isso permite identificar visualmente os blocos de código e verificar se existem pares de delimitadores incompletos.  
  
 Os delimitadores são realçados quando você digita a letra final que completa o par. Por exemplo, em um par BEGIN END em que você digita BEGIN primeiro, seguido por END, o realce será ativado quando você digitar a letra final de END. Não é necessário digitar o delimitador inicial seguido pelo delimitador de fechamento para ativar o realce. Se você digitar END primeiro e, em seguida, retroceder no script e digitar BEGIN, o realce será ativado quando você digitar a letra final de BEGIN. A letra final digitada não precisa ser a letra final do delimitador. Por exemplo, se você digitar incorretamente BEGIN como BEIN, quando inserir o G final, o par BEGIN END será realçado.  
  
 Os par de delimitadores permanecerá realçado até que você mova o cursor. O realce é desativado quando o cursor se move, mesmo que a nova posição do cursor permaneça no mesmo delimitador. Você pode reativar o realce excluindo e digitando novamente qualquer letra de qualquer membro do par.  
  
## <a name="analysis-services-xmla-query-editor-brace-matching"></a>Correspondência de colchetes do Editor de Consultas XMLA do Analysis Services  
 A correspondência de colchetes do Editor de Consultas XMLA mostra se você fechou os elementos realçando os colchetes de abertura e de fechamento. Também é possível usar o atalho de teclado CTRL+] para saltar de uma chave para a chave correspondente.  
  
 O Editor de Consultas XMLA faz a correspondência de chaves dos seguintes termos:  
  
-   Correspondência de marcas inicial e de fim.  
  
-   Qualquer par de "\<" e colchete angular ">".  
  
-   Início e fim de comentários.  
  
-   Início e fim de instruções de processamento.  
  
-   Início e fim de blocos CDATA.  
  
-   Início e fim de declarações DTD.  
  
-   Aspas de abertura e fechamento em abributos.  
  
## <a name="mdx-and-dmx-editor-parenthesis-matching"></a>Correspondência de parênteses dos Editores MDX e DMX  
 Os Editores MDX (Expressões Multidimensionais) e DMX (Expressões de Mineração de Dados) combinam automaticamente pares de parênteses nas funções.  
  
  
