---
title: SQLConfigDataSource (Driver Paradoxo) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLConfigDataSource
ms.assetid: 59e84c4e-debe-49d7-b97b-84c736b0c793
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68e60d7ca9c37865c1b265297d24591638a44965
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283926"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (Driver do Paradox)
> [!NOTE]  
>  Este tópico fornece informações específicas do Paradox Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 A função **SQLConfigDataSource,** usada para adicionar, modificar ou excluir uma fonte de dados, usa dinamicamente as seguintes palavras-chave.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|SEQÜÊNCIA DE COLISÃO|A seqüência em que os campos são classificados.<br /><br /> Quando o driver Paradoxé é usado, a seqüência pode ser ASCII (padrão), internacional, sueco-finlandês ou norueguês-dinamarquês.<br /><br /> Isso define a mesma opção **que A seqüência de colisão** na caixa de diálogo de configuração.|  
|Dbq|O nome do arquivo do banco de dados.<br /><br /> Isso define a mesma opção que o **Banco de Dados** na caixa de diálogo de configuração.|  
|Defaultdir|A especificação do caminho para o diretório.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção **que Description** na caixa de diálogo de configuração.|  
|DRIVER|A especificação do caminho para o driver DLL.|  
|DRIVERID|Uma id inteira para o motorista.<br /><br /> 26 (Paradoxo 3.x)<br /><br /> 282 (Paradoxo 4.x)<br /><br /> 538 (Paradoxo 5.x)|  
|Exclusivo|Determina se o banco de dados será aberto no modo exclusivo (acessado por apenas um usuário por vez) ou no modo compartilhado (acessado por mais de um usuário por vez). Pode ser verdadeiro (modo exclusivo) ou falso (modo compartilhado).<br /><br /> Isso define a mesma opção **que Exclusive** na caixa de diálogo de configuração.|  
|Fil|Tipo de arquivo Paradox 3.x, Paradox o 4.x ou Paradoxo 5.x|  
|Filetype|Tipo de arquivo para o driver texto (Texto).|  
|PAGETIMEOUT|Especifica o período de tempo, em décimos de segundo, que uma página (se não usada) permanece no buffer antes de ser removida. O padrão é 600 décimos de segundo (60 segundos). Observe que essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> Isso define a mesma opção que **o Tempo de página** na caixa de diálogo de configuração.|  
|PARADOXNETPATH|O caminho completo do diretório contendo um banco de dados de bloqueio paradoxo, porque contém o arquivo PDOXUSRS.net (no Paradox4.* x*) ou o arquivo PARADOX.net (no Paradoxo 5.* x*). Se o diretório não contiver um desses arquivos, o driver Paradoxo criará um. Para obter informações sobre esses arquivos, consulte a documentação do Paradoxo.<br /><br /> Antes que um diretório de rede possa ser selecionado, um nome de usuário do Paradox deve ser inserido.<br /><br /> Isso define a mesma opção que **Selecionar diretório de rede** na caixa de diálogo de configuração.|  
|PARADOXNETSTYLE|Para o driver Paradox, o estilo de acesso à rede a ser usado ao acessar dados do Paradox: ou "3.x" para Paradox3. *x* ou "4.x" para Paradoxo 4. *x* ou 5. *x*. Pode ser definido como "3.x" ou "4.x" se a versão for Paradox 4. *x* ou 5. *x*; se a versão é Paradoxo 3. *x*, o estilo deve ser "3.x".<br /><br /> Isso define a mesma opção que o **Net Style** na caixa de diálogo de configuração.|  
|NOME PARADOXUSER|Para o driver Paradox, o nome de usuário Paradox.<br /><br /> Isso define a mesma opção **que nome de usuário** na caixa de diálogo de configuração.|  
|PWD|A senha.<br /><br /> Esta é uma palavra-chave opcional e nunca será escrita no arquivo pelo motorista. Ele é usado em uma chamada para **SQLDriverConnect** contra arquivos Paradox protegidos por senha. A senha usada será válida sempre que uma tabela for aberta. Se nenhuma senha for passada na seqüência de conexão, nenhuma senha será estabelecida para essa tabela. Se as tabelas tiverem senhas diferentes, mais de uma não poderá ser aberta na mesma sessão, nem as mesas podem ser aderidas.|  
|READONLY|TRUE para tornar somente leitura de arquivo; FALSO para fazer o arquivo não ler somente.<br /><br /> Isso define a mesma opção **que Read Only** na caixa de diálogo de configuração.|  
|Tópicos|O número de roscas de fundo para o motor usar. Este valor é 3, e não pode ser alterado.<br /><br /> Isso define a mesma opção **que os Threads** na caixa de diálogo de configuração.|
