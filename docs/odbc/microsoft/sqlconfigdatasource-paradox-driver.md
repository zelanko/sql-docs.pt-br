---
title: SQLConfigDataSource (driver do Paradox) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 33cc778d921b90a460dab6bda352fd7627d2cf7b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68054075"
---
# <a name="sqlconfigdatasource-paradox-driver"></a>SQLConfigDataSource (Driver do Paradox)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver do Paradox. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 A função **SQLConfigDataSource** que é usada para adicionar, modificar ou excluir uma fonte de dados usa dinamicamente as seguintes palavras-chave.  
  
|Palavra-chave|DESCRIÇÃO|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|A sequência na qual os campos são classificados.<br /><br /> Quando o driver do Paradox é usado, a sequência pode ser ASCII (padrão), internacional, sueco-finlandês ou norueguês-dinamarquês.<br /><br /> Isso define a mesma opção que a **sequência de agrupamento** na caixa de diálogo de instalação.|  
|DBQ|O nome do arquivo de banco de dados.<br /><br /> Isso define a mesma opção que o **banco de dados** na caixa de diálogo de instalação.|  
|DEFAULTDIR|A especificação de caminho para o diretório.|  
|DESCRIÇÃO|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção que a **Descrição** na caixa de diálogo de instalação.|  
|DRIVER|A especificação de caminho para a DLL do driver.|  
|DRIVERid|Uma ID de inteiro para o driver.<br /><br /> 26 (Paradox 3. x)<br /><br /> 282 (Paradox 4. x)<br /><br /> 538 (Paradox 5. x)|  
|Exclude|Determina se o banco de dados será aberto em modo exclusivo (acessado por apenas um usuário por vez) ou por um modo compartilhado (acessado por mais de um usuário de cada vez). Pode ser verdadeiro (modo exclusivo) ou falso (modo compartilhado).<br /><br /> Isso define a mesma opção como **exclusiva** na caixa de diálogo de instalação.|  
|FIL|Tipo de arquivo Paradox 3. x, Paradox 4. x ou Paradox 5. x|  
|Talvez|Tipo de arquivo do driver de texto (texto).|  
|PAGETIMEOUT|Especifica o período de tempo, em décimos de segundo, que uma página (se não usada) permanece no buffer antes de ser removida. O padrão é 600 décimos de segundo (60 segundos). Observe que essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> Isso define a mesma opção como **tempo limite de página** na caixa de diálogo de instalação.|  
|PARADOXNETPATH|O caminho completo do diretório que contém um banco de dados de bloqueio do Paradox, pois ele contém o arquivo PDOXUSRS.net (no Paradox 4.* x*) ou o arquivo Paradox.net (no Paradox 5.* x*). Se o diretório não contiver um desses arquivos, o driver do Paradox criará um. Para obter informações sobre esses arquivos, consulte a documentação do Paradox.<br /><br /> Antes que um diretório de rede possa ser selecionado, um nome de usuário do Paradox deve ser inserido.<br /><br /> Isso define a mesma opção que **Selecionar diretório de rede** na caixa de diálogo de instalação.|  
|PARADOXNETSTYLE|Para o driver do Paradox, o estilo de acesso à rede a ser usado ao acessar dados do Paradox: "3. x" para o Paradox 3. *x* ou "4. x" para o Paradox 4. *x* ou 5. *x*. Pode ser definido como "3. x" ou "4. x" se a versão for o Paradox 4. *x* ou 5. *x*; se a versão for o Paradox 3. *x*, o estilo deve ser "3. x".<br /><br /> Isso define a mesma opção como **net Style** na caixa de diálogo de instalação.|  
|PARADOXUSERNAME|Para o driver do Paradox, o nome de usuário do Paradox.<br /><br /> Isso define a mesma opção como **nome de usuário** na caixa de diálogo de instalação.|  
|PWD|A senha.<br /><br /> Essa é uma palavra-chave opcional e nunca será gravada no arquivo pelo driver. Ele é usado em uma chamada para **SQLDriverConnect** em relação aos arquivos do Paradox protegidos por senha. A senha usada será válida sempre que uma tabela for aberta. Se nenhuma senha for passada na cadeia de conexão, nenhuma senha será estabelecida para essa tabela. Se as tabelas tiverem senhas diferentes, mais de uma não poderá ser aberta na mesma sessão, nem as tabelas poderão ser Unidas.|  
|READONLY|TRUE para tornar o arquivo somente leitura; FALSE para tornar o arquivo não somente leitura.<br /><br /> Isso define a mesma opção como **somente leitura** na caixa de diálogo de instalação.|  
|THREADS|O número de threads em segundo plano a ser usado pelo mecanismo. Esse valor é 3 e não pode ser alterado.<br /><br /> Isso define a mesma opção que os **threads** na caixa de diálogo de instalação.|
