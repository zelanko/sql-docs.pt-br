---
title: SQLConfigDataSource (dBASE Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], dBASE Driver
ms.assetid: 19909902-054c-4e19-9c06-a212aace13fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 18c6721b4f34772e8c3cd8e4f515233f80566fb3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283966"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (Driver do dBASE)
> [!NOTE]  
>  Este tópico fornece informações específicas do dBASE Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 A função **SQLConfigDataSource,** usada para adicionar, modificar ou excluir uma fonte de dados, usa dinamicamente as seguintes palavras-chave.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|SEQÜÊNCIA DE COLISÃO|A seqüência em que os campos são classificados.<br /><br /> A sequência pode ser: ASCII (o padrão) ou Internacional.<br /><br /> Isso define a mesma opção **que A seqüência de colisão** na caixa de diálogo de configuração.|  
|Defaultdir|A especificação do caminho para o diretório.|  
|DELETED|Para o driver dBASE, especifica se as linhas que foram marcadas como excluídas podem ser recuperadas ou posicionadas. Se definido como 1, as linhas excluídas não serão exibidas; se definido como 0, as linhas excluídas são tratadas da mesma forma que linhas não excluídas.<br /><br /> Isso define a mesma opção **que Mostrar linhas excluídas** na caixa de diálogo de configuração.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção **que Description** na caixa de diálogo de configuração.|  
|DRIVER|A especificação do caminho para o driver DLL.|  
|DRIVERID|Uma id inteira para o motorista.<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|Fil|Tipo de arquivo dBase III, dBase IV ou dBase 5|  
|PAGETIMEOUT|Especifica o período de tempo, em décimos de segundo, que uma página (se não usada) permanece no buffer antes de ser removida. O padrão é 600 décimos de segundo (60 segundos). Observe que essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> Isso define a mesma opção que **o Tempo de página** na caixa de diálogo de configuração.|  
|READONLY|TRUE para tornar somente leitura de arquivo; FALSO para fazer o arquivo não ler somente.<br /><br /> Isso define a mesma opção **que Read Only** na caixa de diálogo de configuração.|  
|STATISTICS|Para o driver dBASE, determina se as estatísticas de tamanho da tabela são aproximadas. Observe que essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> Isso define a mesma opção **que contagem aproximada de linha** na caixa de diálogo de configuração.|  
|Tópicos|O número de roscas de fundo para o motor usar. Este valor é 3 e não pode ser alterado.<br /><br /> Isso define a mesma opção **que os Threads** na caixa de diálogo de configuração.|
